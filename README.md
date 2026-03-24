markdown# USB-C Audio Interface — Desktop / Streaming / Meetings

**Status: PCB-Design abgeschlossen — unbestückt**  
**Tool:** KiCad | **Layer:** 4-Layer | **Hersteller-ready:** Ja

---

## Projektbeschreibung

Kompaktes USB-C Audio-Interface für Desktop, Streaming und Meetings.
Wird am PC/Mac/Linux als Standard-USB-Audio-Device (UAC2) erkannt,
ohne Treiber. Entwickelt als reproduzierbarer Prototyp mit sauberem
Mixed-Signal-Layout (Analog + Digital).

**Besonderheiten:**
- USB Audio Class 2 (UAC2) — Plug & Play, treiberlos
- Stereo Kopfhörerverstärker mit I²C-Lautstärkeregelung (DirectPath)
- Elektret-Mikrofon-Bias + Hardware-Mute
- Rotary Encoder für Lautstärke + Mute
- Getrennte Digital/Analog-Versorgung (Buck → 3V3D → LDO → 3V3A)
- ESD-Schutz USB + Audio
- Testpunkte für alle kritischen Rails und Signale

---

## Hardware

| Komponente | Beschreibung |
|---|---|
| USB Audio Codec | PCM2912APJTR (ADC + DAC, USB-Enumeration integriert) |
| Kopfhörerverstärker | TPA6130A2RTJR (Stereo, I²C Volume, DirectPath/Capless) |
| Steuer-MCU | ATtiny1616 (Encoder, I²C, Button Handling) |
| Buck Converter | TPS62150A (5V → 3.3V Digital) |
| Analog LDO | TPS7A2033PDBVR (3.3V Digital → 3.3V Analog, Low-Noise) |
| ESD-Schutz | TPD4E05U06DQAR (USB, Audio, GPIO) |
| Stackup | 4-Layer (Signal / GND-Plane / Power / Signal+Pour) |
| Tool | KiCad |

---

## Anschlüsse

- USB-C  — Daten + Versorgung (Bus-Powered)
- TRRS 3.5mm Klinke CTIA (Headset: Mic + L/R + GND)
- Rotary Encoder (Lautstärke + Mute)
- LEDs: Power, Mic-Mute, Clip/Status
- I²C Header (OLED / Erweiterung)
- GPIO Header
- UPDI Header (ATtiny Programmierung)

---

## Architektur

**Versorgung:**
USB 5V → Buck (TPS62150A) → 3V3 Digital → LDO (TPS7A2033) → 3V3 Analog

**Signalführung:**
- USB D+/D− als Differential Pair
- Audio-Pfade kurz, getrennt von Digital
- Keine GND-Splits — gemeinsame GND-Plane (L2 durchgehend)

**Testpunkte:** 5V, 3V3D, 3V3A, GND, USB D+/D−, Audio-Nodes

---

## Ausschlüsse

Kein Serienprodukt — kein CE/EMV, keine Normenfreigabe,
keine sicherheitskritischen Funktionen.

---

## Dateien in diesem Repository

- `/kicad/` — KiCad Projektdateien
- `/screenshots/` — PCB- und Schematic-Ansichten

---

> Entwickelt von [Shawn Schneider](https://tracelabs-pcb.de)  
> — PCB-Design & Lötservice, Wolfsburg
