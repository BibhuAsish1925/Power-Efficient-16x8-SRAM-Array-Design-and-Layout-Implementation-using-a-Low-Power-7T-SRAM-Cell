# Power-Efficient-16-8-SRAM-Array-Design-and-Layout-Implementation-using-a-Low-Power-7T-SRAM-Cell

## Project Overview
This project presents the design and analysis of a **power-efficient 16×8 SRAM memory array** using a **7-Transistor (7T) SRAM cell** architecture. The objective is to improve **read stability and reduce power consumption** compared to the conventional **6T SRAM cell**. The design integrates SRAM cells with essential **peripheral circuits** such as row decoder, precharge circuit, write driver, and sense amplifier to demonstrate complete memory functionality. All circuits are designed and simulated using **Cadence Virtuoso in 180 nm CMOS technology**.

---
## Problem Statement

Conventional **6T SRAM cells** are widely used in memory architectures due to their compact structure and fast operation. However, with the continuous scaling of CMOS technology, several design challenges have emerged that affect the reliability and efficiency of SRAM-based memory systems.

One of the major issues in conventional SRAM cells is **read stability degradation**. During a read operation, the access transistor connects the internal storage node to the bitline, which can disturb the stored data. This disturbance reduces the **Static Noise Margin (SNM)** of the cell and may lead to read failures.

Another significant concern is **leakage power consumption**. As transistor dimensions shrink and threshold voltages decrease, **subthreshold leakage currents** increase considerably. Since SRAM arrays contain thousands or millions of cells, leakage currents accumulate and lead to significant standby power consumption.

Additionally, conventional SRAM cells face the following challenges:

- **Reduced static noise margin (SNM)** due to device scaling
- **Increased leakage current** in deep submicron technologies
- **Sensitivity to process variations**
- **Read disturb problems**
- **Higher power consumption during operation**

To overcome these limitations, this project proposes a **7T SRAM cell architecture** that introduces an additional transistor to improve cell stability and reduce power dissipation. The additional transistor helps isolate the storage nodes during certain operations, thereby improving **read stability and reducing leakage paths**.

The objective of this project is to design and analyze a **power-efficient 7T SRAM memory system** integrated with peripheral circuits and compare its performance with the conventional **6T SRAM architecture** in terms of **stability, power consumption, and reliability**.
---

## Key Features
- Design of **6T and 7T SRAM cells**
- Implementation of **16×8 SRAM memory array**
- Integration of peripheral circuits:
  - 4×16 Row Decoder
  - Precharge Circuit
  - Write Driver
  - Sense Amplifier
- **Read and Write functional verification**
- **Static Noise Margin (SNM) analysis**
- **Power consumption comparison**
- **Layout implementation of basic logic circuits**

---

## SRAM Architecture

The complete SRAM system consists of the following blocks:

- **SRAM Cell Array** – Stores data using SRAM cells  
- **Row Decoder** – Selects the wordline based on address input  
- **Precharge Circuit** – Precharges and equalizes bitlines before read operation  
- **Write Driver** – Drives data onto bitlines during write operation  
- **Sense Amplifier** – Detects and amplifies small voltage difference during read  

---
.

---

## Key Features
- Design of **6T and 7T SRAM cells**
- Implementation of **16×8 SRAM memory array**
- Integration of peripheral circuits:
  - 4×16 Row Decoder
  - Precharge Circuit
  - Write Driver
  - Sense Amplifier
- **Read and Write functional verification**
- **Static Noise Margin (SNM) analysis**
- **Power consumption comparison**
- **Layout implementation of basic logic circuits**

---

## SRAM Architecture

The complete SRAM system consists of the following blocks:

- **SRAM Cell Array** – Stores data using SRAM cells  
- **Row Decoder** – Selects the wordline based on address input  
- **Precharge Circuit** – Precharges and equalizes bitlines before read operation  
- **Write Driver** – Drives data onto bitlines during write operation  
- **Sense Amplifier** – Detects and amplifies small voltage difference during read  

---
