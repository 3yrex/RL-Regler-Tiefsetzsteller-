# Recherche: Reinforcement Learning in der Regelungstechnik für Tiefsetzsteller

## Ziel der Recherche

Untersucht wurde, ob die Grundidee dieses Repositories bereits in ähnlicher Form umgesetzt wurde:

- **RL-/KI-basierte Regelung eines Tiefsetzstellers (Buck-Konverters)**
- **direkte Vorgabe des Duty-Cycle / Tastverhältnisses**
- **Regelziel Spannungsregelung**
- **Fokus auf Regelungstechnik / Leistungselektronik**, nicht auf allgemeines RL

Als interne Referenz für das Repo-Konzept wurden insbesondere `/home/runner/work/RL-Regler-Tiefsetzsteller-/RL-Regler-Tiefsetzsteller-/Grundsystem.md` und `/home/runner/work/RL-Regler-Tiefsetzsteller-/RL-Regler-Tiefsetzsteller-/Grundlagen_Tiefsetzsteller.md` verwendet.

---

## Kurzfazit

**Ja – das Grundkonzept wurde bereits mehrfach umgesetzt.**

Es gibt bereits:

1. **direkt verwandte Arbeiten** zur RL-Regelung von Buck-Konvertern,
2. **mehrere öffentliche Implementierungen** in MATLAB/Simulink,
3. **Paper-Verweise** auf wissenschaftliche Veröffentlichungen mit sehr ähnlicher Zielsetzung.

Die Idee des Repositories ist also **fachlich relevant, aber nicht grundsätzlich neu**.  
Das mögliche Alleinstellungsmerkmal dieses Repos liegt eher in:

- der **sauberen deutschsprachigen Aufarbeitung**,
- der **systematischen Gegenüberstellung** zu klassischer Regelung,
- der **schrittweisen Untersuchung** von konstantem Sollwert, Sollwertsprüngen und Lastsprüngen,
- und einem möglichen **Vergleich mehrerer RL-Verfahren unter identischen Randbedingungen**.

---

## Vorgehen und Quellenlage

Die Recherche wurde auf **RL in der Regelungstechnik und leistungselektronischen Wandlern** fokussiert.  
Berücksichtigt wurden vor allem:

- Paper-Verweise in öffentlich zugänglichen Repositories,
- Reproduktions-Repositories,
- Implementierungen in MATLAB/Simulink,
- angrenzende Arbeiten, wenn sie methodisch ähnlich sind.

Hinweis: Einige Verlagsseiten waren aus der Laufzeitumgebung nicht direkt abrufbar. In diesen Fällen wurden **öffentlich sichtbare Repository-Beschreibungen und README-Dateien** als Quelle für Titel, Einordnung und Kontext genutzt.

---

## Abgleich mit dem Repo-Konzept

Das hiesige Repo beschreibt im Kern:

- einen **Buck-Konverter / Tiefsetzsteller**,
- eine **Policy**, die direkt das Tastverhältnis \(\tau_g\) ausgibt,
- eine **Spannungsregelung** über \(u_C\),
- einen Start im **idealen gemittelten Modell**,
- später mögliche Erweiterungen auf **Sollwertsprünge, Rampen und Lastsprünge**,
- optional beobachtbare Zustände wie **\(i_L\), \(u_C\)** und evtl. **Störgröße \(z\)**.

Genau diese Struktur taucht in mehreren RL-Arbeiten zur Leistungselektronik bereits auf.

---

## Hochrelevante Quellen

### 1) Tianxiao Yang et al. / Shanghai University of Electric Power

**Quelle:**  
Repository: `tianxiaoy9/Data-driven-deep-reinforcement-learning-controller-for-DC-DC-buck-converter-feeding-CPLs`  
<https://github.com/tianxiaoy9/Data-driven-deep-reinforcement-learning-controller-for-DC-DC-buck-converter-feeding-CPLs>

Im README dieses Repositories werden direkt drei thematisch passende Paper genannt:

1. **Voltage Regulation of DC-DC Buck Converters Feeding CPLs via Deep Reinforcement Learning**  
   <https://ieeexplore.ieee.org/abstract/document/9521987>
2. **Implementation of Transferring Reinforcement Learning for DC–DC Buck Converter Control via Duty Ratio Mapping**  
   <https://ieeexplore.ieee.org/abstract/document/9841427>
3. **Robustness enhancement of DRL controller for DC–DC buck converters fusing ESO**  
   <https://www.tandfonline.com/doi/full/10.1080/23307706.2023.2201587>

**Warum sehr relevant:**  
- Buck-Konverter  
- direkte RL-Regelung  
- Fokus auf Spannungsregelung  
- explizit auf **Duty-Ratio / Duty-Cycle-Control**

