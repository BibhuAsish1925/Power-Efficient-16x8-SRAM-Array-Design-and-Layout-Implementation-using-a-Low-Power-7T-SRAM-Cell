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

## Conventional 6T SRAM Cell Architecture

The conventional Static Random Access Memory (SRAM) cell consists of **six transistors (6T)** forming a bistable latch capable of storing one bit of data. The structure is composed of **two cross-coupled CMOS inverters** and **two access transistors** that connect the cell to the bitlines during read and write operations.

### 6T SRAM Structure

The 6T SRAM cell consists of:

- **2 Pull-Up PMOS Transistors (P1, P2)**
- **2 Pull-Down NMOS Transistors (N1, N2)**
- **2 Access NMOS Transistors (N3, N4)**

The cross-coupled inverters store the data, while the access transistors allow the memory cell to communicate with the bitlines.

### Main Nodes

- **Q** – Stored data node  
- **QB (Q̅)** – Complementary data node  
- **BL** – Bitline  
- **BLB** – Complementary bitline  
- **WL** – Wordline

### SRAM Operations

#### Hold Operation
When the **wordline (WL) = 0**, the access transistors are OFF and the cell is isolated from the bitlines.  
The cross-coupled inverters maintain the stored value using positive feedback.

#### Write Operation
1. The write driver forces **BL and BLB** according to the input data.
2. **WL is asserted (WL = 1)** enabling the access transistors.
3. The forced bitline values overpower the internal node and change the stored data.

Example:
- BL = 1, BLB = 0 → Q = 1
- BL = 0, BLB = 1 → Q = 0

#### Read Operation
1. Bitlines are **precharged to VDD**.
2. **WL = 1** activates the access transistors.
3. The internal node storing **0 discharges one bitline slightly**.
4. The **sense amplifier detects the small voltage difference** and amplifies it to produce the output data.

### Limitations of 6T SRAM

Although the 6T SRAM cell is widely used, it suffers from several challenges in scaled technologies:

- Read disturb problem
- Reduced Static Noise Margin (SNM)
- Increased leakage current
- Sensitivity to process variations
- Higher power consumption in large arrays

Due to these limitations, alternative SRAM architectures such as **7T SRAM** are proposed to improve stability and reduce power consumption.

---

## Transistor Sizing Analysis

Proper transistor sizing is essential for stable SRAM operation. The sizing of pull-up, pull-down, and access transistors determines the **read stability, write ability, and overall reliability** of the memory cell.

The sizing constraints are derived using **MOSFET current equations and Kirchhoff current relations**.

### MOSFET Saturation Current Equation

The drain current of a MOS transistor operating in saturation is given by:

ID = (1/2) μ Cox (W/L) (VGS − VT)²

Where:

μ → Carrier mobility  
Cox → Oxide capacitance per unit area  
W/L → Transistor aspect ratio  
VGS → Gate-to-source voltage  
VT → Threshold voltage  

The parameter **β (beta)** represents the transistor strength:

β = μ Cox (W/L)

---

### Read Stability Condition

During the read operation, the access transistor connects the internal storage node to the bitline.  
To avoid flipping the stored data, the **pull-down transistor must be stronger than the access transistor**.

Condition:

βPD > βAX

Where:

βPD → Pull-down NMOS strength  
βAX → Access transistor strength  

The **Cell Ratio (CR)** is defined as:

CR = (W/L)pull-down / (W/L)access

Typical design requirement:

CR ≥ 1.5

This ensures that the internal node storing logic '0' remains stable during read operation.

---

### Write Ability Condition

During write operation, the access transistor must be strong enough to overwrite the internal node.

Condition:

βAX > βPU

Where:

βPU → Pull-up PMOS strength  

The **Pull-up Ratio (PR)** is defined as:

PR = (W/L)access / (W/L)pull-up

Typical requirement:

PR ≥ 1

This allows the bitline driver to successfully change the stored data.

---

### Summary of Sizing Constraints

| Parameter | Condition | Purpose |
|----------|-----------|--------|
| Pull-Down > Access | βPD > βAX | Read stability |
| Access > Pull-Up | βAX > βPU | Write ability |
| Cell Ratio (CR) | ≥ 1.5 | Prevent read disturb |
| Pull-up Ratio (PR) | ≥ 1 | Enable successful write |

---

### Transistor Width Configuration

| Transistor | Function | Width (W) |
|-----------|----------|----------|
| Pull-Up PMOS (P1, P2) | Maintain stored value | 400nm |
| Pull-Down NMOS (N1, N2) | Strong discharge during read | 1.2um |
| Access NMOS (N3, N4) | Connect cell to bitlines | 600nm |

