# synapsVCO 🎛️⚡

**synapsVCO** ist ein kompakter, leistungsstarker und professioneller Eurorack-Wavetable-VCO (Voltage Controlled Oscillator) auf Basis des **ATmega328P** Mikrocontrollers. Entwickelt für performative Live-Einsätze, kombiniert das Modul eine rauscharme analoge Signalverarbeitung mit mächtigen digitalen Klangformungsmöglichkeiten auf ultra-kompakten **6 TE** (30,48 mm).

## 🔬 Hauptmerkmale & Features

* **High-Performance Audio Path:**
  * Dual 12-Bit DAC (**MCP4922**) für hochauflösende Audiosignale.
  * Symmetrische Pufferung und Rekonstruktionsfilterung über Quad Op-Amp (**TL074**).

* **Killer Performance-Features:**
  * **Hard-Sync (`SYNC_IN`):** Triggert sofortigen Phasen-Reset an Interrupt-Pin `PD0` für aggressive Lead-Sounds und Sync-Sweeps.
  * **Morph-CV (`MORPH_CV`):** Gepufferter CV-Modulationseingang (über TL074 auf ADC `PC3`) zur dynamischen Modulation von Wavetables, Wave-Folding oder Pulsweite.
  * **Hardware Sub-Oszillator (`SUB_OUT`):** Dezidierter Auskopplungspfad (1 Oktave tiefer) über ATmega-Digitalpin `PD6` mit DC-Blocker für solides Bass-Fundament.

* **Audio- & Kontroll-Schnittstellen:**
  * **1V/Oct Pitch CV (`CV_IN`):** Impedanzgewandelter Eingangs-Pfad mit Zener-Diodenschutz.
  * **Gate In (`GATE_IN`) & Clock In (`CLOCK_IN`):** Dedizierte Digital-Eingänge für rhythmische Noten- und Takt-Trigger.
  * **Stereo/Dual Audio-Out (`AudioOut_L` / `AudioOut_R`).**

* **Robuste Stromversorgung & Protection:**
  * Bipolare $\pm 12\text{V}$ Eurorack-Versorgung.
  * Schutz vor Verpolung durch Schottky-Dioden (`MBRA140T3G`) und rückstellende Polyfuses (`250mA`).
  * Rauschfreie $\pm 12\text{VA}$ Analogschienen durch LC-Filterung (Ferrite Beads `120R@100MHz` + Entkopplungskondensatoren).
  * Effizienter Onboard 5V DC/DC-Schaltregler (`TPS54302`).

## 📏 Formfaktor & Layout

* **Breite:** 6 TE (30,48 mm)
* **Höhe:** Standard Eurorack 3U (128,5 mm Frontplatte / ~108,5 mm Platine)
* **Bauteil-Spezifikation:** Durchgängig **0603 SMD-Komponenten** (resistors/caps) für optimale Packungsdichte bei hervorragender manueller Lötbarkeit.

## 🛠️ Hardware-Architektur & Belegung

### Pin-Mapping (ATmega328P-AU TQFP-32)

| Pin | Symbol / Net | Funktion / Beschreibung |
| :--- | :--- | :--- |
| **Pin 30** | `PD0` | **Hard-Sync Input** (External Interrupt) |
| **Pin 32** | `PD2` | **Gate Input** |
| **Pin 1** | `PD3` | **Clock Input** |
| **Pin 10** | `PD6` | **Sub-Oszillator Output** |
| **Pin 25** | `PC2 / ADC2` | **1V/Oct CV Input** |
| **Pin 26** | `PC3 / ADC3` | **Morph-CV Input** |
| **Pin 23 / 24** | `PC0 / PC1` | **Potentiometer 1 & 2** (Parametertrimmer) |
| **Pin 14–17** | `PB2–PB5` | **SPI Interface** (MCP4922 DAC Steuerung) |
| **Pin 7 / 8** | `XTAL1 / XTAL2` | **16 MHz Quarz-Taktgeber** |

## 📋 Bauteilübersicht (BOM Kurzfassung)

* **Microcontroller:** ATmega328P-AU (TQFP-32)
* **DAC:** MCP4922-E/SL (SOIC-14)
* **Op-Amp:** TL074CDR (SOIC-14)
* **Power Regulator:** TPS54302 (SOT-23-6)
* **Dioden:** MBRA140T3G (SMA), B340A (SMA), 5.1V Zener (SOD-123)
* **Buchsen:** 3.5mm PJ301M-12 (THT)
* **Potentiometer:** Alpha RK09K Serie (THT)

## ⚡ Inbetriebnahme & Flashen

1. **Power-Check:** Vor dem Einsetzen von ICs oder der Firmware-Programmierung sicherstellen, dass an den Power-Rails des TL074 $+12\text{V}$ (Pin 4) und $-12\text{V}$ (Pin 11) anliegen sowie die Mikrocontroller-Schiene exakt $+5\text{V}$ aufweist.
2. **ISP-Programming:** Das Modul verfügt über einen Standard **2x3-Pin ISP Header** (`J2`).
3. **Fuses setzen:** Für den externen 16 MHz Quarz (`Y2`):
   * High Fuse: `0xD9`
   * Low Fuse: `0xFF`
   * Extended Fuse: `0xFD`

## 📄 Lizenz

Dieses Projekt ist Open-Source-Hardware unter der **CERN-OHL-P (Permissive)** Lizenz.