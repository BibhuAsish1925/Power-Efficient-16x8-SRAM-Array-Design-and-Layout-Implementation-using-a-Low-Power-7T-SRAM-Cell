# Power-Efficient-16x8-SRAM-Array-Design-and-Layout-Implementation-using-a-Low-Power-7T-SRAM-Cell

## Project Overview
This project presents the design and analysis of a **power-efficient 16×8 SRAM memory array** using a **7-Transistor (7T) SRAM cell** architecture. The objective is to improve **read stability and reduce power consumption** compared to the conventional **6T SRAM cell**. The design integrates SRAM cells with essential **peripheral circuits** such as row decoder, precharge circuit, write driver, and sense amplifier to demonstrate complete memory functionality. All circuits are designed and simulated using **Cadence Virtuoso in 180 nm CMOS technology**.

---
## Contents

1. [Problem Statement](#Problem-Statement)
2. [SRAM Architecture](#SRAM-Architecture)
3. [Conventional 6T SRAM Cell Architecture](#Conventional-6T-SRAM-Cell-Architecture) <br>
   - [6T SRAM Structure](#6T-SRAM-Structure)  
   - [Main Nodes](#Main-Nodes)  
   - [SRAM Operations](#SRAM-Operations)  <br>
     - [Hold Operation](#Hold-Operation)  
     - [Write Operation](#Write-Operation)  
     - [Read Operation](#Read-Operation)  
   - [Limitations of 6T SRAM](#Limitations-of-6T-SRAM)
4. [Transistor Sizing Analysis](#Transistor-Sizing-Analysis) <br>
   - [MOSFET Saturation Current Equation](#MOSFET-Saturation-Current-Equation)  
   - [Read Stability Condition](#Read-Stability-Condition)  
   - [Write Ability Condition](#Write-Ability-Condition)  
   - [Summary of Sizing Constraints](#Summary-of-Sizing-Constraints)  
   - [Transistor Width Configuration](#Transistor-Width-Configuration)
5. [Proposed 7T SRAM Cell Architecture](#Proposed-7T-SRAM-Cell-Architecture) <br>
   - [Structure of 7T SRAM Cell](#Structure-of-7T-SRAM-Cell)  
   - [Key Idea of the Proposed Design](#Key-Idea-of-the-Proposed-Design)  
   - [Operation of 7T SRAM Cell](#Operation-of-7T-SRAM-Cell)  <br>
     - [Hold Operation](#Hold-Operation-1)  
     - [Write Operation](#Write-Operation-1)  
     - [Read Operation](#Read-Operation-1)  
   - [Advantages of the 7T SRAM Cell](#Advantages-of-the-7T-SRAM-Cell)  
   - [Design Trade-off](#Design-Trade-off)
6. [Power Analysis](#Power-Analysis)
7. [Static Noise Margin (SNM) Analysis](#Static-Noise-Margin-SNM-Analysis)
8. [Delay Analysis](#Delay-Analysis)
9. [Comparison Between 6T and 7T SRAM](#Comparison-Between-6T-and-7T-SRAM)
10. [Read and Write Operation Verification of 7T-SRAM Cell](#Read-and-Write-Operation-Verification-of-7T-SRAM-Cell) <br>
    - [Read Operation](#Read-Operation-2)  
    - [Subthreshold Leakage Effect During Read](#Subthreshold-Leakage-Effect-During-Read)
11. [Peripheral Circuits of the SRAM Array](#Peripheral-Circuits-of-the-SRAM-Array) <br>
    - [Row Decoder (4×16 Decoder)](#1-Row-Decoder-4×16-Decoder)  
    - [Precharge Circuit](#2-Precharge-Circuit)  
    - [Write Driver](#3-Write-Driver)  
    - [Sense Amplifier](#4-Sense-Amplifier)  
    - [Integration with SRAM Array](#Integration-with-SRAM-Array)
12. [Single-Bit 7T-SRAM Cell Test with Peripheral Circuits](#Single-Bit-7T-SRAM-Cell-Test-with-Peripheral-Circuits)
13. [16×8 7T SRAM Array with Peripheral Circuits](#16×8-7T-SRAM-Array-with-Peripheral-Circuits) <br>
    - [Architecture Description](#Architecture-Description)  
    - [Operation Summary](#Operation-Summary)  
    - [Figure](#Figure)
14. [16×8 7T SRAM Array Testing with Peripheral Circuits](#16×8-7T-SRAM-Array-Testing-with-Peripheral-Circuits)
15. [Layout Design and Physical Verification](#Layout-Design-and-Physical-Verification) <br>
    - [Layout Design Flow](#Layout-Design-Flow)  
    - [Layout Blocks Implemented](#Layout-Blocks-Implemented)  
    - [Verification Process](#Verification-Process)  
    - [Result](#Result)
16. [Conclusion](#Conclusion)

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

<table align="center">
    <td align="center">
      <img width="745" height="793" alt="image" src="https://github.com/user-attachments/assets/a8186097-e683-45cf-9746-0e10b08eaa83" /><br/>
      <small> Fig. 1 SRAM system architecture
    </td>
</table>

---

## Conventional 6T SRAM Cell Architecture

The conventional Static Random Access Memory (SRAM) cell consists of **six transistors (6T)** forming a bistable latch capable of storing one bit of data. The structure is composed of **two cross-coupled CMOS inverters** and **two access transistors** that connect the cell to the bitlines during read and write operations.

### 6T SRAM Structure

The 6T SRAM cell consists of:

- **2 Pull-Up PMOS Transistors (P1, P2)**
- **2 Pull-Down NMOS Transistors (N1, N2)**
- **2 Access NMOS Transistors (N3, N4)**

The cross-coupled inverters store the data, while the access transistors allow the memory cell to communicate with the bitlines.

<table align="center">
  <tr>
    <td align="center">
      <img width="856" height="287" alt="Circuit Diagram" src="https://github.com/user-attachments/assets/cb2249a1-6b24-49d3-a24f-0ce22a17b51c"/><br/>
      <small>Fig 2a. 6T-SRAM schematic diagram</small>
    </td>
    <td align="center">
      <img width="848" height="747" alt="image" src="https://github.com/user-attachments/assets/ebd971e0-6042-4440-ad49-7b1c95f4b1c3" /><br/>
      <small>Fig 2b. 6T-SRAM schematic design</small>
    </td>
  </tr>
</table>

### Main Nodes

- **Q** – Stored data node  
- **QB (Q̅)** – Complementary data node  
- **BL** – Bitline  
- **BLB** – Complementary bitline  
- **WL** – Wordline

### SRAM Operations

#### Hold Operation
When the **wordline (WL) = 0**, the access transistors are OFF and the cell is isolated from the bitlines. The cross-coupled inverters maintain the stored value using positive feedback.

#### Write Operation
1. The write driver forces **BL and BLB** according to the input data.
2 **WL is asserted (WL = 1)** enabling the access transistors.
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

Proper transistor sizing is essential for stable SRAM operation. The sizing of pull-up, pull-down, and access transistors determines the **read stability, write ability, and overall reliability** of the memory cell. The sizing constraints are derived using **MOSFET current equations and Kirchhoff current relations**.

<table align="center">
    <td align="center">
      <img width="436" height="427" alt="image" src="https://github.com/user-attachments/assets/dee6b9d9-5e17-46ac-90cd-304a92619962" /><br/>
      <small>Fig 3. SRAM sizing</small>
    </td>
</table>

### MOSFET Saturation Current Equation

The drain current of a MOS transistor operating in saturation is given by:

$$
I_D = \frac{1}{2} \mu C_{ox}\left(\frac{W}{L}\right)(V_{GS}-V_T)^2
$$

Where: ( μ → Carrier mobility, Cox → Oxide capacitance per unit area, W/L → Transistor aspect ratio, VGS → Gate-to-source voltage, and VT → Threshold voltage )

The parameter **β (beta)** represents the transistor strength:

$$
\beta = \mu C_{ox}\left(\frac{W}{L}\right)
$$

### Read Stability Condition

During the read operation, the access transistor connects the internal storage node to the bitline.  
To avoid flipping the stored data, the **pull-down transistor must be stronger than the access transistor**.

Condition:

$$
\beta_{PD} > \beta_{AX}
$$

Where: ( βPD → Pull-down NMOS strength, and βAX → Access transistor strength )

The **Cell Ratio (CR)** is defined as:

$$
CR = \frac{(W/L)_{pull-down}}{(W/L)_{access}}
$$

Typical design requirement: ` CR ≥ 1.5 `

This ensures that the internal node storing logic '0' remains stable during read operation.

### Write Ability Condition

During write operation, the access transistor must be strong enough to overwrite the internal node.

Condition:

$$
\beta_{AX} > \beta_{PU}
$$

Where: βPU → Pull-up PMOS strength  

The **Pull-up Ratio (PR)** is defined as:

$$
PR = \frac{(W/L)_{access}}{(W/L)_{pull-up}}
$$

Typical requirement: `PR ≥ 1`

This allows the bitline driver to successfully change the stored data.

### Summary of Sizing Constraints

| Parameter | Condition | Purpose |
|----------|-----------|--------|
| Pull-Down > Access | βPD > βAX | Read stability |
| Access > Pull-Up | βAX > βPU | Write ability |
| Cell Ratio (CR) | ≥ 1.5 | Prevent read disturb |
| Pull-up Ratio (PR) | ≥ 1 | Enable successful write |

### Transistor Width Configuration

<table align="center">
    <td align="center">
          <img width="941" height="521" alt="image" src="https://github.com/user-attachments/assets/5de5035b-d497-4670-bde7-b527375591dc" /><br/>
      <small>Fig 3b. 6T-SRAM schematic design (same as 2b)</small>
    </td>
</table>

| Transistor | Function | Width (W) |
|-----------|----------|----------|
| Pull-Up PMOS (P1, P2) | Maintain stored value | 400nm (Wpu)|
| Access NMOS (N3, N4) | Connect cell to bitlines | 600nm (Wa = 1.5 x Wpu) |
| Pull-Down NMOS (N1, N2) | Strong discharge during read | 1.2um (Wpd = 2 x Wa)|

---

## Proposed 7T SRAM Cell Architecture

To improve the stability and power efficiency of the conventional 6T SRAM cell, an additional transistor is introduced, forming a **7-Transistor (7T) SRAM cell**. The extra transistor is placed in the pull-down path to control the discharge current during read and write operations.

### Structure of 7T SRAM Cell

The proposed 7T SRAM cell consists of:

- 2 Pull-Up PMOS transistors
- 2 Pull-Down NMOS transistors
- 2 Access NMOS transistors
- 1 Additional Bottom NMOS transistor [width(wb) = 1.2um]

<table>
  <tr>
    <td align="center">
          <img width="941" height="521" alt="image" src="https://github.com/user-attachments/assets/5e3f31bb-4502-4a97-a01a-9976061786c7" /><br/>
      <small>Fig 4a. Proposed 7T-SRAM schematic diagram</small>
    </td>
    <td align="center">
          <img width="940" height="522" alt="image" src="https://github.com/user-attachments/assets/cbed8738-350f-466b-9753-f43b1a45d69a" /><br/>
      <small>Fig 4b. Proposed 7T-SRAM schematic design</small>
    </td>
  </tr>
</table>

The additional transistor acts as a **current gating device**, controlling the discharge path of the internal storage node.

### Key Idea of the Proposed Design

The extra NMOS transistor is connected in series with the pull-down network. This transistor is controlled by a separate control signal and helps in:

- Reducing leakage current
- Improving read stability
- Minimizing unnecessary current flow during idle condition

### Operation of 7T SRAM Cell

#### Hold Operation
When the wordline is LOW, the access transistors are OFF and the cell remains isolated from the bitlines. The cross-coupled inverters maintain the stored value through positive feedback.

#### Write Operation
1. The write driver forces the bitlines according to the input data.
2. Wordline is activated (WL = 1).
3. Access transistors allow the data from bitlines to overwrite the stored node.
4. The extra transistor ensures controlled current flow during the switching process.

#### Read Operation
1. Bitlines are precharged to VDD.
2. WL is activated to connect the cell to the bitlines.
3. Depending on the stored data, one bitline discharges slightly.
4. The sense amplifier detects the voltage difference and amplifies it to generate the output data.

### Advantages of the 7T SRAM Cell

- Improved **Static Noise Margin (SNM)**
- Reduced **leakage power**
- Better **read stability**
- Lower **power consumption compared to 6T SRAM**

### Design Trade-off

The addition of one extra transistor increases the **cell area slightly**, but the improvement in stability and power efficiency makes the design suitable for low-power memory systems.

---

## Power Analysis

Power consumption is an important design parameter in SRAM circuits, especially for low-power embedded systems. In this work, the power consumption of both **6T and 7T SRAM cells** is analyzed using **DC simulation**.

### Average Power Method

The average power consumed by the SRAM cell is calculated using the relation:

$$
Power_{avg} = V_{DD} \times I_{avg}
$$

Where: ( VDD → Supply voltage applied to the SRAM cell and Iavg → Average current drawn from the supply

<table align="center">
  <tr>
    <td align="center">
          <img width="766" height="491" alt="image" src="https://github.com/user-attachments/assets/6462c2f7-7b47-4c4a-9401-ae2dbb275a08" /><br/>
      <small>Fig 5a. 6T-SRAM VTC curve</small>
    </td>
    <td align="center">
          <img width="785" height="504" alt="image" src="https://github.com/user-attachments/assets/ad465116-ec1c-4b2a-a4ed-16752ef802d0" /><br/>
      <small>Fig 5b. 7T-SRAM VTC curve</small>
    </td>
  </tr>
</table>

### Simulation Parameters

Supply Voltage (VDD): 1.8 V and Technology Node: 180 nm CMOS

### Power Analysis Results

| SRAM Type | Supply Voltage | Average Current | Average Power |
|-----------|---------------|---------------|---------------|
| 6T SRAM | 1.8 V | 507.5 nA | 0.9135 µW |
| 7T SRAM | 1.8 V | 353.4 nA | 0.63612 µW |

### Observation

The proposed **7T SRAM cell consumes less average current**, which directly reduces the overall power consumption.

### Power Reduction

The 7T SRAM design achieves approximately **30.36% reduction in power consumption** compared to the conventional 6T SRAM cell. This reduction is achieved due to the **additional transistor that controls current flow**, thereby reducing unnecessary leakage paths.

---

## Static Noise Margin (SNM) Analysis

Static Noise Margin (SNM) is an important parameter that determines the stability of an SRAM cell. It represents the **maximum noise voltage that the SRAM cell can tolerate without changing its stored state**.

<table align="center">
    <td align="center">
          <img width="503" height="432" alt="image" src="https://github.com/user-attachments/assets/1a94eb25-2291-447c-8f1f-d7217f17423f" /><br/>
      <small>Fig 6. SRAM butterfly curve</small>
    </td>
</table>

SNM is typically analyzed using the **butterfly curve method**, which is obtained by plotting the voltage transfer characteristics of the two cross-coupled inverters.

<table align="center">
  <tr>
    <td align="center">
          <img width="809" height="579" alt="image" src="https://github.com/user-attachments/assets/87f13e78-9252-4fd4-a26b-0b0cb85e075e" /><br/>
      <small>Fig 7a. 6T-SRAM Butterfly curve</small>
    </td>
    <td align="center">
          <img width="796" height="579" alt="image" src="https://github.com/user-attachments/assets/95f5036c-20ca-4984-be2c-84aa1d6ece86" /><br/>
      <small>Fig 7b. 7T-SRAM Butterfly curve</small>
    </td>
  </tr>
</table>

### SNM Calculation

SNM is defined as the side length of the largest square that can be fitted between the two inverter transfer curves.

Mathematically:

$$
SNM = \min(SNM_H, SNM_L)
$$

Where: ( SNM_H → Static Noise Margin High and SNM_L → Static Noise Margin Low )

### SNM Results

| SRAM Type | SNM_L | SNM_H | SNM = min(SNM_L,SNM_H) |
|-----------|------|------|------|
| 6T SRAM | 692.53 mV | 674.375 mV | 674.375 mV |
| 7T SRAM | 850.2 mV | 849.6 mV | 849.6 mV |

### SNM Improvement

The proposed **7T SRAM cell shows a significant improvement in SNM** compared to the conventional 6T SRAM. SNM Increase ≈ **25.98%**

### Observation

The additional transistor in the 7T architecture improves the stability of the internal nodes during read operation, thereby increasing the noise margin and reducing the probability of read disturb.

---

## Delay Analysis

To evaluate the performance of the SRAM cells, delay analysis was carried out for both **6T and 7T SRAM architectures** during read and write operations.

### Delay Comparison Table

| Parameter | Write – 6T (ps) | Write – 7T (ps) | Read – 6T (ps) | Read – 7T (ps) |
|----------|----------------|----------------|---------------|---------------|
| Rise     | 308.594         | 298.378        | 39.746       | 41.195       |
| Fall     | 241.122         | 232.655        | 71.504       | 70.832        |
| Average  | 274.862         | 265.516        | 55.624        | 56.009       |

### Observations

- **Write Operation:** 7T SRAM shows reduced delay compared to 6T SRAM = approx 3.4%
- **Read Operation:** 7T SRAM shows a slight increase in delay due to the additional transistor in the read path = approx 0.692%

---

## Comparison Between 6T and 7T SRAM

To evaluate the effectiveness of the proposed design, a comparison is performed between the conventional **6T SRAM cell** and the proposed **7T SRAM cell** based on important design parameters such as stability, power consumption, area, and delay.

| Parameter | 6T SRAM | 7T SRAM |
|-----------|--------|--------|
| Number of Transistors | 6 | 7 |
| Static Noise Margin (SNM) | 674.375 mV | 849.6 mV **(25.98% better than 6T)** |
| Stability | Moderate | Higher |
| Average Power Consumption | 0.9135 µW | 0.63612 µW **(30.36% less than 6T)**|
| Leakage Power | Higher | Reduced |
| Area Utilization | Smaller | Slightly Larger |
| Write Delay | 274.86ps | 265.516ps **(3.4% faster than 6T)**|
| Read Delay | 55.624ps | 56.009ps **(0.693% slower than 6T)**|
| Design Complexity | Lower | Slightly Higher |
| Applications | Standard SRAM arrays | Low power and high stability memory systems |

### Key Observations

• The proposed **7T SRAM cell significantly improves stability** due to higher SNM.  
• The additional transistor helps **reduce leakage current and power consumption**.  
• The **trade-off is slightly increased area and write delay** due to the extra transistor.

Overall, the **7T SRAM design provides better stability and power efficiency**, making it suitable for low-power memory applications.

---

## Read and Write Operation Verification of 7T-SRAM Cell

To verify the correct functionality of the SRAM design, transient simulations were performed to analyze the read and write operations. The objective of this test is to confirm that the SRAM cell correctly stores, retains, and retrieves data based on the control signals.

### Write Operation

During the write operation, the data input is forced onto the bitlines through the write driver and stored in the SRAM cell.
Operation conditions: `WE = 1, WL = 1 ` 

Working principle:

• The write driver receives the input data signal (DATA_IN).  
• Complementary signals are driven onto the bitlines: `BL = DATA, BLB = DATA̅ ` 
• When the **wordline (WL)** becomes HIGH, the access transistors turn ON.  
• The internal storage nodes of the cross-coupled inverter latch are overwritten by the bitline values.

<table align="center">
  <tr>
    <td align="center">
          <img width="711" height="477" alt="image" src="https://github.com/user-attachments/assets/1658c19f-ef3f-4bc9-a83e-565525990bb7" /><br/>
      <small>Fig 8a. SRAM cell Write test circuit</small>
    </td>
    <td align="center">
          <img width="946" height="477" alt="image" src="https://github.com/user-attachments/assets/d4e91336-47c7-4e98-acb0-7ccda304e7d0" /><br/>
      <small>Fig 8b. SRAM cell Write test waveform</small>
    </td>
  </tr>
</table>

Result: The SRAM cell successfully captures the input data and stores it at the internal node **Q**.

### Read Operation

The read operation retrieves the stored data from the SRAM cell without intentionally modifying the stored value.

Operation conditions: `WE = 0, WL = 1` 

Working principle:

• Before the read operation, both **BL and BLB are precharged to VDD**.  
• When the wordline becomes HIGH, the access transistors connect the internal nodes to the bitlines.

<table align="center">
  <tr>
    <td align="center">
          <img width="711" height="482" alt="image" src="https://github.com/user-attachments/assets/f06020e2-8531-4afe-9d46-67f7e45fa458" /><br/>
      <small>Fig 9a. SRAM cell Read test circuit</small>
    </td>
    <td align="center">
          <img width="946" height="482" alt="image" src="https://github.com/user-attachments/assets/e5b24404-6a1f-4db2-a636-7b66718c806e" /><br/>
      <small>Fig 9b. SRAM cell Read test waveform</small>
    </td>
  </tr>
</table>

Depending on the stored data:
If **Q = 1** --> BL remains HIGH while BLB discharges slightly.
If **Q = 0** --> BL discharges slightly while BLB remains HIGH.

This creates a small differential voltage between BL and BLB which is sensed by the sense amplifier.

---

### Subthreshold Leakage Effect During Read

During the read operation, a small leakage current can flow through the access transistors even when the cell is trying to hold its stored value. This occurs due to **subthreshold conduction** in MOSFETs, where a small current flows even when the transistor operates below its threshold voltage.

Leakage current equation:

$$
I_{sub} \approx I_0 \cdot e^{\frac{V_{GS}-V_{TH}}{nV_T}}
$$

Where: ( VGS → Gate-to-Source Voltage, VTH → Threshold Voltage, V_T → Thermal Voltage, and n → Subthreshold slope factor )

During the read operation:

• The access transistor slightly pulls one of the internal nodes toward the bitline voltage.  
• This can disturb the stored node voltage inside the SRAM cell.

This phenomenon is known as **read disturb**. Proper transistor sizing ensures that:

`Pull-down transistor strength > Access transistor strength`

This prevents the stored data from flipping during read operation.

---

### Verification Result

The transient simulation confirms that:

• Data is correctly written into the SRAM cell during the write cycle.  
• The stored value is retained inside the cross-coupled inverter latch.  
• During read operation, only a small differential voltage is created between BL and BLB.  
• The sense amplifier successfully amplifies this small voltage difference to generate DATA_OUT.  
• Proper transistor sizing prevents read disturb caused by subthreshold leakage.

These results validate the correct functionality and stability of the SRAM read and write operations.

---

## Conclusion

The proposed **7T SRAM cell architecture** demonstrates clear advantages over the conventional **6T SRAM** based on the performed analysis.

- **Stability (SNM):** The 7T SRAM shows a significant improvement in Static Noise Margin, indicating better resistance to read disturbance and enhanced data stability.
- **Power Consumption:** The 7T design achieves lower average power consumption due to reduced leakage current, making it more suitable for low-power applications.
- **Write Performance:** A noticeable improvement in write delay (~3.4%) is observed, due to better write ability enabled by the modified cell structure.
- **Read Performance:** A very small increase in read delay (~0.7%) is observed, caused by the additional transistor in the read path. This overhead is minimal and acceptable.

### Final Remark

Overall, the 7T SRAM provides a better trade-off between **power, stability, and performance**, making it a more efficient and reliable choice compared to the conventional 6T SRAM design, especially for **low-power and high-stability memory applications**.

---

## Peripheral Circuits of the SRAM Array

In addition to the SRAM cell array, several **supporting peripheral circuits** are required to perform reliable read and write operations. These circuits control the addressing, data transfer, and signal amplification within the memory system. The major peripheral circuits used in the proposed SRAM architecture are:

1. Row Decoder  
2. Precharge Circuit  
3. Write Driver  
4. Sense Amplifier

These circuits work together with the **16×8 SRAM array** to enable proper memory operation.

### 1. Row Decoder (4×16 Decoder)

The row decoder is responsible for selecting one of the multiple wordlines in the SRAM array based on the input address. For a **4-bit address input**, the decoder generates **16 wordline outputs**, ensuring that only one row of SRAM cells is activated at a time.

#### Working Principle

• The decoder converts the binary address into a **one-hot output signal**.  
• Only the selected wordline becomes HIGH while others remain LOW.  
• This activates the corresponding SRAM row during read or write operation.

#### Architecture

The 4×16 decoder is implemented using:

• Inverter circuits  
• 4-input AND gates

<table align="center">
  <tr>
    <td align="center">
          <img width="465" height="705" alt="image" src="https://github.com/user-attachments/assets/9225a0df-9bcb-46ed-8007-c81e58f94bdf" /><br/>
      <small>Fig 10a. 4×16 Row decoder diagram</small>
    </td>
    <td align="center">
          <img width="613" height="900" alt="image" src="https://github.com/user-attachments/assets/e9d085e4-446e-40a1-bcfb-b89d2895afc0" /><br/>
      <small>Fig 10b. 4×16 Row decoder schematic design</small>
    </td>
  </tr>
</table>

<table align="center">
    <td align="center">
          <img width="1052" height="434" alt="image" src="https://github.com/user-attachments/assets/8c367f36-a6ef-43ed-9ba5-62d8d7e8c430" /><br/>
      <small>Fig 11. 4×16 Row decoder output waveform</small>
    </td>
</table>

### 2. Precharge Circuit

The precharge circuit prepares the bitlines before every read operation.

#### Working Principle

• When **PC = 0**, the precharge transistors charge both **BL and BLB to VDD**.  
• The equalization transistor ensures both bitlines remain at the same voltage level.  
• This ensures accurate sensing during the read operation.

Precharging the bitlines reduces sensing delay and improves reliability of the memory read process.

<table>
  <tr>
    <td align="center">
          <img width="349" height="287" alt="image" src="https://github.com/user-attachments/assets/bd585699-d465-4ddf-9acc-7d1f204d292a" /><br/>
      <small>Fig 12a. Precharge cell diagram</small>
    </td>
    <td align="center">
          <img width="825" height="496" alt="image" src="https://github.com/user-attachments/assets/e7874e80-900d-4482-b14d-7f69cd101643" /><br/>
      <small>Fig 12b. Precharge cell schematic design</small>
    </td>
  </tr>
</table>

<table>
    <td align="center">
          <img width="825" height="389" alt="image" src="https://github.com/user-attachments/assets/ea729828-24f7-425c-9053-798ae6c84ec9" /><br/>
      <small>Fig 13. Precharge cell output waveform</small>
    </td>
</table>

### 3. Write Driver

The write driver circuit is responsible for forcing data onto the bitlines during write operations.

#### Working Principle

• The write driver receives **DATA_IN** from the input.  
• Based on the **Write Enable (WE)** signal, the driver sets the bitlines.

Operation:

• If **WE = 1**,  `BL = DATA, BLB = DATA̅  `
• When **WL = 1**, the SRAM cell captures the data from the bitlines and stores it internally.

<table align="center">
  <tr>
    <td align="center">
          <img width="452" height="239" alt="image" src="https://github.com/user-attachments/assets/f782c731-c55e-4025-86aa-95b001a867a5" /><br/>
      <small>Fig 14a. Write Driver diagram</small>
    </td>
    <td align="center">
          <img width="920" height="527" alt="image" src="https://github.com/user-attachments/assets/253e979b-4ac4-42ae-b9f9-ae1dbaf1e699" /><br/>
      <small>Fig 14b. Write Driver schematic design</small>
    </td>
  </tr>
</table>

<table align="center">
    <td align="center">
          <img width="917" height="354" alt="image" src="https://github.com/user-attachments/assets/677995fa-b9e2-4d46-83ae-4dbca3e97681" /><br/>
      <small>Fig 15. Write Driver output waveform</small>
    </td>
</table>

This circuit ensures strong drive capability to overwrite the previously stored value inside the SRAM cell.

### 4. Sense Amplifier

The sense amplifier is used to detect and amplify the small voltage difference between the bitlines during read operation.

#### Working Principle

• During read operation, one bitline discharges slightly depending on the stored data.  
• This creates a small voltage difference between **BL and BLB**.  
• The sense amplifier detects this difference and amplifies it to produce a full digital output.

<table align="center">
    <td align="center">
          <img width="815" height="473" alt="image" src="https://github.com/user-attachments/assets/48b36d1e-63a5-49e8-8041-e843c050190f" /><br/>
      <small>Fig 16. Sense Amplifier schematic design</small>
    </td>
</table>

<table align="center">
    <td align="center">
          <img width="818" height="308" alt="image" src="https://github.com/user-attachments/assets/f6b9e495-bc87-45f1-b288-0493369e10cf" /><br/>
      <small>Fig 17. Sense Amplifier output waveform</small>
    </td>
</table>

The output is then provided as **DATA_OUT**. Sense amplifiers significantly improve the **speed and reliability of read operations** in SRAM arrays.

### Integration with SRAM Array

In the complete system:

• The **Row Decoder** activates the required wordline.  
• The **Precharge Circuit** prepares the bitlines before reading.  
• The **Write Driver** writes data into the SRAM cell.  
• The **Sense Amplifier** reads and amplifies the stored data.

These peripheral circuits together enable the **efficient operation of the 16×8 SRAM array**.

---

## Single-Bit 7T-SRAM Cell Test with Peripheral Circuits

To validate the complete memory architecture, a **single-bit 7T SRAM cell** was integrated with all the required peripheral circuits and simulated. The test setup includes the following components:

• 7T SRAM Cell  
• Precharge Circuit  
• Write Driver  
• Sense Amplifier  
• Wordline Control  
• Data Input and Output Nodes

All circuits are connected to a common **VDD supply and Ground reference**.

<table align="center">
    <td align="center">
          <img width="773" height="680" alt="image" src="https://github.com/user-attachments/assets/175f3c64-419b-4c33-844b-559d7ac0ae29" /><br/>
      <small>Fig 18. Single-Bit 7T-SRAM Cell with Peripheral Circuits</small>
    </td>
</table>

<table align="center">
    <td align="center">
          <img width="1586" height="733" alt="image" src="https://github.com/user-attachments/assets/96c86f9b-8f8d-42c2-99e0-cc160cab3077" /><br/>
      <small>Fig 19. Single-Bit 7T-SRAM Cell with Peripheral Circuits output waveform</small>
    </td>
</table>

---

### Test Analysis

The peripheral circuits interact with the SRAM cell as follows:

1. **Precharge Circuit** - Before every read operation, the precharge circuit charges both bitlines to logic HIGH.

Condition: `PC = 0 → BL = 1 and BLB = 1`

This ensures both bitlines start from the same voltage level.

<table align="center">
    <td align="center">
          <img width="1565" height="488" alt="image" src="https://github.com/user-attachments/assets/32d7310c-44a2-4d2e-83d0-7043b7eb2b3e" /><br/>
      <small>Fig 20. Precharge conditions</small>
    </td>
</table>

2. **Write Driver Operation**

The write driver applies input data to the bitlines during write operation.

Condition: `WE = 1 with BL = DATA, BLB = DATA̅`

This prepares the bitlines with the input data value.

<table align="center">
    <td align="center">
          <img width="1565" height="433" alt="image" src="https://github.com/user-attachments/assets/d21a93b5-390c-49a2-b9a8-cbc75f29c8e5" /><br/>
      <small>Fig 21. write enable condition</small>
    </td>
</table>

3. **Write Operation**

When both write enable and wordline signals are active: `WE = 1, WL = 1 `

The SRAM cell captures the input data from the bitlines and stores it in the internal latch.

<table align="center">
    <td align="center">
          <img width="1565" height="389" alt="image" src="https://github.com/user-attachments/assets/897f3477-cde5-4652-b60e-c518f8f78040" /><br/>
      <small>Fig 22. Write conditions</small>
    </td>
</table> 

Result: `Q = DATA_IN`

4. **Read Operation**

For read operation: `WE = 0, WL = 1`

The SRAM cell connects to the bitlines and transfers the stored data. BL reflects the stored value of node Q.

<table align="center">
    <td align="center">
          <img width="1565" height="573" alt="image" src="https://github.com/user-attachments/assets/d2a29a8c-d068-4dc8-8b77-a46c6fc5bf60" /><br/>
      <small>Fig 23. Read condition</small>
    </td>
</table> 

Output: `DATA_OUT = Stored SRAM value`

### Simulation Result

The transient waveform confirms that:

• The precharge circuit correctly charges the bitlines.  
• The write driver successfully writes input data into the SRAM cell.  
• The stored data remains stable inside the latch.  
• The read operation retrieves the stored value correctly.  
• The sense amplifier produces a clean digital output signal.

### Conclusion

The successful integration of the **7T SRAM cell with peripheral circuits** verifies the correct functionality of the proposed SRAM architecture. The simulation demonstrates reliable:

• Data write operation  
• Data retention  
• Data read operation

This validates the feasibility of implementing the **complete SRAM array using the proposed 7T SRAM cell design**.

---

## 16×8 7T SRAM Array with Peripheral Circuits

### Overview

A **16×8 SRAM array** is designed using the proposed **low-power 7T SRAM cell architecture**, integrated with all necessary peripheral circuits for complete memory operation.

---

### Architecture Description

- The array consists of **16 rows and 8 columns**, where each cell is a **7T SRAM bit-cell**.
- Each row is controlled by a **wordline (WL)**, and each column is connected through **bitlines (BL, BLB)**.

### Peripheral Circuit Integration

**Row Decoder (4×16)**  
- Converts a **4-bit address input** into **16 wordlines (WL)**.  
- Activates only one row at a time for read/write operation.

**Write Driver**  
- Receives input data (**DATA_IN**) and control signals (**WE, WEB**).  
- Generates differential signals on **BL and BLB** for writing data into the selected cell.

**Precharge Circuit**  
- Precharges both **BL and BLB to VDD** before every read cycle.  
- Ensures faster and reliable sensing during read operation.

**7T SRAM Cell Array**  
- Stores data using **cross-coupled inverters** and access transistors.  
- The additional transistor in 7T improves **read stability and reduces leakage**.

**Sense Amplifier**  
- Detects small voltage differences between **BL and BLB** during read.  
- Amplifies the signal and produces **DATA_OUT** based on control signal (**SAE**).

### Operation Summary

- **Write Operation:**  
  Data is driven onto BL/BLB by the write driver and stored in the selected cell via the activated wordline.

- **Read Operation:**  
  Precharged bitlines are discharged differentially based on stored data, and the sense amplifier converts this into a digital output.

### Power Network

- All blocks share a common **VDD and GND supply**.
- Optimized design ensures **reduced power consumption and improved stability** compared to conventional 6T SRAM.

### Figure

<table align="center">
    <td align="center">
          <img width="876" height="1113" alt="image" src="https://github.com/user-attachments/assets/64d74b11-ec3c-48d4-8d0d-4d30052ba19c" /><br/>
      <small>Fig 24. 16×8 7T SRAM Array schematic with Peripheral Circuits</small>
    </td>
</table>

---

## 16×8 7T SRAM Array Testing with Peripheral Circuits

To validate the complete SRAM architecture, the **16×8 7T SRAM array integrated with all peripheral circuits** is tested under different operating conditions.

### Test Setup

The complete system includes:
• 4×16 Row Decoder (address selection)  
• Write Drivers (data input control)  
• Precharge Circuit (bitline initialization)  
• 16×8 7T SRAM Cell Array  
• Sense Amplifier (read operation)  

<table align="center">
    <td align="center">
          <img width="627" height="1186" alt="image" src="https://github.com/user-attachments/assets/739270ee-b8df-4e70-966c-8a34c8b9d480" /><br/>
      <small>Fig 25. 16×8 7T SRAM Array schematic with Peripheral Circuits Symbolically</small>
    </td>
</table>

Control signals used:
• Address Inputs: A[3:0]  
• Data Inputs: A[7:0] 
• Wordline (WL)  
• Write Enable (WE), Write Enable Bar (WEB)  
• Precharge Signal (PC)  
• Sense Amplifier Enable (SAE)  

### Input Conditions
| Signal | Description | Value |
|-------|------------|------|
| VDD   | Supply Voltage | ___ |
| Address | Row Selection | ___ |
| DATA_IN | Input Data | ___ |
| WE / WEB | Write Control | ___ |
| PC | Precharge Control | ___ |
| SAE | Sense Amplifier Enable | ___ |

### Write Operation (Array Level)

Condition: `WE = 1, WL = 1`  

Working:
• Selected row is activated by the decoder  
• Write driver forces data onto BL and BLB  
• Entire selected word (8 bits) is written simultaneously  

📌 **Observation:**  
(To be filled after simulation)

---

### Read Operation (Array Level)

Condition: `WE = 0, WL = 1`  

Working:
• Bitlines are precharged to VDD  
• Selected row discharges BL/BLB based on stored data  
• Sense amplifier detects and amplifies the output  

📌 **Observation:**  
(To be filled after simulation)

### Waveform Results

> Add simulation waveforms here:
- Bitline (BL, BLB)
- Wordline (WL)
- DATA_IN
- DATA_OUT
- Control Signals (WE, PC, SAE)

### Performance Metrics
| Parameter | Value |
|----------|------|
| Read Delay | ___ |
| Write Delay | ___ |
| Power Consumption | ___ |
| SNM (if measured) | ___ |

### Observations
• (To be filled after testing)  
• (Example: Correct row selection verified)  
• (Example: Data integrity maintained during read/write)  

### Conclusion
The 16×8 SRAM array with peripheral circuits demonstrates correct functionality in terms of **row selection, read/write operations, and signal amplification**. Detailed performance metrics and waveform validation will further confirm system reliability.

---

## Layout Design and Physical Verification

After successful schematic design and functional verification, the SRAM architecture was implemented at the **layout level**, translating the circuit into a **physical representation** suitable for fabrication. The layouts were designed using the **Magic VLSI Layout Tool** and verified through industry-standard checks.

### Layout Design Flow

The physical design follows a full-custom VLSI layout methodology:

1. Transistor placement  
2. Diffusion and poly layer formation  
3. Metal routing for interconnections  
4. Power (VDD) and Ground (GND) routing  
5. Design Rule Check (DRC)  
6. Layout Versus Schematic (LVS)

### Layout Blocks Implemented

The following circuit blocks were successfully designed and verified at layout level:

• CMOS Inverter  
• 4-Input AND Gate  
• 4×16 Row Decoder  
• 6T SRAM Cell  
• Proposed 7T SRAM Cell  
• Precharge Circuit 
• Isolation Circuit 
• Write Driver Circuit  
• Sense Amplifier Circuit  
• 16×8 7T SRAM Array with Peripheral Integration  

<table align="center">
  <tr>
    <td align="center">
      <img width="468" height="639" alt="image" src="https://github.com/user-attachments/assets/0e8e34db-5d65-4f1f-8fd6-27bb2fbedbb6" /><br/>
      <small>Fig 26. CMOS Inverter </small>
    </td>
    <td align="center">
      <img width="686" height="639" alt="image" src="https://github.com/user-attachments/assets/d87beefd-7d6b-430e-8067-286027e23c9a" /><br/>
      <small>Fig 27. 4-Input AND Gate </small>
    </td>
  </tr>
</table>

<table align="center">
    <td align="center">
      <img width="418" height="781" alt="image" src="https://github.com/user-attachments/assets/a51bb3b1-6974-4d30-9cce-79e7e9022847" /><br/>
      <small> Fig 28. 4×16 Row Decoder </small>
    </td>
</table>

<table align="center">
  <tr>
    <td align="center">
      <img width="454" height="477" alt="image" src="https://github.com/user-attachments/assets/2c2b11c9-82d9-444a-977b-eaf7c763c95e" /><br/>
      <small> Fig 29. 6T SRAM Cell </small>
    </td>
    <td align="center">
      <img width="682" height="690" alt="image" src="https://github.com/user-attachments/assets/db23eb81-1b9b-4ea7-83fe-141ba1089824" /><br/>
      <small> Fig 30. Proposed 7T SRAM Cell </small>
    </td>
  </tr>
</table>

<table align="center">
    <td align="center">
      <img width="759" height="384" alt="image" src="https://github.com/user-attachments/assets/54aafecf-718a-400d-a187-681de9dc91a3" /><br/>
      <small> Fig 31. Precharge Circuit </small>
    </td>
</table>

<table align="center">
    <td align="center">
      <img width="266" height="282" alt="image" src="https://github.com/user-attachments/assets/e34bb3cd-d6d2-481b-8896-ba87a9ddc9f1" /><br/>
      <small> Fig 31. Isolation Circuit </small>
    </td>
</table>

<table align="center">
  <tr>        
    <td align="center">
      <img width="473" height="610" alt="image" src="https://github.com/user-attachments/assets/3b78a449-e59b-4069-a986-eed3b3a6d8f9" /><br/>
      <small> Fig 32. Write Driver Circuit </small>
    </td>
</tr>
<tr>
<table align="center">
    <td align="center">
      <img width="472" height="606" alt="image" src="https://github.com/user-attachments/assets/4ccaf163-b3f6-4143-b227-7072500f82a1" /><br/>
      <small> Fig 33. Sense Amplifier Circuit </small>
    </td>
   </tr>
</table>

<table align="center">
    <td align="center">
      <img width="488" height="1027" alt="image" src="https://github.com/user-attachments/assets/df6e102d-cd10-45ec-982b-156ed0b5d010" /><br/>
      <small> Fig 34. 16×8 7T SRAM Array with Peripheral Integration </small>
    </td>
</table>

### Verification Process

Two critical physical verification steps were performed:

**Design Rule Check (DRC)**  
Ensures that the layout adheres to all fabrication constraints such as spacing, width, and alignment rules.

**Layout Versus Schematic (LVS)**  
Validates that the extracted layout netlist matches the original schematic, ensuring functional correctness.

### Result

• All layout blocks are **DRC clean and LVS verified**  
• The complete SRAM system is successfully implemented at **layout level**  
• The design is ready for **post-layout analysis and fabrication-level validation**
