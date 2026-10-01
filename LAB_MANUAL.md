# Analog Electronic Systems (AES) Lab Manual

> **Course:** Analog Electronic Systems Lab  
> **Institution:** Indian Institute of Technology Madras (IIT Madras)  
> **Official Document:** [`BS_Analog_Systems_Lab_Manual.pdf`](BS_Analog_Systems_Lab_Manual.pdf)  
> **Demonstrations:** [YouTube Channel: @arpit_iit.madras](https://youtube.com/@arpit_iit.madras?si=c5lhNswLiiwFaNUQ)

---

## 📌 Overview of Lab Experiments

### Objective
Design a complete analog electronic system for processing audio/biomedical signals and driving an 8Ω/32Ω speaker.

### System Architecture
```
                  ┌─────────────────┐
               ┌─►│ Bandpass Filter │─┐
               │  │  (156.25 Hz)    │ │
Audio Signal   │  └─────────────────┘ ▼
 (or Heart/ ───┤                     ( + ) ──► Class-D Audio ──► Speaker
 Lung Sound)   │  ┌─────────────────┐ ▲          Amplifier        (32Ω)
               └─►│ Bandpass Filter │─┘
                  │    (625 Hz)     │
                  └─────────────────┘
```

### Learning Outcomes
At the end of this lab series, students understand the following concepts with real-world applications:
* Feedback theory & loop stability
* Open and closed loop operational amplifier systems
* Opamp-RC Integrator
* Schmitt Trigger and Relaxation Oscillator
* Active-RC Filters (Second-order Bandpass)
* Summing Amplifier (Adder)
* Class-D Audio Power Amplifier (PWM Modulator + Discrete BJT H-Bridge)

### Brief Description
Typically, heart beat and lung sounds are used as inputs and processed in an electronic stethoscope module. This lab aims to realize the electronic system for the stethoscope. However, alternate audio signals such as fixed frequency tones from a function generator or audio source are used as test inputs. We realize each module in separate experiments and finally integrate all blocks into a full working system.

---

## 📋 List of Experiments

1. [Experiment 1: Ramp Generator](#experiment-1-ramp-generator)
2. [Experiment 2: Single Ended-to-Differential Input Converter and PWM Modulator](#experiment-2-single-ended-to-differential-input-converter-and-pwm-modulator)
3. [Experiment 3: H-Bridge Driver and Integration](#experiment-3-h-bridge-driver-and-integration)
4. [Experiment 4: Bandpass Filter](#experiment-4-bandpass-filter)
5. [Experiment 5: Adder](#experiment-5-adder)
6. [Experiment 6: Top Level Integration](#experiment-6-top-level-integration)

---

## Experiment 1: Ramp Generator

### Theory & Operation
The ramp or triangle wave generator is an oscillator implemented using an opamp-RC integrator stage followed by a Schmitt trigger comparator.

* **Peak-to-Peak Ramp Amplitude ($V_M$):**
  $$V_M = 2 \left( \frac{R_2}{R_3} \right) V_{CM}$$

* **Oscillation Frequency ($F_{SW}$):**
  $$F_{SW} = \frac{1}{T_{SW}} = \frac{R_3}{4 R_2 R_1 C_1}$$

### Specifications
* Supply Voltage ($V_{DD}$): $5\text{ V}$
* Common Mode Voltage ($V_{CM}$): $V_{DD}/2 = 2.5\text{ V}$
* Oscillation Frequency ($F_{SW}$): $5\text{ kHz}$
* Peak-to-Peak Ramp Amplitude ($V_M$): $1\text{ V}$

### List of Components
* **OPA1:** MCP6004 Quad Op-Amp
* **CMP1:** LM339 Comparator (Open-collector; requires a $4.7\text{ k}\Omega$ pullup resistor between $V_{DD}$ and $V_{OUT}$)
* **Resistors:** $R_1 = 25\text{ k}\Omega$, $R_2 = 45\text{ k}\Omega$, $R_3 = 200\text{ k}\Omega$, Pullup $= 4.7\text{ k}\Omega$
* **Capacitor:** $C_1 = 10\text{ nF}$

### Pre-Lab Exercises
1. Derive expressions for ramp amplitude ($V_M$) and oscillation frequency ($F_{SW}$).
2. Simulate the ramp generator in LTspice (`Week-01_Ramp_Generator/Analog1.asc`) and observe the effect of variations in $R_1, R_2, R_3, C_1$.
3. Plot waveforms ($V_{RAMP}$ and $V_{SQR}$) and measure amplitude and frequency.

### Measurements
1. Set $V_{DD} = 5\text{ V}$, $V_{CM} = 2.5\text{ V}$.
2. Capture integrator output ($V_{RAMP}$) and Schmitt trigger output ($V_{SQR}$).
3. Measure and record frequency and peak-to-peak amplitude.

#### Hardware Measurement Waveforms
<p align="center">
  <img src="assets/images/week1_ramp_square_alice_scope.jpg" alt="Ramp and Square Wave Measurements" width="750"/>
  <br>
  <em>Measured ALICE Desktop oscilloscope output: Triangle Ramp (CB-V green, 1 Vpp @ 5 kHz) and Schmitt Trigger square wave (CA-V orange, 0 to 4.5 V).</em>
</p>

---

## Experiment 2: Single Ended-to-Differential Input Converter and PWM Modulator

### Theory & Operation
Converts a single-ended audio input signal into differential signals ($V_{in\_a+}$ and $V_{in\_a-}$, 180° out of phase) and modulates them against the triangular ramp carrier using dual comparators to produce complementary PWM signals ($V_{PWM\_P}$ and $V_{PWM\_N}$).

For $R_1 = R_2$:
$$V_{in\_a+} = V_{in\_a(ac)} + V_{CM}$$
$$V_{in\_a-} = -V_{in\_a(ac)} + V_{CM}$$

### Specifications
* Supply Voltage: $V_{DD} = 5\text{ V}$, $V_{CM} = 2.5\text{ V}$
* PWM Carrier Frequency: $5\text{ kHz}$
* Input Audio Signal: Sinusoid at $312.5\text{ Hz}$ (amplitude matched to ramp carrier)

### List of Components
* **CMP1, CMP2:** LM339 (Open-collector with pull-up resistors)
* **Inverters:** MC14069 / CD4069
* **Coupling Capacitor:** $C_{in} = 10\ \mu\text{F}$
* **Resistors:** $10\text{ k}\Omega$ matched pair, $4.7\text{ k}\Omega$ pullups

### Pre-Lab Exercises
1. Derive expressions for $V_{in+}$ and $V_{in-}$ and prove they have equal amplitude but opposite polarity.
2. Find the expression for differential PWM $(V_{PWM\_P} - V_{PWM\_N})$ and prove the average output is an amplified version of the input.
3. Build and simulate the complete circuit in LTspice (`Week-02_Differential_PWM/Analog1,2.asc`).

### Measurements
1. Verify $V_{in+}$ and $V_{in-}$ are 180° out of phase.
2. Capture duty cycles of $V_{PWM\_P}$ and $V_{PWM\_N}$; verify $D_N = 1 - D_P$.
3. Filter PWM outputs with an RC filter ($f_c \approx 1\text{--}2\text{ kHz}$) to reconstruct and verify the demodulated audio sinusoid.

#### Hardware Implementation & Probing
| Annotated IC Layout & Pin Routing | Hardware Verification with DMM & ALICE |
|:---:|:---:|
| <img src="assets/images/week2_pwm_breadboard_annotated_layout.jpg" width="360"/> | <img src="assets/images/week2_pwm_multimeter_alice_measurement.jpg" width="360"/> |
| *Breadboard IC placement: MCP6004 and LM339 comparator rail routing.* | *Live measurement of differential PWM outputs and RMS AC voltage.* |

---

## Experiment 3: H-Bridge Driver and Integration

### Theory & Operation
The H-bridge power stage provides high-efficiency power delivery to drive speaker loads. It consists of two complementary half-bridge drivers (2N2222 NPN + 2N2907 PNP) driven through non-overlapping clock generation logic (or inverter buffers) to eliminate shoot-through cross-conduction current.

* **Speaker Model:** Series combination of coil resistance $R_L$ ($32\,\Omega$) and coil inductance $L$ ($100\ \mu\text{H}$ to $1\text{ mH}$).

### Specifications
* Supply Voltage: $V_{DD} = 5\text{ V}$
* PWM Frequency: $5\text{ kHz}$
* Load Resistance: $R_L = 32\,\Omega$ (tested with resistive load first, then physical speaker)

### Pre-Lab Exercises
1. Build the complete Class-D circuit in LTspice (`Week-03_H-Bridge_Driver/Analog3.asc`).
2. Simulate with the speaker load model and plot inductor current.

### Measurements
1. Measure duty cycle and waveform symmetry at $V_{OUT\_P}$ and $V_{OUT\_N}$.
2. Verify audio reconstruction via passive low-pass filtering.
3. Conduct acoustic hearing tests across frequencies from $156.25\text{ Hz}$ to $1.25\text{ kHz}$.

#### Hardware Implementation
<p align="center">
  <img src="assets/images/week3_hbridge_driver_circuit.jpg" alt="Discrete BJT H-Bridge Stage" width="600"/>
  <br>
  <em>Discrete complementary BJT H-Bridge power output stage (2N2222 NPN + 2N2907 PNP) with bulk supply bypass capacitors.</em>
</p>

---

## Experiment 4: Bandpass Filter

### Theory & Operation
Two active second-order multiple-feedback bandpass filters isolate desired tone frequencies while rejecting out-of-band harmonics and noise:
$$H(s) = \frac{A_0 \left(\frac{\omega_0}{Q}\right) s}{s^2 + \left(\frac{\omega_0}{Q}\right) s + \omega_0^2}$$

### Specifications
* Supply Voltage: $V_{DD} = 5\text{ V}$, $V_{CM} = 2.5\text{ V}$
* Center Frequencies:
  * **BPF 1:** $f_{o1} = 156.25\text{ Hz}$
  * **BPF 2:** $f_{o2} = 625\text{ Hz}$
* Quality Factor: $Q_{o1} = Q_{o2} = 10$
* Midband Gain: $A_{o1} = A_{o2} = 1\ (0\text{ dB})$

### Pre-Lab Exercises
1. Derive the second-order bandpass transfer function $H(s)$.
2. Calculate resistor and capacitor values ($R_{1a}, R_{2a}, R_{3a}, C_a$ and $R_{1b}, R_{2b}, R_{3b}, C_b$).
3. Simulate AC frequency sweep and transient response in LTspice (`Week-04_Bandpass_Filter/Analog4,5.asc`).

### Measurements
1. Apply audio sinusoid ($0.9 \times V_M$) at $156.25\text{ Hz}$ and $625\text{ Hz}$; verify maximum response at respective center frequencies.
2. Perform frequency sweep from $100\text{ Hz}$ to $1.25\text{ kHz}$ to confirm out-of-band attenuation.

#### Hardware Implementation
<p align="center">
  <img src="assets/images/week4_bandpass_filter_breadboard.jpg" alt="Active Bandpass Filter Breadboard" width="600"/>
  <br>
  <em>Second-order active RC bandpass filter circuits with MCP6004 and precision film capacitors.</em>
</p>

---

## Experiment 5: Adder Circuit

### Theory & Operation
An active summing amplifier combines the filtered outputs ($V_{out\_bpf1}$ and $V_{out\_bpf2}$) from Experiment 4 before feeding them into the Class-D power amplifier stage.
$$V_{out\_adder} = (V_{in1} + V_{in2}) \quad \text{referenced around } V_{CM}$$

### Specifications
* Input amplitude: Maximum $0.9 \times V_M$
* Op-Amp: MCP6004 Quad Op-Amp
* Single-supply: $V_{DD} = 5\text{ V}$, $V_{CM} = 2.5\text{ V}$

### Pre-Lab Exercises
1. Calculate equal feedback and input resistor values ($R$).
2. Simulate the adder in LTspice (`Week-05_Adder_Circuit/Analog5.asc`).

### Measurements
1. Apply test tones and verify linear addition without saturation clipping.
2. Connect BPF-1 and BPF-2 outputs to adder inputs and sweep frequency from $100\text{ Hz}$ to $1\text{ kHz}$.

#### Hardware Implementation
<p align="center">
  <img src="assets/images/week5_adder_circuit_probing.jpg" alt="Active Adder Circuit Probing" width="600"/>
  <br>
  <em>Active summing mixer stage under node probing with multimeter and oscilloscope clips.</em>
</p>

---

## Experiment 6: Top Level Integration

### Integration Architecture
Top-level integration interconnects all modules into a complete analog stethoscope / audio amplification system:

```
[Audio Input] ──► [Bandpass Filters (Exp 4)]
                         │
                         ▼
                  [Adder (Exp 5)]
                         │
                         ▼
        [Class-D Modulator & H-Bridge (Exp 2, 3)] ◄── [Ramp Generator (Exp 1)]
                         │
                         ▼
                   [Speaker (32Ω)]
```

<p align="center">
  <img src="assets/images/system_integration_adalm1000_speaker.jpg" alt="Complete Top Level System Setup" width="800"/>
  <br>
  <em>Complete top-level system integrated on dual breadboards, driven by ADALM1000 module and connected to 32Ω dynamic speaker.</em>
</p>

### Critical Integration Guidelines
1. **Module-by-Module Verification:** Ensure each individual module is verified in LTspice and hardware before interconnecting.
2. **Star Grounding & Power Isolation:**
   * Connect $V_{DD}$ and GND ($V_{SS}$) of each block directly to the power supply (star topology) rather than daisy-chaining on breadboard rails.
   * Prevents high-current switching noise from the H-bridge and PWM stage from coupling into sensitive analog filters and ramp generator.
3. **Decoupling Capacitors:** Place $0.1\ \mu\text{F}$ ceramic and $10\ \mu\text{F}$ electrolytic decoupling capacitors close to the $V_{DD}$ and $V_{SS}$ pins of every IC.
4. **Current Limiting:** Set bench power supply current limit to $1.5\times$ normal operating current prior to turning power ON to safeguard against accidental shorts.
5. **Color Coding & Labeling:**
   * Red = $V_{DD}$ ($+5\text{ V}$)
   * Black = GND ($0\text{ V}$)
   * Green = $V_{CM}$ ($+2.5\text{ V}$)
   * Yellow/Blue/White = Signal lines brought out with test tape tags for oscilloscope probing.

---

## 📺 Video Demonstrations

All experiments, bench setups, and hardware execution runs are showcased on YouTube:  
👉 **[YouTube Channel: @arpit_iit.madras](https://youtube.com/@arpit_iit.madras?si=c5lhNswLiiwFaNUQ)**
