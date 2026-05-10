# Wissenschaftliche Recherche: Reinforcement Learning zur Regelung von Tiefsetzstellern

## 1. Zielsetzung und Forschungsfrage

Diese Recherche untersucht, ob die in diesem Repository formulierte Grundidee bereits in der Fachliteratur oder in öffentlich zugänglichen Implementierungen umgesetzt wurde. Ausgangspunkt ist das in `Grundsystem.md` und `Grundlagen_Tiefsetzsteller.md` beschriebene Konzept:

- Regelung eines **Tiefsetzstellers (Buck-Konverters)**,
- **direkte Ausgabe des Duty-Cycle** durch eine RL-Policy,
- **Spannungsregelung** als primäre Regelungsaufgabe,
- Start mit einem **idealen gemittelten Modell**,
- spätere Erweiterung um **Sollwertsprünge, Rampen und Lastsprünge**.

Daraus ergibt sich folgende Forschungsfrage:

> **Ist die RL-basierte direkte Regelung eines Buck-Konverters über das Tastverhältnis bereits Stand der Forschung, und in welchem Ausmaß entspricht bestehende Literatur dem hier verfolgten regelungstechnischen Ansatz?**

---

## 2. Methodisches Vorgehen

Die Recherche wurde auf Arbeiten aus den Bereichen **Reinforcement Learning**, **Regelungstechnik** und **Leistungselektronik** eingegrenzt. Berücksichtigt wurden nur Quellen, die inhaltlich mindestens einen der folgenden Punkte abdecken:

1. RL-basierte Regelung von **Buck- oder verwandten DC-DC-Wandlern**,
2. **direkte Stellgrößenbildung** über Duty-Cycle bzw. Duty-Ratio,
3. Fokus auf **Spannungsregelung** oder eng verwandte Aufgaben,
4. methodische Nähe zu modellbasierten oder gemittelten Wandlerbeschreibungen.

Die Auswertung ist zweigeteilt:

- **wissenschaftliche Literatur / paper-nahe Quellen**,
- **öffentliche GitHub-Repositories als gesonderte Implementierungsquellen**.

Hinweis zur Quellenlage: Einige Verlagsseiten waren aus der Laufzeitumgebung nicht direkt abrufbar. In diesen Fällen wurden öffentlich sichtbare Repository-Angaben, README-Texte und offen zugängliche Projektbeschreibungen als Sekundärbeleg genutzt. Für eine formale Abschlussarbeit sollten diese Angaben später zusätzlich über Bibliothekszugänge oder DOI-Recherche verifiziert werden.

---

## 3. Einordnung des Repository-Konzepts

Das vorliegende Repository positioniert sich im Kern als **regelungstechnische Machbarkeitsstudie** für RL auf einem Tiefsetzsteller. Charakteristisch sind dabei:

- physikalisch motivierte Zustandsgrößen wie \(i_L\) und \(u_C\),
- eine direkt lernende Policy für \(\tau_g\),
- der Verzicht auf eine klassische PI- oder MPC-Reglerstruktur als eigentlichen Regler,
- ein sukzessiver Ausbau von der einfachen Referenzfolge hin zu Stör- und Robustheitsfragen.

Damit liegt das Projekt in einem Forschungsfeld, das zwischen **datengetriebener Regelung**, **RL in physikalischen Systemen** und **Leistungselektronikregelung** angesiedelt ist.

---

## 4. Wissenschaftliche Literaturübersicht

### 4.1 Hochrelevante wissenschaftliche Quellen

#### 4.1.1 Yang et al.: RL-basierte Spannungsregelung von Buck-Konvertern mit CPL

Im Repository `tianxiaoy9/Data-driven-deep-reinforcement-learning-controller-for-DC-DC-buck-converter-feeding-CPLs` werden drei einschlägige Arbeiten genannt:

