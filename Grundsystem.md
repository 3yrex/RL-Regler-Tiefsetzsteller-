# Common Ground / Ground Truth: Grundsystem „Tiefsetzsteller (Buck) + KI-Regelung“

Dieses Dokument bündelt **alle im Gespräch festgelegten Informationen** zum Grundsystem und den Randbedingungen. Es dient als **Common Ground** für andere Sprachmodelle/Agenten (konzeptionell, keine Umsetzung).

---

## 1) Grundziel (Regelungsaufgabe)
Ziel ist die autonome Regelung eines **Tiefsetzstellers (Buck-Konverter)** mit einer KI/NN/RL-Policy.

- **Regelgröße (Output):** normierte Kondensatorspannung  
  \[
  u_C(t) \in [0,1] \quad (\text{normiert auf } U_N)
  \]
- **Sollwert / Referenz:**  
  - Start: **konstanter Sollwert**
  - Ausbauziel: **Sollwertsprünge (Steps)**, später **Rampen**
  - Sollwertintervall:
    \[
    u_{C,\mathrm{ref}} \in [0.1,\ 0.9]
    \]
- **Stellgröße (Control Input):** Duty Cycle / Tastverhältnis  
  \[
  \tau_g(t) \in [0,1]
  \]
  Dieses Signal wird **von der KI ausgegeben** (Policy-Output).

**Wichtig:** Es soll **keine klassische Referenzreglerstruktur** (z.B. PI, klassisches MPC) als Controller verwendet werden. Schutz-/Sättigungsblöcke sind zulässig (Safety/Clamping), da sie nicht der Regelstrategie entsprechen, sondern den Modell-/Hardwaregrenzen.

---

## 2) Grundmodell (aus Bachelorarbeit, Abschnitt „Tiefsetzsteller“)

### 2.1 Physikalische Gleichungen (mit Index „P“)
1) PWM-/Modulator-Mittelwert:
\[
\overline{e} = \tau_g \cdot U_{in,P}
\]

2) Induktivität:
\[
u_{L,P} = L \cdot \frac{d i_{L,P}}{dt}
\]

3) Kondensator:
\[
i_{C,P} = C \cdot \frac{d u_{C,P}}{dt}
\]

4) Ohmsche Last:
\[
u_{C,P} = R \cdot i_{R,P}
\quad\Leftrightarrow\quad
i_{R,P}=\frac{u_{C,P}}{R}
\]

5) Knoten (Ausgangsknoten):
\[
i_{L,P} = i_{C,P} + i_{R,P}
\]

6) Masche (Induktorspannung):
\[
u_{L,P} = \overline{e} - u_{C,P}
\]

**Definition der Störung:**
- Im Chat und in der Herleitung wird der **Laststrom** als Störung bezeichnet:
  \[
  z \equiv i_{R,P}
  \]
  bzw. normiert:
  \[
  z \equiv i_R
  \]
- Hinweis: Im LaTeX-Ausschnitt ist in Gleichung (6) die Markierung „=z“ unter \(u_{C,P}\) sehr wahrscheinlich ein Tippfehler. Für dieses Common-Ground-Dokument gilt: **z ist Laststrom, nicht Kondensatorspannung**.

---

### 2.2 Normierung
Normiert wird auf \(U_N\) und \(I_N\). Relevante Definitionen:

- Zeitkonstanten:
\[
T_L = \frac{L \cdot I_N}{U_N}, \qquad
T_C = \frac{C \cdot U_N}{I_N}
\]

- Normierte Größen:
\[
u_L = \frac{u_{L,P}}{U_N},\;
u_C = \frac{u_{C,P}}{U_N},\;
u_{in} = \frac{u_{in,P}}{U_N}
\]
\[
i_L = \frac{i_{L,P}}{I_N},\;
i_C = \frac{i_{C,P}}{I_N},\;
i_R = \frac{i_{R,P}}{I_N}
\]
\[
e = \frac{\overline{e}}{U_N}
\]

