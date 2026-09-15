# STM32_Bluetooth_Hardware_Design_PCB
4‑layer PCB (49 × 24 mm, 1.6 mm) using STM32WB55CEU6 for Bluetooth. Features USB‑C with ESD protection, RF + U.FL antenna, SWD debug header, and SMPS power. Includes impedance‑controlled routing, custom footprint (DLF162500LT‑5028A1), 3D STEP models, and validated with ERC/DRC checks.

# 📡 STM32WB55 Bluetooth Hardware Design (KiCad, 4‑Layer)

## 📖 Project Overview
This project is a **4‑layer PCB design** using **STM32WB55CEU6 microcontroller** for Bluetooth communication.  
It integrates USB‑C interface, RF with U.FL antenna connector, SWD debug header, and regulated 3.3V supply.  
Custom footprints and 3D models were created to ensure accurate visualization and manufacturing readiness.

---

## 📐 PCB Specifications
- **Board size:** 49 mm × 24 mm  
- **Thickness:** 1.6 mm  
- **Layers:** 4‑layer stackup  
- **Copper Pour:**  
  - **Layer 1 (Front):** GND plane  
  - **Layer 2 (In1):** GND plane  
  - **Layer 3 (In2):** GND plane  
  - **Layer 4 (Bottom):** Power plane  
- **Impedance Control:**  
  - 50 Ω ±10% single‑ended microstrip (trace width 0.19 mm)  
  - 90 Ω ±10% differential microstrip (trace width 0.22 mm, spacing 0.15 mm)  

---

## 🔌 Schematic Explanation

### Power Supply & SMPS
- **MIC5365‑3.3 LDO regulator** converts USB 5V to 3.3V.  
- Multiple **decoupling capacitors (100nF)** placed near VDD pins.  
- **SMPS pins (VLXSMPS, SMPSLX, SMPSFB, VFBSMPS)** connected with inductors/capacitors for internal buck converter.  
- Provides efficient power delivery for RF and digital domains.
- This reduces power consumption compared to pure LDO mode.

**Working:**  
STM32WB55 uses an internal buck converter. VLXSMPS pin drives the inductor, SMPSFB senses feedback, and VFBSMPS stabilizes output.This lowers current draw and heat, especially important for battery‑powered designs.

---

### ESD Protection
- **USBLC6‑2SC6 diode array** protects USB D+ and D‑ lines.  
- Ensures compliance with USB 2.0 signal integrity while clamping high‑voltage spikes
- Prevents damage from static discharge when plugging/unplugging USB‑C.  

---

### SWD Debug Connection
- **SWD_CLK (PA14)** → Debug clock.  
- **SWD_DIO (PA13)** → Bidirectional data line.  
- **SWO (PB3)** → Trace output.  
- **NRST** → Reset line.  
- Connected via **Tag‑Connect header** for programming/debugging. 

---

### RF Front‑End
- RF output routed through **matching network (L3, capacitors)**. - **DLF162500LT low‑pass filter** ensures clean 2.4–2.5 GHz band. - **U.FL coaxial connector** for external antenna.  
- Ground stitching vias improve impedance control and reduce noise.

**Working:**  
MCU generates Bluetooth RF signal → passes through matching network → filtered → sent to antenna. Impedance control (50 Ω single‑ended) ensures maximum power transfer and minimal reflection.

---

### USB‑C Interface
- USB‑C connector with **CC1/CC2 resistors** for orientation detection.  
- D+ / D‑ routed with **90 Ω differential impedance**.  
- Protected by ESD diodes.  
- VBUS feeds the LDO regulator.

---

### Peripherals
- **UART header** for communication/debugging.  
- **LED with resistor** for status indication.  
- **Push button** for Boot0/reset.  
- **Crystals:**  
  - HSE (32 MHz) → system clock.  
  - LSE (32.768 kHz) → RTC.  

---

## ✅ Design Validation
- **ERC check:** Successfully completed for schematic (no electrical rule errors).  
- **DRC check:** Successfully completed for PCB layout (no design rule violations).  

---

## ⚙️ How It Works
1. USB‑C provides 5V → LDO converts to 3.3V → SMPS stabilizes supply.  
2. MCU runs with external crystals for accurate timing.  
3. SWD header allows firmware flashing and debugging.  
4. Bluetooth RF routed through matching network + LPF → antenna.  
5. USB‑C handles data, UART header provides serial debug.  
6. ESD diodes protect USB lines, ground stitching reduces noise.  
7. LED shows status, push button controls Boot0/reset.  

---

## 🛠️ Skill Highlights
- KiCad schematic capture & 4‑layer PCB design  
- Custom footprint creation (DLF162500LT‑5028A1)  
- 3D STEP model integration (MCU, filter, crystal)  
- Impedance‑controlled routing (USB & RF)  
- SWD debug integration  
- USB‑C interface with ESD protection  
- RF matching & antenna connector design  
- ERC & DRC validation for schematic and PCB  
- Copper pour strategy (3 GND planes + 1 power plane)  
- Gerber/BOM/pick‑and‑place generation  
- Ground stitching & copper pour techniques  