1. **Voltage Regulation of DC-DC Buck Converters Feeding CPLs via Deep Reinforcement Learning**
2. **Implementation of Transferring Reinforcement Learning for DC–DC Buck Converter Control via Duty Ratio Mapping**
3. **Robustness enhancement of DRL controller for DC–DC buck converters fusing ESO**

Diese Arbeiten sind für das vorliegende Repository von **höchster Relevanz**, weil sie die gleiche Grundlogik verfolgen:

- Buck-Konverter als Regelstrecke,
- RL als primäre Reglerinstanz,
- direkte Beeinflussung des **Duty-Ratio**,
- Spannungsregelung als Zielgröße.

Aus wissenschaftlicher Sicht ist besonders bedeutsam, dass hier nicht nur eine abstrakte RL-Idee formuliert wird, sondern ein **konkretes Anwendungsfeld der Leistungselektronik** adressiert wird. Die Arbeiten belegen damit, dass RL für DC-DC-Wandlerregelung nicht nur konzeptionell denkbar, sondern bereits als Forschungsgegenstand etabliert ist.

**Passung zum Repo:** sehr hoch.

**Wesentliche Abweichung:**  
Der Schwerpunkt dieser Arbeiten liegt auf **Constant Power Loads (CPL)**. Das ist gegenüber einer reinen ohmschen Last ein anspruchsvolleres Lastmodell. Für das hiesige Repository bedeutet das: Die Grundidee ist bereits vorhanden, jedoch kann die eigene Arbeit durch eine klare Behandlung von **ohmscher Last, Lastsprung und normiertem Grundmodell** weiterhin einen eigenständigen Beitrag leisten.

---

#### 4.1.2 Lee et al.: RL-Regelung eines Buck-Konverters unter Berücksichtigung von Zeitverzögerungen

Das Repository `KimDaevvon/RL_Buck_Converter` verweist explizit auf die Arbeit:

**Reinforcement Learning-Based Control of DC–DC Buck Converter Considering Controller Time Delay** (2024).

Diese Quelle ist wissenschaftlich besonders relevant, weil sie das Grundproblem über das reine Machbarkeitsszenario hinaus erweitert. Die Berücksichtigung von **Controller-Zeitverzögerungen** adressiert einen für die praktische Regelung entscheidenden Aspekt, der in idealisierten RL-Umgebungen häufig zunächst ausgeblendet wird.

**Passung zum Repo:** hoch.

**Wissenschaftliche Bedeutung:**  
Die Arbeit zeigt, dass RL-basierte Buck-Regelung nicht nur unter idealisierten Simulationsannahmen untersucht wird, sondern bereits in Richtung **implementierungsnaher Randbedingungen** weiterentwickelt wurde. Für eine wissenschaftliche Arbeit ist das wichtig, weil sich daraus eine Entwicklungslinie ableiten lässt:

1. gemitteltes Idealmodell,  
2. Referenz- und Lastvariation,  
3. Berücksichtigung realer Verzögerungen,  
4. später ggf. Hardwaretransfer.

---

### 4.2 Teilweise hochrelevante, methodisch nahe Quellen

#### 4.2.1 DDPG für Buck-Konverter

Das Repository `pabloajimenezc/DDPG-DC-DC-Converter` beschreibt eine MATLAB-/Simulink-Umgebung, in der ein **DDPG-Agent** für die Regelung eines DC-DC-Buck-Konverters trainiert wird.

Aus wissenschaftlicher Perspektive ist diese Quelle vor allem deshalb relevant, weil sie den Übergang von der allgemeinen Fragestellung „Kann RL einen Buck-Konverter regeln?“ hin zur konkreten Wahl eines **kontinuierlichen Actor-Critic-Verfahrens** markiert. DDPG ist insbesondere dann naheliegend, wenn das Tastverhältnis nicht nur aus einer kleinen diskreten Menge, sondern als nahezu kontinuierliche Stellgröße behandelt werden soll.

**Passung zum Repo:** hoch.