**Passung zum Repo:** **sehr hoch**

**Wichtige Unterschiede:**  
- der Fokus liegt dort stark auf **Constant Power Loads (CPL)** und damit auf einer anspruchsvolleren Lastklasse,  
- nicht primär auf der im hiesigen Repo beschriebenen ohmschen Last bzw. Lastsprung-Betrachtung.

**Bewertung:**  
Diese Quelle ist die stärkste Bestätigung dafür, dass die Grundidee „**Buck + RL + direkte Duty-Cycle-Regelung**“ bereits wissenschaftlich umgesetzt wurde.

---

### 2) Reproduktion eines Papers zu Buck-Convertern mit RL und Zeitverzögerung

**Quelle:**  
Repository: `KimDaevvon/RL_Buck_Converter`  
<https://github.com/KimDaevvon/RL_Buck_Converter>

Öffentliche Repository-Beschreibung:

> “Reproduction of a reinforcement learning controller for a DC–DC buck converter (based on: Donghun Lee et al., "Reinforcement Learning-Based Control of DC–DC Buck Converter Considering Controller Time Delay", 2024)”

**Warum relevant:**  
- erneut **Buck-Konverter**  
- erneut **RL-basierte Regelung**  
- expliziter Verweis auf eine wissenschaftliche Arbeit

**Passung zum Repo:** **hoch**

**Wichtige Unterschiede:**  
- Schwerpunkt auf **Controller-Zeitverzögerungen**, also einem praxisnäheren Aspekt,  
- damit bereits einen Schritt weiter als das im Repo formulierte ideale Machbarkeitsszenario.

**Bewertung:**  
Diese Quelle ist besonders wichtig, weil sie zeigt, dass das Thema nicht nur als Machbarkeitsstudie existiert, sondern bereits in Richtung **realistischere Implementierungsbedingungen** weitergedacht wurde.

---

### 3) DDPG-Implementierung für Buck-Konverter

**Quelle:**  
Repository: `pabloajimenezc/DDPG-DC-DC-Converter`  
<https://github.com/pabloajimenezc/DDPG-DC-DC-Converter>

Öffentliche Repository-Beschreibung:

> “With these you can run and train a custom reinforcement learning DDPG agent to control a DC-DC Buck Converter.”

**Warum relevant:**  
- Buck-Konverter  
- kontinuierliche RL-Regelung mit **DDPG**  
- MATLAB/Simulink-Umfeld

**Passung zum Repo:** **hoch**

**Wichtige Unterschiede:**  
- die öffentlich sichtbaren Informationen sind knapper als bei den Paper-nahen Repositories,  
- der Schwerpunkt liegt stärker auf der **praktischen Agentenimplementierung** als auf einer ausführlichen theoretischen Einordnung.

**Bewertung:**  
Die Quelle ist ein klarer Beleg dafür, dass die direkte RL-Regelung eines Buck-Konverters nicht nur theoretisch beschrieben, sondern auch als trainierbare MATLAB/Simulink-Umgebung öffentlich umgesetzt wurde.

---

### 4) Frühe Buck-Converter-RL-Arbeit mit Fokus auf Ausgangsspannung

**Quelle:**  
Repository: `abdalremal/Power-Converter-RL`  
<https://github.com/abdalremal/Power-Converter-RL>

README-Auszug:

> “Reinforcement learning as a control technique for the duty cycle, and therefore output voltage, of a 24:12V buck converter using IGBT's.”

Im sichtbaren MATLAB-Code `Environment_actions_and_observations.m` wird zudem ein RL-Setup mit:

- Beobachtungen: **integrated error, error, voltage**
- **DDPG-Agent**
- Simulink-Umgebung

beschrieben.

**Warum relevant:**  
- Buck-Konverter  
- direkte Verknüpfung von **Duty Cycle** und **Ausgangsspannung**  
- klarer Bezug zur Regelungsaufgabe

**Passung zum Repo:** **hoch**

**Wichtige Unterschiede:**  
- stärker fehlerbasierte Beobachtungsdefinition statt physikalisch motivierter Zustandsgrößen wie \(i_L\) und \(u_C\),  
- damit konzeptionell etwas näher an einer klassischen Tracking-Sicht als an einer physikalisch strukturierten Zustandsbeschreibung.

**Bewertung:**  
Sehr relevante Quelle, weil sie die gleiche Grundregelungsaufgabe adressiert, aber mit einem anderen Zustands-/Beobachtungsdesign.

---

## Teilweise relevante Quellen

### 5) PPO-LSTM für Buck-Boost-Wandler mit CPL