Aus (1) folgt **explizit** (normiert):
\[
e = \tau_g \, u_{in}
\]

---

### 2.3 Zeitbereichsdarstellung (ODE) des normierten Grundsystems
Das Blockbild entspricht genau folgendem normierten Zustandsmodell mit Zuständen \([i_L,\ u_C]^T\):

- Induktordynamik:
\[
\dot i_L = \frac{1}{T_L}\,(u_L)
          = \frac{1}{T_L}\,(e-u_C)
\]

- Kondensatordynamik (aus \(i_C = i_L - z\) und \(i_C = T_C \dot u_C\)):
\[
\dot u_C = \frac{1}{T_C}\,(i_C)
         = \frac{1}{T_C}\,(i_L - z)
\]

mit
\[
e=\tau_g\,u_{in}
\]

---

### 2.4 Laplace-/Blockdarstellung
Im Laplace-Bereich (mit \(p\) als Laplace-Variable):

\[
u_L = i_L \, p T_L \quad\Leftrightarrow\quad i_L=\frac{1}{pT_L}u_L
\]
\[
i_C = u_C \, p T_C \quad\Leftrightarrow\quad u_C=\frac{1}{pT_C}i_C
\]
\[
u_L = e - u_C,\qquad i_C=i_L-z,\qquad e=\tau_g u_{in}
\]

---

## 3) Last-/Störmodell (Chat-Festlegung)
Die Last wird als **paralleler Widerstand \(R\)** am Ausgang modelliert, der **variieren oder springen** kann.

Physikalisch:
\[
i_{R,P}=\frac{u_{C,P}}{R}
\]

Normiert ergibt sich allgemein:
\[
i_R = \frac{u_{C,P}}{R}\cdot\frac{1}{I_N}
    = \frac{U_N}{R\,I_N}\,u_C
    = k_R\,u_C
\]
mit
\[
k_R=\frac{U_N}{R\,I_N}
\]
Ein Lastsprung entspricht einem Sprung in \(R\) bzw. \(k_R\).

> Für die Untersuchung können zwei Störmodelle betrachtet werden:
> 1) „Explizites z“: z wird als (messbarer) Laststrom behandelt.
> 2) „R-Last“: z ergibt sich implizit über \(R\) (bzw. \(k_R\)).

---

## 4) Messbarkeit / Beobachtungen (Machbarkeit, ideal)
Im Machbarkeitsszenario: **ideal**, kein Rauschen, keine Delays, so simpel wie möglich.

Verfügbare Signale (grundsätzlich):
- \(u_C\): ja
- \(i_L\): ja
- \(u_{in}\): ja
- \(z\): wird in zwei Varianten geprüft:
  - **z beobachtbar**
  - **z nicht beobachtbar**

---

## 5) Sättigungen / Grenzen / Safety (Chat-Festlegung)
- Alle relevanten normierten Größen sind auf Maximalwert 1 bezogen.
- Ein **Sättigungsblock** verhindert Werte **> 1** (Hard-Clipping).
- Umgang mit negativen Werten ist **noch offen** (darf später entschieden werden).

Optional/experimentell:
- Rate-Limit (oder Metrik) für \(\Delta\tau_g\) ist interessant, bleibt zunächst offen.

---

## 6) Fokus der Studie (Vorgehensidee)
- Start: **einfachstes Machbarkeitsszenario** (ideal, averaged, konstante Referenz).
- Danach: Steps → Rampen → Lastsprünge (R-Sprünge) → Robustheitserweiterungen.

---

## 7) Begriffs-Mapping (eindeutig)
- \(\tau_g\): Stellgröße / Duty Cycle (KI-Output)
- \(u_C\): Regelgröße / Kondensatorspannung (normiert)
- \(z\): Störung = Laststrom \(i_R\) (normiert oder physikalisch)
- \(u_{in}\): Eingangsspannung (normiert)
- \(T_L, T_C\): normierte Zeitkonstanten aus L und C