**Abweichung:**  
Die öffentlich sichtbare Materiallage ist stärker implementierungsorientiert als theoretisch begründet. Als Primärquelle für eine wissenschaftliche Argumentation ist dieses Repository daher schwächer als die paper-nahen Yang-Arbeiten, aber als methodischer Nachweis weiterhin wertvoll.

---

#### 4.2.2 Reinforcement Learning als Duty-Cycle-Regler eines Buck-Konverters

Das Repository `abdalremal/Power-Converter-RL` beschreibt RL ausdrücklich als Verfahren zur Regelung des Duty-Cycle und damit der Ausgangsspannung eines 24:12V-Buck-Konverters. Im sichtbaren MATLAB-Code werden Beobachtungen wie **integrierter Fehler, Fehler und Ausgangsspannung** sowie ein **DDPG-Agent** verwendet.

Für eine wissenschaftliche Einordnung ist diese Quelle interessant, weil sie zeigt, dass es innerhalb des Themenfelds zwei nahe, aber unterschiedliche Modellierungsphilosophien gibt:

- **physikalisch strukturierte Zustandswahl** wie \(i_L, u_C\),
- **tracking-orientierte Beobachtungswahl** wie Fehler, integrierter Fehler, Ausgangsspannung.

**Passung zum Repo:** hoch.

**Abweichung:**  
Das hier beschriebene Repository arbeitet stärker mit fehlerbasierten Beobachtungen; das hiesige Projekt ist stärker an einer regelungstechnisch-physikalischen Zustandsbeschreibung orientiert.

---

### 4.3 Methodisch verwandte, aber nicht deckungsgleiche Literatur

#### 4.3.1 PPO-LSTM für Buck-Boost-Konverter

Das Repository `KevinKoay/PPO-LSTM-deep-reinforcement-learning-based-controller-for-buck-boost-converter-with-constant-power-l` dokumentiert eine RL-Regelung eines **Buck-Boost-Konverters** mittels **PPO** und rekurrenten Anteilen.

Wissenschaftlich ist diese Quelle vor allem für die **Methodenwahl** relevant. Sie zeigt:

- PPO ist im Wandlerkontext einsetzbar,
- rekurrente Strukturen werden genutzt, wenn zeitliche Abhängigkeiten besonders wichtig sind,
- der RL-Einsatz ist nicht auf Buck-Konverter beschränkt, sondern auf verwandte Topologien ausdehnbar.

**Passung zum Repo:** mittel bis hoch.

**Abweichung:**  
Topologie und Lastannahme unterscheiden sich; daher ist diese Quelle eher für den **Methodenvergleich** als für den direkten Stand-der-Technik-Abgleich geeignet.

---

#### 4.3.2 Hybridregelung aus PID und RL

Das Repository `PVasantharajan/rl-dc-dc-converter-control` beschreibt einen Buck-Konverter im **averaged model**, kombiniert jedoch klassische PID-Schleifen mit einem PPO-basierten Residualagenten.

Diese Quelle ist wissenschaftlich relevant, weil sie eine alternative Position im Forschungsfeld sichtbar macht: RL wird nicht zwingend als vollständiger Ersatz klassischer Regelung, sondern auch als **Ergänzung oder Residualregler** eingesetzt.

**Passung zum Repo:** mittel.

**Abweichung:**  
Das hier verfolgte Repository möchte gerade keinen klassischen Regler als zentrale Regelstrategie verwenden. Damit markiert diese Quelle eher einen **Kontrastfall** innerhalb der Literatur.

---

## 5. Synthese der Literatur

Die ausgewerteten wissenschaftlichen Quellen lassen drei zentrale Aussagen zu:

### 5.1 Die Grundidee ist nicht neu

Die Kombination aus

- Buck-Konverter,
- RL-basierter Regelung,
- direkter oder nahezu direkter Duty-Cycle-Bildung,
- Spannungsregelung als Ziel

ist bereits mehrfach untersucht worden. Insbesondere die Yang-Arbeiten belegen dies sehr deutlich.