**Quelle:**  
Repository: `KevinKoay/PPO-LSTM-deep-reinforcement-learning-based-controller-for-buck-boost-converter-with-constant-power-l`  
<https://github.com/KevinKoay/PPO-LSTM-deep-reinforcement-learning-based-controller-for-buck-boost-converter-with-constant-power-l>

Im sichtbaren MATLAB-Code `PPO_DRL_Code.m` werden u. a. beschrieben:

- **PPO-Agent**
- **LSTM/RNN-Nutzung**
- diskreter Duty-Cycle-Aktionsraum
- Spannungsreferenz `V_ref`
- Simulink-Environment für einen **buck_boost_model**

**Warum relevant:**  
- sehr ähnliche Methodik: RL regelt direkt den Wandler  
- direkter Bezug zu Duty-Cycle-Entscheidungen  
- gut geeignet als Vergleich für Algorithmuswahl

**Passung zum Repo:** **mittel bis hoch**

**Wichtige Unterschiede:**  
- **Buck-Boost** statt Buck,  
- LSTM-basierter Ansatz,  
- Lastszenario mit CPL.

**Bewertung:**  
Methodisch sehr nützlich, fachlich aber nicht ganz so präzise passend wie die Buck-spezifischen Quellen.

---

### 6) RL für Buck-Konverter im Batterie-Ladefall

**Quelle:**  
Repository: `PVasantharajan/rl-dc-dc-converter-control`  
<https://github.com/PVasantharajan/rl-dc-dc-converter-control>

README-Kernaussagen:

- Buck-Konverter als **averaged model**
- Kombination aus **PID-Regelung + PPO-Residualagent**
- Ziel ist sicheres und effizientes Laden

**Warum relevant:**  
- ebenfalls RL im Umfeld eines Buck-Konverters  
- ebenfalls Regelungsaufgabe im physikalischen System

**Passung zum Repo:** **mittel**

**Wichtige Unterschiede:**  
- kein rein RL-basierter Regler, sondern **hybrider Ansatz**,  
- Anwendungsziel ist Batterieladung statt generische Spannungsregelung des Wandlers.

**Bewertung:**  
Gut als angrenzende Quelle, aber nicht die beste Referenz für das hier verfolgte „reine RL-Policy statt klassischer Regler“-Leitbild.

---

### 7) RL auf echter Hardware / leistungselektronische Systeme

**Quelle:**  
Repository: `Solaire-42/RaspberryPyReinforcementLearningControlPowerElectronicSystems`  
<https://github.com/Solaire-42/RaspberryPyReinforcementLearningControlPowerElectronicSystems>

Öffentliche Repository-Beschreibung:

> “AI based model-free and system-independent control of power electronic systems (Master thesis code)”

In `rl_control_util.py` ist sichtbar:

- Verwendung von **tf-agents / DDPG**
- kontinuierlicher Aktionsraum für den **Duty Cycle**
- hardwarebezogene Systemgrenzen und PWM-/ADC-Anbindung
- Beobachtungsvektor aus **Ausgang, Referenz, Fehler, Aktion**

**Warum relevant:**  
- zeigt, dass RL-Regelung leistungselektronischer Systeme auch **hardware-nah** umgesetzt wurde,  
- bestätigt die Übertragbarkeit von RL-Regelung aus der Simulation in reale Systeme.

**Passung zum Repo:** **mittel**

**Wichtige Unterschiede:**  
- stärker hardware- und implementierungsorientiert,  
- keine klare Fokussierung allein auf das in diesem Repo beschriebene normierte Grundmodell.

**Bewertung:**  
Sehr wertvoll als Ausblick: Das hiesige Repo könnte langfristig in genau so eine Richtung weiterentwickelt werden.

---

### 8) RL für MPPT mit Buck-Konverter

**Quelle:**  
Repository: `SmartSystems-UniAndes/Train_and_Convert_RL_MPPT`  
<https://github.com/SmartSystems-UniAndes/Train_and_Convert_RL_MPPT>

README-Kernaussagen:

- Training von RL-Agenten in MATLAB/Simulink
- Bezug zu **Buck Converter**
- Deployment-Richtung via TensorFlow Lite / Raspberry Pi
- Anwendungsfall: **Maximum Power Point Tracking**

**Warum relevant:**  
- ebenfalls RL + Buck-Konverter  
- ebenfalls leistungselektronischer Regelungskontext

**Passung zum Repo:** **niedrig bis mittel**

**Wichtige Unterschiede:**  
- Zielgröße ist nicht primär klassische Spannungsregelung, sondern **MPPT**.

**Bewertung:**  
Methodisch interessant, aber thematisch deutlich weiter weg als die Buck-Spannungsregler-Quellen.

---

## Gesamtbewertung der Passung

### Was bereits klar umgesetzt wurde

Folgende Kernelemente des Repos sind in der Literatur und in öffentlichen Implementierungen bereits vorhanden:

