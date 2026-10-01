# Analog Electronics Experiments & Systems Design

[![YouTube Channel](https://img.shields.io/badge/YouTube-@arpit__iit.madras-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://youtube.com/@arpit_iit.madras?si=c5lhNswLiiwFaNUQ)
[![IIT Madras](https://img.shields.io/badge/Institution-IIT%20Madras-002147?style=for-the-badge&logo=academia)](https://www.iitm.ac.in)
[![Simulation](https://img.shields.io/badge/EDA-LTspice-blue?style=for-the-badge)](https://www.analog.com/en/resources/design-tools-and-calculators/ltspice-simulator.html)
[![Hardware](https://img.shields.io/badge/Hardware-ADALM1000-orange?style=for-the-badge)](https://www.analog.com/en/resources/evaluation-hardware-and-software/evaluation-boards-kits/ADALM1000.html)

This repository contains the complete laboratory experiments, circuit schematics, simulation models, and design reports for the **Analog Electronic Systems (AES) Lab** at **IIT Madras**, authored by **Arpit Katiyar**.

---

## 📺 Video Demonstrations

All practical circuit breadboard implementations, waveform measurements, and hardware testing runs are recorded and uploaded on YouTube:

> 🔗 **Watch all experiment demonstration videos here:**  
> **[YouTube: @arpit_iit.madras](https://youtube.com/@arpit_iit.madras?si=c5lhNswLiiwFaNUQ)**

---

## 📑 Repository Structure

```text
.
├── README.md
├── .gitignore
├── LICENSE
├── Week-01_Ramp_Generator/
│   ├── Analog1.asc                   # LTspice schematic (Ramp Generator)
│   ├── Analog1.log                   # LTspice simulation log
│   ├── LM339.New.asy                 # Custom symbol for LM339 comparator
│   └── Analog_Lab_Week_1_Report.docx # Lab report with derivations & results
├── Week-02_Differential_PWM/
│   ├── Analog1,2.asc                 # LTspice schematic (Single-to-Diff & PWM)
│   ├── Analog1,2.log                 # Simulation log
│   ├── LM339.asy                     # Comparator symbol file
│   └── Analog_Lab_Week_2_Report.docx # Complete laboratory documentation
├── Week-03_H-Bridge_Driver/
│   ├── Analog3.asc                   # LTspice schematic (H-Bridge Class-D stage)
│   └── Analog_Lab_Week_3_Report.pdf  # Comprehensive Lab Report
├── Week-04_Bandpass_Filter/
│   ├── Analog4,5.asc                 # LTspice schematic (Active Bandpass Filter)
│   └── Analog_Lab_Week_4_Report.pdf  # Lab Report & Frequency Analysis
├── Week-05_Adder_Circuit/
│   ├── Analog5.asc                   # LTspice schematic (Active Adder / Mixer)
│   ├── Analog5.net                   # SPICE netlist
│   └── Analog_Lab_Week_5_Report.pdf  # Final Lab Report
└── Design-Projects_Amplifiers/
    ├── Trans-Impedence Amplifier.pdf # Precision TIA design & stability report
    └── Voltage Amplifier.pdf         # 0-1V to 0-50V High-Voltage Amplifier report
```

---

## 🔬 Experiment Overview

### [Week 1: Ramp Wave Generator](Week-01_Ramp_Generator/)
* **Objective:** Design and implement a relaxation-oscillator ramp wave generator using an operational amplifier integrator stage and an LM339 Schmitt trigger comparator.
* **Key Components:** MCP6004 Quad Op-Amp, LM339 Comparator, timing resistor/capacitor network ($R_1 = 25\text{ k}\Omega$, $R_2 = 45\text{ k}\Omega$, $R_3 = 200\text{ k}\Omega$, $C = 10\text{ nF}$, pull-up $4.7\text{ k}\Omega$).
* **Hardware Setup:** Single-supply operation ($V_{DD} = 5\text{ V}$, $V_{CM} = 2.5\text{ V}$) tested using the ADALM1000 Active Learning Module.
* **Video Demonstration:** [Experiment 1: Ramp Generator](https://youtube.com/@arpit_iit.madras?si=c5lhNswLiiwFaNUQ)

---

### [Week 2: Single-Ended to Differential Input Converter & PWM Modulator](Week-02_Differential_PWM/)
* **Objective:** Convert a single-ended analog audio/test signal into balanced differential signals ($V_{in+}$ and $V_{in-}$, 180° out of phase) and compare them with the ramp carrier to produce differential pulse-width modulated (PWM) switching signals (`PWM_P` and `PWM_N`).
* **Key Components:** MCP6004 Op-Amp, dual LM339 comparators, RC demodulation/low-pass filters.
* **Validation:** Verified both on LTspice transient analysis and on breadboard hardware using ALICE desktop oscilloscope tools.
* **Video Demonstration:** [Experiment 2: Single Ended-to-Differential Converter and PWM Modulator](https://youtube.com/@arpit_iit.madras?si=c5lhNswLiiwFaNUQ)

---

### [Week 3: H-Bridge Driver and Class-D Integration](Week-03_H-Bridge_Driver/)
* **Objective:** Build a discrete BJT H-Bridge power output stage driven by differential PWM signals to efficiently drive low-impedance inductive/resistive loads (speakers).
* **Key Components:** 2N2222 (NPN) and 2N2907 (PNP) BJTs, base drive networks, $16\,\Omega$ load resistor, coupling/filter capacitors.
* **Video Demonstration:** [Experiment 3: H-Bridge Driver and Integration](https://youtube.com/@arpit_iit.madras?si=c5lhNswLiiwFaNUQ)

---

### [Week 4: Active Bandpass Filter](Week-04_Bandpass_Filter/)
* **Objective:** Design, simulate, and physically implement an active bandpass filter circuit to isolate specific signal bandwidths while suppressing out-of-band harmonics and noise.
* **Analysis:** AC frequency sweep (Bode plot), resonant frequency calculation, Q-factor, and gain characterization.
* **Video Demonstration:** [Experiment 4: Bandpass Filter](https://youtube.com/@arpit_iit.madras?si=c5lhNswLiiwFaNUQ)

---

### [Week 5: Active Adder / Audio Mixer Circuit](Week-05_Adder_Circuit/)
* **Objective:** Design an active inverting/non-inverting summing amplifier to combine multiple audio channels with minimal cross-talk and uniform gain response.
* **Analysis:** AC, transient, and operating-point DC sweep simulations; physical circuit verification on breadboard.
* **Video Demonstration:** [Experiment 5: Adder Circuit](https://youtube.com/@arpit_iit.madras?si=c5lhNswLiiwFaNUQ)

---

## ⚡ Advanced Amplifier Design Projects

Located in the [`Design-Projects_Amplifiers/`](Design-Projects_Amplifiers/) directory:

1. **Transimpedance Amplifier (TIA) for Photodiode Front-Ends:**
   * Design of transimpedance feedback network ($R_f = 1\text{ k}\Omega$ to $50\text{ k}\Omega$, $C_f$).
   * AC stability analysis ensuring phase margin $\ge 60^\circ$ across photodiode junction capacitance ($2\text{--}10\text{ pF}$).
   * Input-referred current noise analysis and transient step response comparison between LTC6268 and UniversalOpAmp2.

2. **High-Voltage Actuator Driver ($0\text{--}1\text{ V} \to 0\text{--}50\text{ V}$):**
   * Non-inverting high-voltage amplifier design with gain $A_v \approx 50\times$.
   * Capacitive load handling ($10\text{--}200\text{ nF}$) modeling piezoelectric (PZT) transducers.
   * Closed-loop stability, step response, output noise spectrum, and supply rail constraints using LTC6090.

---

## 🛠️ Tools & Technologies

| Category | Tools / Components |
|---|---|
| **Simulation** | LTspice XVII / 24 |
| **Hardware Instrument** | Analog Devices ADALM1000 (Active Learning Module) |
| **Measurement Software**| ALICE Desktop, Pixelpulse |
| **Active ICs** | MCP6004 (Quad Rail-to-Rail Op-Amp), LM339 (Quad Comparator), LTC6090, LTC6268 |
| **Discrete Semis** | 2N2222 (NPN), 2N2907 (PNP) |
| **Documentation** | LaTeX, Microsoft Word, PDF Reports |

---

## 🚀 How to Run the Simulations

1. Download and install [LTspice](https://www.analog.com/en/resources/design-tools-and-calculators/ltspice-simulator.html).
2. Clone this repository:
   ```bash
   git clone https://github.com/123Arp/Analog-Electronics-Experiments.git
   cd Analog-Electronics-Experiments
   ```
3. Open any `.asc` file in LTspice (e.g. `Week-01_Ramp_Generator/Analog1.asc`).
   * *Note: Keep custom symbol files (such as `LM339.New.asy` or `LM339.asy`) in the same directory as the schematic so LTspice resolves component models automatically.*
4. Click the **Run** button (running man icon) in LTspice to view simulated waveforms.

---

## 👤 Author

* **Arpit Katiyar**
* Indian Institute of Technology Madras (IIT Madras)
* 📺 YouTube: [@arpit_iit.madras](https://youtube.com/@arpit_iit.madras?si=c5lhNswLiiwFaNUQ)
* 🐙 GitHub: [@123Arp](https://github.com/123Arp)

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).