### 5.2 Der wissenschaftliche Mehrwert liegt in der konkreten Ausgestaltung

Neuheit entsteht im vorliegenden Themenfeld weniger durch die bloße Verwendung von RL, sondern durch:

- die **präzise Modellwahl**,
- die **Zustands- und Beobachtungsdefinition**,
- die **Lastmodellierung**,
- die **Robustheitsbetrachtung**,
- und den **Vergleich zu klassischer Regelung**.

Für dieses Repository sind daher insbesondere folgende wissenschaftliche Beiträge denkbar:

1. systematischer Vergleich verschiedener RL-Verfahren unter identischer Strecke,  
2. Untersuchung der Beobachtbarkeit von Störgrößen wie \(z\),  
3. Vergleich von physikalisch motivierten und fehlerbasierten Beobachtungsvektoren,  
4. geordneter Übergang vom idealen gemittelten Modell zu realistischeren Szenarien.

### 5.3 Das Repo ist als wissenschaftlich strukturierte Reproduktions- und Vergleichsarbeit gut begründbar

Auch wenn die Grundidee bereits bekannt ist, bleibt die Arbeit wissenschaftlich sinnvoll. Gerade in der Regelungstechnik ist eine **saubere Reproduktion**, **systematische Variation der Modellannahmen** und **transparente Methodik** häufig wertvoller als ein nur formal neuer, aber schlecht nachvollziehbarer Ansatz.

---

## 6. Gesonderte Übersicht öffentlicher GitHub-Repositories

Die folgenden Repositories werden **bewusst getrennt** von der eigentlichen Literaturübersicht aufgeführt. Sie sind als **Implementierungs-, Reproduktions- oder Demonstrationsquellen** nützlich, besitzen aber nicht automatisch den Status einer begutachteten wissenschaftlichen Primärquelle.

### 6.1 Repositories mit sehr hoher Relevanz

1. **tianxiaoy9/Data-driven-deep-reinforcement-learning-controller-for-DC-DC-buck-converter-feeding-CPLs**  
   Sehr hohe Relevanz, da direkt Paper-bezogen und thematisch nahezu deckungsgleich.

2. **KimDaevvon/RL_Buck_Converter**  
   Hohe Relevanz als Reproduktionsquelle mit explizitem Bezug auf ein Buck-RL-Paper.

3. **pabloajimenezc/DDPG-DC-DC-Converter**  
   Hohe Relevanz als konkrete MATLAB-/Simulink-Implementierung für Buck + DDPG.

4. **abdalremal/Power-Converter-RL**  
   Hohe Relevanz, da RL explizit als Duty-Cycle-Regler für Buck-Spannungsregelung formuliert wird.

### 6.2 Repositories mit mittlerer Relevanz

5. **KevinKoay/PPO-LSTM-deep-reinforcement-learning-based-controller-for-buck-boost-converter-with-constant-power-l**  
   Methodisch sehr interessant, aber andere Wandlerstruktur.

6. **PVasantharajan/rl-dc-dc-converter-control**  
   Relevant als Hybridansatz, jedoch nicht als rein RL-basierter Regler.

7. **Solaire-42/RaspberryPyReinforcementLearningControlPowerElectronicSystems**  
   Besonders interessant für spätere Hardwareperspektive, aber nur teilweise deckungsgleich mit dem Grundmodell dieses Repositories.

### 6.3 Repositories mit eher angrenzender Relevanz

8. **SmartSystems-UniAndes/Train_and_Convert_RL_MPPT**  
   Relevant als RL-Anwendung am Buck-Konverter, jedoch mit Schwerpunkt MPPT statt klassischer Spannungsregelung.

---

## 7. Schlussfolgerung für eine wissenschaftliche Arbeit

Für eine wissenschaftliche Arbeit lässt sich der Stand der Recherche wie folgt verdichten:

