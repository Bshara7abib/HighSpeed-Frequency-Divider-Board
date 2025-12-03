# High-Speed Clock Divider PCB

This repository contains the design and implementation of a **high-speed digital frequency divider (clock divider)** board, developed as the final project in the *Board Design* course in the Department of Electrical & Electronics Engineering.

The goal of the project is to design and build a **robust, low-noise frequency divider** that can reliably divide a **high-frequency clock (above 30 MHz, tested around 60 MHz)** down to lower frequencies, while dealing with real-world issues such as **signal integrity, crosstalk and PCB layout for high-speed digital signals**.

---

## 📡 Project Overview

Many digital systems require dividing a fast clock in order to generate slower clocks or detect when a certain number of pulses has occurred. Doing this reliably at tens of MHz with standard logic ICs is not trivial: wiring, parasitic capacitances and PCB layout can introduce **noise, glitches and timing errors**.

In this project we:

- Designed a **frequency divider** based on **74LS74 D-type flip-flops** and a **74LS90 counter**.  
- Prototyped and tested the circuit using **wire-wrap** and a **~60 MHz crystal oscillator** (SG-8002JC).  
- Measured significant **crosstalk-induced noise** at the counter output on the first prototype.  
- Applied step-by-step **noise-mitigation techniques** (decoupling capacitors, shorter wiring, pull-down resistors) and reduced the noise from tens of millivolts to only a few millivolts.  
- Migrated the improved solution to a **two-layer PCB designed in KiCad**, including a solid **ground plane** and layout suitable for high-frequency operation.

The result is a compact, manufacturable board that demonstrates **stable, low-noise frequency division at high input frequencies**.

---

## ⚙️ Functional Description

At a high level, the board performs the following:

1. Receives a **high-frequency clock input** from a crystal oscillator module (around 60 MHz).  
2. Uses a chain of **74LS74 D flip-flops** together with a **74LS90 counter** to divide the input clock by a chosen factor (for example, by 2, 4, 10, etc.), achieving an output frequency of approximately **15 MHz** in the final design.  
3. Stabilizes supply and signal lines using:
   - **Three 10 nF decoupling capacitors** placed near the ICs.  
   - **Four 10 kΩ pull-down resistors** on sensitive inputs to avoid undefined logic levels.

The design focuses on a solution that is **simple, reliable and easy to reproduce** with standard TTL logic components.

---

## 🧪 Design & Development Flow

### 1. Simulation and Concept Validation

- The digital logic was first designed and verified using **schematic-level simulation tools** (Logisim and KiCad’s schematic editor).  
- Simulations were used to validate:
  - Correct division ratios in the flip-flop chain and counter.  
  - Timing relationships between the divided clock signals.

### 2. Wire-Wrap Prototype and Noise Investigation

- The first hardware prototype was built using **wire-wrap** on a prototyping board.  
- A ~60 MHz clock was applied and the outputs were observed with an **oscilloscope**.  
- The prototype worked functionally, but measurements revealed:
  - Distorted waveforms at some flip-flop outputs due to parasitics.  
  - Noticeable **crosstalk and noise spikes** at the counter output, on the order of tens of millivolts.

### 3. Noise Mitigation Steps

To improve signal quality, three incremental hardware changes were made and measured:

1. **Decoupling capacitors**  
   - Added capacitors between VCC and GND near the flip-flops and counter.  
   - Reduced high-frequency noise and supply ringing.

2. **Shorter and cleaner wiring**  
   - Re-routed the wire-wrap prototype with shorter connections, especially for high-speed lines.  
   - Further reduced coupling between signals.

3. **Pull-down resistors**  
   - Added pull-down resistors to stabilize floating inputs and prevent spurious switching.  
   - Final measurements showed clean, stable square waves with residual noise of only a few millivolts at the divided clock output.

These steps clearly demonstrated how **good hardware practices** can dramatically improve signal integrity in high-speed digital circuits.

### 4. PCB Design in KiCad

After optimizing the prototype, the circuit was transferred to a **two-layer PCB**:

- **Component placement**
  - The crystal oscillator, flip-flops and counter are placed to minimize trace lengths between sequential stages.  
  - Decoupling capacitors are located very close to the power pins of the ICs.

- **Routing**
  - High-frequency signal traces are kept short and separated from each other where possible.  
  - Power traces are slightly wider to reduce resistance and inductance.

- **Ground plane**
  - A continuous **GND copper pour** is used to provide a low-impedance return path and reduce crosstalk.

If these files exist in the repository, they illustrate the design:

```markdown
![Schematic](Schematic.png)
![PCB 3D – Top](PCB.png)
![PCB 3D – Bottom](PCB2.png)
![Wire-wrap Prototype](physical_connected.png)
![Prototype with Supply Connected](physical_connected_withVCCandGND.png)
```

Make sure the filenames in the repo match these names or update the links accordingly.

---

## 📁 Suggested Repository Structure

You can organize the repository, for example, as follows:

- `kicad/` – KiCad project files (`.kicad_pro`, `.kicad_sch`, `.kicad_pcb`, etc.).  
- `images/` – Schematic screenshots, PCB layout and 3D renders, prototype photos.  
- `README.md` – Project overview and documentation (this file).

---

## 🔧 How to Use / Reproduce

1. **Open the KiCad project**  
   - Install KiCad (version 7 or later recommended).  
   - Open the project file from the `kicad/` directory.

2. **Review the schematic and layout**  
   - Examine the connections between the oscillator, flip-flops, counter, capacitors and resistors.  
   - Inspect the ground plane and placement for high-frequency signals.

3. **Generate fabrication files**  
   - From KiCad, generate **Gerber** and **drill** files and send them to a PCB manufacturer.

4. **Assemble the board**  
   - Solder the components according to the schematic/BOM.  
   - Connect a 5 V supply and the high-frequency clock input.  
   - Measure the output with an oscilloscope and verify the expected divided frequency and waveform quality.

---

## 📌 Key Learning Outcomes

This project demonstrates that:

- **High-frequency digital circuits are very sensitive** to wiring, parasitics and PCB layout.  
- Simple measures such as **decoupling capacitors**, **short traces**, **proper grounding** and **pull-down resistors** can greatly reduce noise and crosstalk.  
- **Oscilloscope measurements are essential**; many real-world effects do not appear in ideal digital simulations.  
- Moving from a hand-wired prototype to a **designed PCB** significantly improves stability, repeatability and suitability for manufacturing.

---

## 👥 Contributors

- **Bshara Habib**  
- **Francis Aboud**  
- **Maria Nakhleh**  
- **Tatiana Abu Shakra**