- RL für **Buck-Konverter**
- direkte Erzeugung des **Duty-Cycle**
- **Spannungsregelung** als Ziel
- MATLAB/Simulink-basierte Trainingsumgebungen
- Untersuchung dynamischer Lastfälle, insbesondere auch anspruchsvoller Lasten

### Was im Repo dennoch sinnvoll und untersuchbar bleibt

Trotzdem ist das hiesige Projekt weiterhin sinnvoll, wenn es sich auf Punkte konzentriert, die in den gefundenen Quellen **nicht systematisch gleichartig aufbereitet** sind:

1. **klarer physikalischer Einstieg** aus dem normierten Tiefsetzsteller-Modell,  
2. **transparenter Vergleich zu klassischer Regelung**,  
3. **schrittweise Eskalation der Schwierigkeit**:
   - konstanter Sollwert
   - Sollwertsprung
   - Rampe
   - Lastsprung
4. **systematischer Vergleich mehrerer RL-Verfahren** unter derselben Modellbasis,  
5. Untersuchung der Frage, ob eine Policy mit Beobachtung \([i_L, u_C]\) bereits genügt oder ob zusätzliche Störinformation \(z\) messbar sein muss.

---

## Einordnung der wissenschaftlichen Nähe

### Sehr nahe am Repo-Thema

- Tianxiao-Yang-Arbeiten zu **Buck + DRL + Duty Ratio**
- KimDaevvon-Reproduktion eines Papers zu **Buck + RL**
- DDPG- und ähnliche MATLAB/Simulink-Repositories für **Buck-Spannungsregelung**

### Verwandt, aber nicht deckungsgleich

- Buck-Boost-Arbeiten
- hybride PID+RL-Ansätze
- MPPT statt Spannungsregelung
- hardwarefokussierte RL-Implementierungen für leistungselektronische Systeme

---

## Schlussfolgerung

Das Konzept dieses Repositories ist **bereits in ähnlicher Form umgesetzt worden**.  
Insbesondere die Kombination

- **Buck-Konverter**
- **Reinforcement Learning**
- **direkte Duty-Cycle-Regelung**
- **Spannungsregelung**

ist durch mehrere öffentliche Quellen bereits abgedeckt.

Die Recherche spricht daher gegen eine Einordnung als völlig neue Idee, aber klar **für** eine sinnvolle Weiterarbeit an diesem Repo, wenn der Fokus auf einer der folgenden Leistungen liegt:

- saubere wissenschaftliche Reproduktion,
- systematischer Benchmark verschiedener RL-Verfahren,
- didaktisch gute Dokumentation,
- oder robuste Erweiterung auf Störungen, Lastsprünge und realitätsnähere Randbedingungen.

---

## Quellenliste

1. `tianxiaoy9/Data-driven-deep-reinforcement-learning-controller-for-DC-DC-buck-converter-feeding-CPLs`  
   <https://github.com/tianxiaoy9/Data-driven-deep-reinforcement-learning-controller-for-DC-DC-buck-converter-feeding-CPLs>
2. IEEE-Link aus obigem Repository:  
   <https://ieeexplore.ieee.org/abstract/document/9521987>
3. IEEE-Link aus obigem Repository:  
   <https://ieeexplore.ieee.org/abstract/document/9841427>
4. Taylor & Francis-Link aus obigem Repository:  
   <https://www.tandfonline.com/doi/full/10.1080/23307706.2023.2201587>
5. `KimDaevvon/RL_Buck_Converter`  
   <https://github.com/KimDaevvon/RL_Buck_Converter>
6. `pabloajimenezc/DDPG-DC-DC-Converter`  
   <https://github.com/pabloajimenezc/DDPG-DC-DC-Converter>
7. `abdalremal/Power-Converter-RL`  
   <https://github.com/abdalremal/Power-Converter-RL>
8. `KevinKoay/PPO-LSTM-deep-reinforcement-learning-based-controller-for-buck-boost-converter-with-constant-power-l`  
   <https://github.com/KevinKoay/PPO-LSTM-deep-reinforcement-learning-based-controller-for-buck-boost-converter-with-constant-power-l>
9. `PVasantharajan/rl-dc-dc-converter-control`  
   <https://github.com/PVasantharajan/rl-dc-dc-converter-control>
10. `Solaire-42/RaspberryPyReinforcementLearningControlPowerElectronicSystems`  
    <https://github.com/Solaire-42/RaspberryPyReinforcementLearningControlPowerElectronicSystems>
11. `SmartSystems-UniAndes/Train_and_Convert_RL_MPPT`  
    <https://github.com/SmartSystems-UniAndes/Train_and_Convert_RL_MPPT>