1. **Die Grundidee ist bereits umgesetzt worden.**  
   RL-basierte Buck-Regelung über Duty-Cycle ist kein unbearbeitetes Neuland mehr.

2. **Die thematisch passendsten Quellen stammen aus der Schnittmenge von RL und Leistungselektronik.**  
   Besonders relevant sind paper-nahe Arbeiten zu Buck-Konvertern mit Spannungsregelung und direkter Duty-Ratio-Bildung.

3. **Ein tragfähiger wissenschaftlicher Beitrag liegt in der Systematik.**  
   Das Repository kann dennoch eine sinnvolle wissenschaftliche Arbeit stützen, wenn es nicht bloß „RL auf Buck“ wiederholt, sondern methodisch sauber strukturiert:
   - klares Grundmodell,
   - definierte Beobachtungsräume,
   - definierte Lastfälle,
   - nachvollziehbarer Vergleich klassischer und RL-basierter Regelung,
   - Auswertung von Robustheit und Generalisierungsverhalten.

4. **Die GitHub-Repositories sollten in einer Arbeit nicht mit Paperquellen vermischt werden.**  
   Sie sind als Implementierungs- und Reproduktionsbelege wertvoll, sollten aber formal gesondert von der Primärliteratur geführt werden.

---

## 8. Literaturverzeichnis

### 8.1 Wissenschaftliche bzw. paper-nahe Quellen

1. Yang, T. et al.: **Voltage Regulation of DC-DC Buck Converters Feeding CPLs via Deep Reinforcement Learning**. IEEE Xplore.  
   <https://ieeexplore.ieee.org/abstract/document/9521987>

2. Yang, T. et al.: **Implementation of Transferring Reinforcement Learning for DC–DC Buck Converter Control via Duty Ratio Mapping**. IEEE Xplore.  
   <https://ieeexplore.ieee.org/abstract/document/9841427>

3. Yang, T. et al.: **Robustness enhancement of DRL controller for DC–DC buck converters fusing ESO**. Taylor & Francis.  
   <https://www.tandfonline.com/doi/full/10.1080/23307706.2023.2201587>

4. Lee, D. et al. (laut Reproduktionsrepository): **Reinforcement Learning-Based Control of DC–DC Buck Converter Considering Controller Time Delay** (2024).  
   Paperhinweis über: <https://github.com/KimDaevvon/RL_Buck_Converter>

### 8.2 Gesonderte öffentliche GitHub-Repositories

1. `tianxiaoy9/Data-driven-deep-reinforcement-learning-controller-for-DC-DC-buck-converter-feeding-CPLs`  
   <https://github.com/tianxiaoy9/Data-driven-deep-reinforcement-learning-controller-for-DC-DC-buck-converter-feeding-CPLs>

2. `KimDaevvon/RL_Buck_Converter`  
   <https://github.com/KimDaevvon/RL_Buck_Converter>

3. `pabloajimenezc/DDPG-DC-DC-Converter`  
   <https://github.com/pabloajimenezc/DDPG-DC-DC-Converter>

4. `abdalremal/Power-Converter-RL`  
   <https://github.com/abdalremal/Power-Converter-RL>

5. `KevinKoay/PPO-LSTM-deep-reinforcement-learning-based-controller-for-buck-boost-converter-with-constant-power-l`  
   <https://github.com/KevinKoay/PPO-LSTM-deep-reinforcement-learning-based-controller-for-buck-boost-converter-with-constant-power-l>

6. `PVasantharajan/rl-dc-dc-converter-control`  
   <https://github.com/PVasantharajan/rl-dc-dc-converter-control>

7. `Solaire-42/RaspberryPyReinforcementLearningControlPowerElectronicSystems`  
   <https://github.com/Solaire-42/RaspberryPyReinforcementLearningControlPowerElectronicSystems>

8. `SmartSystems-UniAndes/Train_and_Convert_RL_MPPT`  
   <https://github.com/SmartSystems-UniAndes/Train_and_Convert_RL_MPPT>
