# Grundsystem: Tiefsetzsteller (Buck-Konverter)

Dieses Dokument fasst die **konzeptionelle und mathematische Grundlage** des Grundsystems aus den Quellen  
`Grundlagen_PhyModel.tex` und `Regelung_lin_nonlin.tex` zusammen.

## 1) Systemgrenzen und Signale

- Strecke: Tiefsetzsteller mit Induktivität \(L\), Ausgangskondensator \(C\), Lastwiderstand \(R\)
- Eingang: \(U_{in,P}\)
- Stellgröße: Tastverhältnis \(\tau_g\)
- Ausgang/Regelgröße: Kondensatorspannung \(u_{C,P}\) (normiert: \(u_C\))
- Störgröße: Laststrom \(i_{R,P}\) (normiert: \(i_R\), im Blockbild als \(z\); formale Definition in Abschnitt 4)

## 2) Physikalisches Modell (nicht normiert)

\[
\overline{e} = \tau_g \, U_{in,P}
\]
\[
u_{L,P} = L \frac{d i_{L,P}}{dt}
\]
\[
i_{C,P} = C \frac{d u_{C,P}}{dt}
\]
\[
u_{C,P} = R\,i_{R,P}
\]
\[
i_{L,P} = i_{C,P} + i_{R,P}
\]
\[
u_{L,P} = \overline{e} - u_{C,P}
\]

## 3) Normierung

Referenzgrößen: \(U_N\), \(I_N\)

\[
T_L=\frac{L I_N}{U_N}, \qquad T_C=\frac{C U_N}{I_N}
\]
\[
u_L=\frac{u_{L,P}}{U_N},\;
u_C=\frac{u_{C,P}}{U_N},\;
u_{in}=\frac{u_{in,P}}{U_N},\;
e=\frac{\overline{e}}{U_N}
\]
\[
i_L=\frac{i_{L,P}}{I_N},\;
i_C=\frac{i_{C,P}}{I_N},\;
i_R=\frac{i_{R,P}}{I_N}
\]
\[
e=\tau_g\,u_{in}
\]

## 4) Normiertes Grundsystem (Zeitbereich)

Mit \(z \equiv i_R\):
\[
\dot{i}_L = \frac{1}{T_L}(e-u_C)
\]
\[
\dot{u}_C = \frac{1}{T_C}(i_L-z)
\]
\[
e=\tau_g\,u_{in}
\]

Äquivalent als Zustandsmodell mit \(x=[i_L,\;u_C]^T\):
\[
\dot{x}=
\begin{bmatrix}
0 & -\frac{1}{T_L}\\[2mm]
\frac{1}{T_C} & 0
\end{bmatrix}x+
\begin{bmatrix}
\frac{1}{T_L}\\[2mm]
0
\end{bmatrix}e+
\begin{bmatrix}
0\\[2mm]
-\frac{1}{T_C}
\end{bmatrix}z
\]

## 5) Laplace-/Blockdarstellung der Strecke

\[
u_L = pT_L\,i_L \;\Longleftrightarrow\; i_L=\frac{1}{pT_L}u_L
\]
\[
i_C = pT_C\,u_C \;\Longleftrightarrow\; u_C=\frac{1}{pT_C}i_C
\]
\[
u_L=e-u_C,\qquad i_C=i_L-z,\qquad e=\tau_g u_{in}
\]

Damit ist das regelungstechnische Blockschaltbild des Tiefsetzstellers vollständig bestimmt.

## 6) Lastmodell (aus Grundgleichungen)

\[
i_{R,P}=\frac{u_{C,P}}{R}
\quad\Rightarrow\quad
i_R=\frac{U_N}{R I_N}\,u_C
\]

Ein Lastsprung kann als Sprung in \(R\) (bzw. in \(\frac{U_N}{R I_N}\)) modelliert werden.

## 7) Bezug zur klassischen Kaskadenregelung (für Kontext)

Aus `Regelung_lin_nonlin.tex`:

- Unterlagerte Stromregelung:
  \[
  F_R(p)=\frac{i_L}{i_{L,\mathrm{soll}}}
  =\frac{K}{K_1K+pT_L}
  \]
  mit
  \[
  K_1=1,\qquad K=\frac{T_L}{T_{\mathrm{Strom}}},\qquad K_2=-\frac{1}{K}
  \]

- Überlagerte Spannungsregelung (ohne/mit Bypass-I-Regler) basiert auf
  \[
  F_R(p)=\frac{u_C}{u_{C,\mathrm{soll}}^*}
  =\frac{C}{C C_1+pT_C}
  \]
  sowie den in der Quelle angegebenen Parametrierbeziehungen für \(C_1\), \(C\), \(C_w^*\), \(T_{Sp}^*\).

Diese Reglergleichungen sind **nicht** das Streckenmodell selbst, aber wichtig als Referenz für spätere KI-Regelungsansätze.

## 8) Abbildungen (Quellen im Repository)

- Physikalisches Schaltbild: `gfx/TSS_phy_s.pdf`
- Regelungstechnisches Blockschaltbild: `gfx/TSS_RBS.pdf`
- Stromregelung: `gfx/TSS_Stromregelung.pdf`
- Spannungsregelung: `gfx/TSS_Spannungsregelung.pdf`

Falls dein Markdown-Viewer keine PDF-Einbettung unterstützt, bitte die Grafiken manuell als PNG/SVG bereitstellen oder konvertieren.
