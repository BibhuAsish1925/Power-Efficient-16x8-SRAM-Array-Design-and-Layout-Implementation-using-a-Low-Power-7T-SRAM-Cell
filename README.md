# Power-Efficient-16-8-SRAM-Array-Design-and-Layout-Implementation-using-a-Low-Power-7T-SRAM-Cell

## Project Overview
This project presents the design and analysis of a **power-efficient 16×8 SRAM memory array** using a **7-Transistor (7T) SRAM cell** architecture.  
The objective is to improve **read stability and reduce power consumption** compared to the conventional **6T SRAM cell**.

The design integrates SRAM cells with essential **peripheral circuits** such as row decoder, precharge circuit, write driver, and sense amplifier to demonstrate complete memory functionality.

All circuits are designed and simulated using **Cadence Virtuoso in 180 nm CMOS technology**.

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
