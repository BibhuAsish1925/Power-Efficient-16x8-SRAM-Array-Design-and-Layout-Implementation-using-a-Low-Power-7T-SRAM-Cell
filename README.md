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
---

## Problem Statement

Conventional **6T SRAM cells** are widely used because of their compact structure and fast access speed. However, continuous CMOS scaling introduces several challenges that reduce memory reliability and power efficiency.

During the **read operation**, the internal storage node is directly connected to the bitline through the access transistor, which can disturb the stored data and reduce the **Static Noise Margin (SNM)**. This can lead to instability under low-power operation.

Another major issue is **subthreshold leakage power**. As transistor dimensions shrink, leakage current increases significantly, causing higher standby power consumption in large SRAM arrays.

The main limitations of conventional 6T SRAM include:

- Reduced read stability  
- Lower SNM  
- Increased leakage current  
- Sensitivity to process variations  
- Higher standby power  

To overcome these limitations, this project proposes a **7T SRAM cell** with an additional transistor in the pull-down path to improve stability and reduce leakage power. The design is implemented as a **16×8 SRAM array** and compared with the conventional 6T SRAM cell.

---

## Key Features

- Design of **6T and proposed 7T SRAM cells**
- Implementation of a **16×8 SRAM array**
- Integration of peripheral circuits:
  - 4×16 Row Decoder  
  - Precharge Circuit  
  - Write Driver  
  - Isolation Circuit  
  - Sense Amplifier  
- Functional **read/write verification**
- **Power, delay, and SNM analysis**
- Schematic and **layout implementation** of major circuit blocks

---

## SRAM Architecture

The complete SRAM system consists of the following blocks:

- **SRAM Cell Array** – stores the data bits  
- **Row Decoder** – selects the required wordline  
- **Precharge Circuit** – precharges bitlines before read  
- **Write Driver** – applies data during write  
- **Isolation Circuit** – separates the sensing path during write  
- **Sense Amplifier** – amplifies the bitline voltage difference  

<table align="center">
    <td align="center">
      <img width="713" height="768" alt="image" src="https://github.com/user-attachments/assets/2ec21fdf-920f-4319-856b-823be1f23959" /><br/>
      <small> Fig. 1 SRAM system architecture
    </td>
</table>
         
---
---

## Conventional 6T SRAM Cell

The conventional **6T SRAM cell** stores one bit using **two cross-coupled CMOS inverters** and **two access transistors** controlled by the wordline.

### Structure

The cell consists of:

- 2 PMOS pull-up transistors  
- 2 NMOS pull-down transistors  
- 2 NMOS access transistors  

The cross-coupled inverters maintain the stored data, while the access transistors connect the cell to **BL** and **BLB** during read and write operations.

<table align="center">
  <tr>
    <td align="center">
      <img width="856" height="287" alt="Circuit Diagram" src="https://github.com/user-attachments/assets/cb2249a1-6b24-49d3-a24f-0ce22a17b51c"/><br/>
      <small>Fig 2a. 6T-SRAM schematic diagram</small>
    </td>
    <td align="center">
      <img width="2717" height="1500" alt="6T Schematic design" src="https://github.com/user-attachments/assets/9feed759-f637-410c-9dab-cf5765d4225b" /><br/>
      <small>Fig 2b. 6T-SRAM schematic design</small>
    </td>
     <td align="center">
      <img width="1366" height="1500" alt="6T SRAM-1 (2)" src="https://github.com/user-attachments/assets/42ded671-19c0-49a1-a33d-91562fca2b0f" /><br/>
      <small>Fig 2c. 6T-SRAM layout</small>
    </td>
  </tr>
</table>

### Main Nodes

- **Q** – stored data  
- **QB** – complementary data  
- **BL / BLB** – differential bitlines  
- **WL** – wordline  

### Basic Operation

**Hold Operation**  
When **WL = 0**, the cell is isolated from the bitlines and the stored data is maintained by positive feedback.

**Write Operation**  
When **WL = 1**, the write driver forces **BL** and **BLB**, updating the stored data.

**Read Operation**  
The bitlines are first precharged to **VDD**. When **WL = 1**, one bitline discharges slightly depending on the stored value, and the sense amplifier detects the voltage difference.

### Limitations of 6T SRAM

The conventional 6T SRAM suffers from:

- Read disturb  
- Reduced SNM  
- Higher leakage current  
- Process variation sensitivity  
- Increased power consumption  

These limitations motivate the use of an improved **7T SRAM architecture** for better stability and lower power.

---
---

## Transistor Sizing Analysis

Proper transistor sizing is essential for reliable SRAM operation. The dimensions of the pull-up, pull-down, and access transistors directly affect **read stability, write ability, and power consumption**. The sizing conditions are determined using **MOSFET current equations** and standard SRAM design ratios.

<table align="center">
    <td align="center">
      <img width="436" height="427" alt="image" src="https://github.com/user-attachments/assets/dee6b9d9-5e17-46ac-90cd-304a92619962" /><br/>
      <small>Fig 3. SRAM sizing</small>
    </td>
</table>

---

### MOSFET Saturation Current Equation

The drain current in saturation is given by:

$$
I_D = \frac{1}{2}\mu C_{ox}\left(\frac{W}{L}\right)(V_{GS}-V_T)^2
$$

The transistor strength parameter is:

$$
\beta = \mu C_{ox}\left(\frac{W}{L}\right)
$$

---

### Read Stability Condition

During read operation:
1. Bitlines are precharged to VDD
2. Wordline becomes WL = 1

If stored value is Q = 0, QB = 1. Then BL tries to pull node Q upward through the access transistor. And this can accidentally flip the stored value. To prevent this `Pull−down strength > Access strength`

$$
\beta_{PD} > \beta_{AX}
$$

The **Cell Ratio (CR)** is defined as:

$$
CR = \frac{(W/L)_{pull-down}}{(W/L)_{access}}
$$

Typical requirement:

$$
CR \geq 1.5
$$

This prevents the stored logic ‘0’ from being disturbed during read.

---

### Write Ability Condition

During write operation, we must force the cell to flip.

Example: Old data = 1 --> New data = 0
The bitline must override the pull-up PMOS. Thus `Access strength > Pull−up strength`

$$
\beta_{AX} > \beta_{PU}
$$

The **Pull-up Ratio (PR)** is:

$$
PR = \frac{(W/L)_{access}}{(W/L)_{pull-up}}
$$

Typical requirement:

$$
PR \geq 1
$$

This ensures that new data can overwrite the previous state.

---

### Transistor Width Configuration

<table align="center">
    <td align="center">
          <img width="941" height="521" alt="image" src="https://github.com/user-attachments/assets/5de5035b-d497-4670-bde7-b527375591dc" /><br/>
      <small>Fig 4. 6T-SRAM schematic design (same as 2b)</small>
    </td>
</table>

### Summary of Sizing Constraints

| Transistor | Function | Width (W) |
|-----------|----------|----------|
| Pull-Up PMOS (P1, P2) | Maintain stored value | 400nm (Wpu)|
| Access NMOS (N3, N4) | Connect cell to bitlines | 600nm (Wa = 1.5 x Wpu) |
| Pull-Down NMOS (N1, N2) | Strong discharge during read | 1.2um (Wpd = 2 x Wa)|

---
---

## Proposed 7T SRAM Cell Architecture

To improve the performance of the conventional 6T SRAM cell, an additional NMOS transistor is introduced in the pull-down path, forming the **7T SRAM cell**.

### Structure of 7T SRAM Cell

The proposed cell consists of:

- 2 Pull-up PMOS transistors  
- 2 Pull-down NMOS transistors  
- 2 Access NMOS transistors  
- 1 Additional bottom NMOS transistor (**1.2 µm**)  

<table>
  <tr>
    <td align="center">
          <img width="941" height="521" alt="image" src="https://github.com/user-attachments/assets/5e3f31bb-4502-4a97-a01a-9976061786c7" /><br/>
      <small>Fig 5a. Proposed 7T-SRAM schematic diagram</small>
    </td>
    <td align="center">
          <img width="2093" height="1500" alt="7T Schematic design" src="https://github.com/user-attachments/assets/869a598a-bbaa-4a3a-b8a6-bf68f16b356d" /><br/>
      <small>Fig 5b. Proposed 7T-SRAM schematic design</small>
    </td>
     <td align="center">
          <img width="1151" height="1500" alt="7T SRAM cell layout" src="https://github.com/user-attachments/assets/7646e9a4-ccd3-4989-9ea6-624dd62961e4" /><br/>
      <small>Fig 5b. Proposed 7T-SRAM schematic design</small>
    </td>
  </tr>
</table>

The transistor sizing of the original 6T cell is retained, while the added bottom transistor improves stability by controlling the discharge path.

### Function of Additional Transistor

The extra transistor acts as a **current control device** and helps in:

- Reducing leakage current  
- Improving read stability  
- Limiting unwanted discharge  
- Enhancing low-power performance  

### Operation of 7T SRAM Cell

**Hold Operation**  
When **WL = 0**, the cell remains isolated and the stored data is retained by the cross-coupled inverters.

**Write Operation**  
When **WL = 1**, the bitline data overwrites the stored node while the additional transistor controls current flow.

**Read Operation**  
After precharge, one bitline discharges slightly depending on the stored data, and the sense amplifier detects the differential voltage.

### Advantages of the 7T SRAM Cell

- Improved **SNM**
- Lower **leakage power**
- Better **read stability**
- Reduced **power consumption**

### Design Trade-off

The additional transistor slightly increases the cell area, but the improvement in **stability and power efficiency** makes the 7T cell more suitable for low-power SRAM applications.

---
---

## Power Analysis

Power consumption is an important design parameter in SRAM circuits, especially for low-power applications. The power performance of both **6T and 7T SRAM cells** is evaluated using simulation in **Cadence Virtuoso**.

### Average Power Equation

The average power is calculated as:

$$
P_{avg}=V_{DD}\times I_{avg}
$$

where:

- $V_{DD}$ = supply voltage  
- $I_{avg}$ = average supply current  

<table align="center">
  <tr>
    <td align="center">
          <img width="1029" height="800" alt="6T-SRAM VTC curve" src="https://github.com/user-attachments/assets/c3721968-3fc7-4e52-8e0a-c206ae93c62a" /><br/>
      <small>Fig 6a. 6T-SRAM VTC curve</small>
    </td>
    <td align="center">
          <img width="1006" height="800" alt="7T-SRAM VTC curve (2)" src="https://github.com/user-attachments/assets/e914d85d-c8d4-44e4-8451-588d62d2290b" /><br/>
      <small>Fig 6b. 7T-SRAM VTC curve</small>
    </td>
  </tr>
</table>

### Simulation Conditions

- **Technology:** 180 nm CMOS  
- **Supply Voltage:** 1.8 V  

### Power Results

| SRAM Type | Supply Voltage | Average Current | Average Power |
|-----------|---------------|---------------|---------------|
| 6T SRAM | 1.8 V | 507.5 nA | 0.9135 µW |
| 7T SRAM | 1.8 V | 353.4 nA | 0.63612 µW |

### Observation

The proposed **7T SRAM cell** shows lower current consumption and achieves nearly **30.36% reduction in power**, mainly due to the additional transistor that limits unwanted current flow.

---

## Static Noise Margin (SNM) Analysis

Static Noise Margin (SNM) indicates the ability of the SRAM cell to retain data in the presence of noise. It is obtained using the **butterfly curve method**.

<table align="center">
    <td align="center">
          <img width="503" height="432" alt="image" src="https://github.com/user-attachments/assets/1a94eb25-2291-447c-8f1f-d7217f17423f" /><br/>
      <small>Fig 7. SRAM butterfly curve</small>
    </td>
</table>

SNM is typically analyzed using the **butterfly curve method**, which is obtained by plotting the voltage transfer characteristics of the two cross-coupled inverters.

<table align="center">
  <tr>
    <td align="center">
          <img width="668" height="645" alt="image" src="https://github.com/user-attachments/assets/756c6e8a-97e5-4fb2-9466-85f82b8ca65f" /><br/>
      <small>Fig 7a. 6T-SRAM Butterfly curve</small>
    </td>
    <td align="center">
          <img width="657" height="645" alt="image" src="https://github.com/user-attachments/assets/572741f3-3639-4bda-9898-aebe3e0e46b8" /><br/>
      <small>Fig 7b. 7T-SRAM Butterfly curve</small>
    </td>
  </tr>
</table>

### SNM Equation

$$
SNM=\min(SNM_H,SNM_L)
$$

### SNM Results

| SRAM Type | SNM_L | SNM_H | SNM = min(SNM_L,SNM_H) |
|-----------|------|------|------|
| 6T SRAM | 692.53 mV | 674.375 mV | 674.375 mV |
| 7T SRAM | 850.2 mV | 849.6 mV | 849.6 mV |

### Observation

The proposed **7T SRAM cell** improves SNM by approximately **25.98%**, providing better read stability and stronger noise immunity.

---

## Delay Analysis

Delay analysis is performed for both **read** and **write** operations to compare speed performance.

### Delay Results

| Parameter | Write – 6T (ps) | Write – 7T (ps) | Read – 6T (ps) | Read – 7T (ps) |
|----------|----------------|----------------|---------------|---------------|
| Rise     | 308.594         | 298.378        | 39.746       | 41.195       |
| Fall     | 241.122         | 232.655        | 71.504       | 70.832        |
| Average  | 274.862         | 265.516        | 55.624        | 56.009       |

### Observation

- **Write delay improves by 3.4%**
- **Read delay increases slightly by 0.69%**

The small read delay increase is acceptable considering the improvement in stability and power reduction.

---

## Comparison Between 6T and 7T SRAM

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

- Improved **stability**
- Lower **power consumption**
- Reduced **leakage current**
- Slight increase in **cell area**
- Minimal change in **read speed**

Overall, the proposed **7T SRAM cell** provides a better balance of **power, stability, and performance** for low-power memory applications.

---
---

## Functional Verification of 7T SRAM Cell

Transient simulations were performed to verify the **hold, write, and read operations** of the proposed **7T SRAM cell**.

### Hold Operation

During hold mode, the cell retains its stored data without accessing the bitlines.

**Condition:** `WE = 0, WL = 0`

- Access transistors remain OFF  
- Cell is isolated from BL and BLB  
- Cross-coupled inverters maintain stored data  

<table align="center">
  <tr>
    <td align="center">
          <img width="1393" height="609" alt="hold test setup (wl=0)" src="https://github.com/user-attachments/assets/65f9b2de-6392-4c87-bb03-13b24d612a3c" /><br/>
      <small>Fig 8a. 7T-SRAM cell Hold test circuit</small>
    </td>
    <td align="center">
          <img width="1807" height="700" alt="7T-SRAM Hold test waveform" src="https://github.com/user-attachments/assets/4fca37aa-43cf-4632-9448-60486f4ef906" /><br/>
      <small>Fig 8b. 7T-SRAM cell Hold test waveform</small>
    </td>
  </tr>
</table>

---

### Write Operation

During write mode, the input data is applied to the bitlines and stored in the cell.

**Condition:** `WE = 1, WL = 1`

- Write driver generates complementary bitlines  
- `BL = DATA`
- `BLB = DATA̅`
- Access transistors turn ON  
- Internal nodes update to new logic state  

<table align="center">
  <tr>
    <td align="center">
          <img width="711" height="477" alt="image" src="https://github.com/user-attachments/assets/1658c19f-ef3f-4bc9-a83e-565525990bb7" /><br/>
      <small>Fig 9a. 7T-SRAM cell Write test circuit</small>
    </td>
    <td align="center">
          <img width="1280" height="700" alt="7T-SRAM Write test waveform" src="https://github.com/user-attachments/assets/d74fa5f6-499a-4644-9945-a3d566e41a80" /><br/>
      <small>Fig 9b. 7T-SRAM cell Write test waveform</small>
    </td>
  </tr>
</table>

**Result:** The SRAM cell correctly stores the applied input data.

---

### Read Operation

During read mode, the stored data is sensed from the bitlines.

**Condition:** `WE = 0, WL = 1`

- BL and BLB are precharged to **VDD**
- Wordline activates access transistors  
- One bitline discharges slightly  
- Sense amplifier detects the voltage difference  

<table align="center">
  <tr>
    <td align="center">
          <img width="711" height="482" alt="image" src="https://github.com/user-attachments/assets/f06020e2-8531-4afe-9d46-67f7e45fa458" /><br/>
      <small>Fig 10a. 7T-SRAM cell Read test circuit</small>
    </td>
    <td align="center">
          <img width="1280" height="700" alt="7T-SRAM Read test waveform" src="https://github.com/user-attachments/assets/0af78cb0-71fc-42fe-b1d7-c93be99107e5" /><br/>
      <small>Fig 10b. 7T-SRAM cell Read test waveform</small>
    </td>
  </tr>
</table>

**Result:** The stored data is read correctly without disturbing the cell.

---

### Subthreshold Leakage Effect During Read

A small leakage current flows through MOS transistors even below threshold voltage:

$$
I_{sub}\approx I_0 e^{\frac{V_{GS}-V_{TH}}{nV_T}}
$$

The additional transistor in the 7T cell helps:

- Reduce leakage current  
- Improve read stability  
- Minimize read disturb  

---

### Verification Summary

The simulation confirms:

- Stable data retention in hold mode  
- Correct write operation  
- Reliable read operation  
- Improved leakage control  
- Better overall stability  

## Conclusion

The proposed **7T SRAM cell** provides improved performance over the conventional **6T SRAM**.

- **Higher SNM**
- **Lower power consumption**
- **Reduced leakage**
- **Improved write delay**
- **Minimal read delay increase**

Overall, the proposed design offers a better balance of **power, stability, and performance** for low-power SRAM applications.

---
---

## Peripheral Circuits of the SRAM Array and Integration

The proposed **16×8 SRAM array** uses several peripheral circuits to ensure reliable addressing, writing, and sensing operations. Each circuit is implemented at both the **schematic and layout level** to verify complete physical realization of the memory system.

The main peripheral blocks are:

- Inverter  
- 4-Input AND Gate  
- 4×16 Row Decoder  
- Precharge Circuit  
- Write Driver  
- Sense Amplifier  
- Isolation Circuit
- 16x8 7T-SRAM array
- 16x8 7T-SRAM array with all Peripheral circuits integarted

---

### 1. Inverter Circuit

The CMOS inverter is used to generate complementary control signals required in the SRAM system. It consists of one PMOS and one NMOS transistor connected in a pull-up and pull-down configuration.

The inverter is mainly used for generating signals such as:

- **WE → WEB**
- **SAE → ISO**

For proper switching, the transistor sizes are chosen as:

- **NMOS = 400 nm**
- **PMOS = 800 nm**

<table align="center">
  <tr>
    <td align="center">
          <img width="228" height="221" alt="image" src="https://github.com/user-attachments/assets/437a132f-a122-4d02-b0f0-dd2a675cef49" /><br/>
      <small>Fig 11a. Inverter diagram</small>
    </td>
    <td align="center">
          <img width="893" height="800" alt="Inverter schematic design" src="https://github.com/user-attachments/assets/ec1b5b85-29db-49a9-87ac-678793c0f061" /><br/>
      <small>Fig 11b. Inverter schematic design</small>
    </td>
     <td align="center">
          <img width="358" height="800" alt="inverter circuit layout" src="https://github.com/user-attachments/assets/6ae8a74f-9a78-416c-86d4-3218fbb6d1ac" /><br/>
      <small>Fig 11c. Inverter layout</small>
    </td>
  </tr>
</table>

---

### 2. 4-Input AND Gate

The 4-input AND gate is used in the row decoding logic to generate a HIGH output for one specific address combination.

The logic is implemented using:

- NAND structure transistors:
  - **NMOS = 400 nm**
  - **PMOS = 800 nm**
- Output inverter transistors:
  - **NMOS = 600 nm**
  - **PMOS = 1.2 µm**

The larger inverter sizing improves the drive strength required for highly capacitive wordlines.

<table align="center">
  <tr>
    <td align="center">
          <img width="912" height="586" alt="4 Input AND gate" src="https://github.com/user-attachments/assets/158adc80-37d5-4e89-9faa-ad34ae2c8b5f" /><br/>
      <small>Fig 12a. 4-input AND gate diagram</small>
    </td>
    <td align="center">
          <img width="1263" height="900" alt="4-input AND gate schematic" src="https://github.com/user-attachments/assets/b5e39fc0-47dc-497a-a79a-2ff234eb69ca" /><br/>
      <small>Fig 12b. 4-input AND gate schematic design</small>
    </td>
     <td align="center">
          <img width="578" height="900" alt="4-input AND gate layout" src="https://github.com/user-attachments/assets/1e6e6bd3-2122-41e4-adac-0ad82e1e3a7f" /><br/>
      <small>Fig 12c. 4-input AND gate layout</small>
    </td>
  </tr>
</table>

<table align="center">
    <td align="center">
          <img width="1910" height="811" alt="and4" src="https://github.com/user-attachments/assets/bd5933e3-98d9-4278-a96e-e92a6c95e007" /><br/>
      <small>Fig 12d. 4-input AND gate output waveform</small>
    </td>
</table>

---

### 3. 4×16 Row Decoder

The row decoder converts a **4-bit address input** into **16 wordlines**, ensuring only one row is selected at a time.

Its operation includes:

- Address inversion using CMOS inverters  
- Logic generation using 4-input AND gates  
- One-hot wordline selection for the SRAM array  

Proper decoder design improves access reliability and prevents row conflicts.

<table align="center">
  <tr>
    <td align="center">
          <img width="465" height="705" alt="image" src="https://github.com/user-attachments/assets/9225a0df-9bcb-46ed-8007-c81e58f94bdf" /><br/>
      <small>Fig 13a. 4×16 Row decoder diagram</small>
    </td>
    <td align="center">
          <img width="467" height="1600" alt="4×16 Row decoder schematic (2)" src="https://github.com/user-attachments/assets/a402583f-6e09-40cb-bd4d-5b5796beaf36" /><br/>
      <small>Fig 13b. 4×16 Row decoder schematic design</small>
    </td>
     <td align="center">
          <img width="559" height="1600" alt="4×16 Row decoder layout" src="https://github.com/user-attachments/assets/ff52dd08-955f-4915-90f9-8fd482b83b7f" /><br/>
      <small>Fig 13c. 4×16 Row decoder layout</small>
    </td>
  </tr>
</table>

<table align="center">
    <td align="center">
          <img width="1052" height="434" alt="image" src="https://github.com/user-attachments/assets/8c367f36-a6ef-43ed-9ba5-62d8d7e8c430" /><br/>
      <small>Fig 13d. 4×16 Row decoder output waveform</small>
    </td>
</table>

---

### 4. Precharge Circuit

The precharge circuit initializes both bitlines before every read operation.

Its operation is:

- **PC = 0:** PMOS transistors turn ON and charge BL and BLB to VDD  
- **PC = 1:** PMOS transistors turn OFF and release the bitlines for sensing  

Transistor sizing:

- Side PMOS transistors = **1.2 µm**
- Equalization PMOS transistor = **800 nm**

This sizing provides faster charging of the highly capacitive bitlines.

<table align="center">
  <tr>
    <td align="center">
          <img width="349" height="287" alt="image" src="https://github.com/user-attachments/assets/bd585699-d465-4ddf-9acc-7d1f204d292a" /><br/>
      <small>Fig 14a. Precharge cell diagram</small>
    </td>
    <td align="center">
          <img width="1506" height="900" alt="Precharge cell schematic" src="https://github.com/user-attachments/assets/6763e8a7-ec3a-4fda-b691-117d79a0a5e7" /><br/>
      <small>Fig 14b. Precharge cell schematic design</small>
    </td>
  </tr>
</table>

<table align="center">
    <td align="center">
          <img width="825" height="389" alt="image" src="https://github.com/user-attachments/assets/ea729828-24f7-425c-9053-798ae6c84ec9" /><br/>
      <small>Fig 14c. Precharge cell output waveform</small>
    </td>
</table>
<table align="center">
<td align="center">
          <img width="1586" height="900" alt="Precharge cell layout" src="https://github.com/user-attachments/assets/ff3795fb-7cea-4ce7-b770-78f31172b25e" /><br/>
      <small>Fig 14d. Precharge cell layout</small>
    </td>
</table>
<table align="center">
    <td align="center">
          <img width="1601" height="339" alt="1x8 pc" src="https://github.com/user-attachments/assets/fefb300d-bf68-4065-8ad3-b4e9f5139a47" /><br/>
      <small>Fig 14e. 1x8 Precharge cell setup </small>
    </td>
</table>

---

### 5. Write Driver

The write driver forces input data onto the bitlines during the write cycle.

Its operation includes:

- Generating complementary outputs:
  - **BL**
  - **BLB**
- Driving large bitline capacitances
- Overwriting stored data in the selected SRAM cell

Because BL and BLB are highly capacitive, stronger transistors are used for reliable writing.

<table align="center">
  <tr>
    <td align="center">
          <img width="452" height="239" alt="image" src="https://github.com/user-attachments/assets/f782c731-c55e-4025-86aa-95b001a867a5" /><br/>
      <small>Fig 15a. Write Driver diagram</small>
    </td>
    <td align="center">
          <img width="1623" height="1200" alt="Write Driver schematic design" src="https://github.com/user-attachments/assets/9748ec46-90bc-44e5-ab87-b6148adcd6ab" /><br/>
      <small>Fig 15b. Write Driver schematic design</small>
    </td>
  </tr>
</table>

<table align="center">
    <td align="center">
          <img width="917" height="354" alt="image" src="https://github.com/user-attachments/assets/677995fa-b9e2-4d46-83ae-4dbca3e97681" /><br/>
      <small>Fig 15c. Write Driver output waveform</small>
    </td>
</table>
<table align="center">
<td align="center">
          <img width="568" height="1217" alt="Write Driver" src="https://github.com/user-attachments/assets/df176d4a-4bcd-4552-bd8c-0f84dbeb7e18" /><br/>
      <small>Fig 15d. Write Driver layout</small>
    </td>
</table>
<table align="center">
    <td align="center">
          <img width="1601" height="559" alt="1x8 write driver" src="https://github.com/user-attachments/assets/b1decd3f-5bc2-443d-a6a4-7d2528dd7770" /><br/>
      <small>Fig 15e. 1x8 Write Driver setup </small>
    </td>
</table>

---

### 6. Sense Amplifier

The sense amplifier detects the small voltage difference between BL and BLB during read operation and converts it into a full digital output.

Its function includes:

- Differential sensing
- Fast signal amplification
- Improved read reliability

Careful transistor matching is required to minimize offset errors and improve sensing accuracy.

<table align="center">
   <tr>
    <td align="center">
          <img width="1180" height="843" alt="Sense Amplifier" src="https://github.com/user-attachments/assets/a2403e61-eca2-4947-9757-82063156012b" /><br/>
      <small>Fig 16a. Sense Amplifier diagram</small>
    </td>
   <td align="center">
          <img width="2188" height="1200" alt="Sense Amplifier schematic design" src="https://github.com/user-attachments/assets/dda274c3-ccf2-4a0c-9517-210198c5bdb1" /><br/>
      <small>Fig 16b. Sense Amplifier schematic design</small>
    </td>
      </tr>
</table>

<table align="center">
    <td align="center">
          <img width="818" height="308" alt="image" src="https://github.com/user-attachments/assets/f6b9e495-bc87-45f1-b288-0493369e10cf" /><br/>
      <small>Fig 16c. Sense Amplifier output waveform</small>
    </td>
</table>
<table align="center">
   <td align="center">
          <img width="569" height="1241" alt="Sense Amplifier" src="https://github.com/user-attachments/assets/572efdd4-b815-45f1-82d8-edece9d9c2f2" /><br/>
      <small>Fig 16d. Sense Amplifier layout</small>
    </td>
</table>
<table align="center">
    <td align="center">
          <img width="1601" height="559" alt="1x8 Sense amplifier" src="https://github.com/user-attachments/assets/af02fab6-112d-48dd-9011-57702f34670e" /><br/>
      <small>Fig 16e. 1x8 Sense Amplifier setup </small>
    </td>
</table>

---

### 7. Isolation Circuit

The isolation circuit controls the connection between the bitlines and the sense amplifier.

Its operation is:

- **ISO = HIGH:** disconnects sense amplifier during write
- **ISO = LOW:** connects sense amplifier during read

This prevents unwanted loading of the bitlines and improves system stability.

Larger transistor sizing is used because the circuit directly drives capacitive bitline nodes.

<table align="center">
   <tr>
    <td align="center">
          <img width="805" height="822" alt="Isolation cell" src="https://github.com/user-attachments/assets/e3771aa6-a2bf-4386-9930-acf5a225f4f7" /><br/>
      <small>Fig 17a. Isolation Circuit diagram</small>
    </td>
   <td align="center">
          <img width="1090" height="700" alt="Isolation Circuit schematic" src="https://github.com/user-attachments/assets/f1058ff8-8a98-4ef0-85cd-72af32e1dc17" /><br/>
      <small>Fig 17b. Isolation Circuit schematic design</small>
    </td>
      </tr>
</table>

<table align="center">
    <td align="center">
          <img width="1590" height="631" alt="Isolation" src="https://github.com/user-attachments/assets/620e0228-c96a-4b16-b136-43a58d5ef2ea" /><br/>
      <small>Fig 17c. Isolation Circuit output waveform</small>
    </td>
</table>
<table align="center">
   <td align="center">
          <img width="1390" height="700" alt="Isolation Circuit layout" src="https://github.com/user-attachments/assets/75c3e48b-2448-44f7-a50d-fa2c29dead35" /><br/>
      <small>Fig 17d. Isolation Circuit layout</small>
    </td>
</table>
<table align="center">
    <td align="center">
          <img width="1601" height="237" alt="1x8 Isolation" src="https://github.com/user-attachments/assets/baf13008-6b68-414d-bc86-331655d3b4d3" /><br/>
      <small>Fig 17e. 1x8 Isolation Circuit setup </small>
    </td>
</table>

---

### 8. SRAM Array

The individual 7T SRAM cells are arranged into a **16×8 memory array**.

Array organization:

- **16 rows**
- **8 columns**
- Shared **wordlines**
- Shared **bitline pairs**

This arrangement allows structured data storage and retrieval while maintaining compact implementation.

<table align="center">
   <tr>
   <td align="center">
          <img width="763" height="1500" alt="16x8 7T SRAM Array" src="https://github.com/user-attachments/assets/40f7df68-6eb6-42f3-a9dc-0b85cb89babf" /><br/>
      <small>Fig 18a. 16x8 7T SRAM Array schematic design</small>
    </td>
   <td align="center">
          <img width="524" height="1500" alt="16x8 7T SRAM Array layout" src="https://github.com/user-attachments/assets/43abe6ac-0392-4fa5-90e0-74a33b387421" /><br/>
      <small>Fig 18b. 16x8 7T SRAM Array layout</small>
    </td>
      </tr>
</table>

---

### 9. System Integration

All peripheral blocks are integrated with the SRAM array to form the complete memory system.

System sequence:

1. Row decoder selects one wordline  
2. Precharge prepares bitlines  
3. Write driver stores input data  
4. Isolation controls sensing path  
5. Sense amplifier generates output data  

This integration ensures proper operation of the complete SRAM memory.

<table align="center">
   <tr>
      <td align="center">
          <img width="797" height="1800" alt="16x8 7T SRAM Array with all Peripheraral circuits integrated schematic design" src="https://github.com/user-attachments/assets/aa069191-b77d-44d6-8c04-9aef95218194" /><br/>
      <small>Fig 19a. 16x8 7T SRAM Array with all Peripheraral circuits integrated schematic design</small>
    </td>
   <td align="center">
          <img width="765" height="1800" alt="16x8 7T SRAM Array with all Peripheraral circuits integrated schematic block design" src="https://github.com/user-attachments/assets/d6c0618e-6973-462f-8680-ba1e665aeb63" /><br/>
      <small>Fig 19b. 16x8 7T SRAM Array with all Peripheraral circuits integrated schematic block design</small>
    </td>
   <td align="center">
          <img width="744" height="1800" alt="16x8 7T SRAM Array with all Peripheraral circuits integrated layout" src="https://github.com/user-attachments/assets/e8f88623-20f6-47ec-85eb-506e6a7bae57" /><br/>
      <small>Fig 19c. 16x8 7T SRAM Array with all Peripheraral circuits integrated layout </small>
    </td>
      </tr>
</table>

---
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
          <img width="832" height="1025" alt="Single-Bit 7T-SRAM Cell with Peripheral Circuits" src="https://github.com/user-attachments/assets/937fb704-54ff-4009-a999-21d7c1414ce4" /><br/>
      <small>Fig 20. Single-Bit 7T-SRAM Cell with Peripheral Circuits</small>
    </td>
</table>

<table align="center">
    <td align="center">
          <img width="1910" height="811" alt="Memory" src="https://github.com/user-attachments/assets/a7ca0667-651c-4f69-959d-99681bc8c669" /><br/>
      <small>Fig 20a. Single-Bit 7T-SRAM Cell with Peripheral Circuits output waveform</small>
    </td>
</table>

---

### Test Analysis

The peripheral circuits interact with the SRAM cell as follows:

1. **Precharge Circuit** - Before every read operation, the precharge circuit charges both bitlines to logic HIGH.

Condition: `PC = 0 → BL = 1 and BLB = 1, WE = 0, SAE = 1, ISO = 0`

This ensures both bitlines start from the same voltage level.

<table align="center">
    <td align="center">
          <img width="1910" height="811" alt="Memory_pc" src="https://github.com/user-attachments/assets/06273a96-3e02-4d59-96c0-ab9d9bb850f6" /><br/>
      <small>Fig 20b. Single-Bit 7T-SRAM Cell Precharge conditions</small>
    </td>
</table>

2. **Write Driver Operation**

The write driver applies input data to the bitlines during write operation.

Condition: `WE = 1 with BL = DATA, BLB = DATA̅`

This prepares the bitlines with the input data value.

<table align="center">
    <td align="center">
          <img width="1910" height="811" alt="Memory_we" src="https://github.com/user-attachments/assets/84947627-550b-4877-b07b-2813d0140802" /><br/>
      <small>Fig 20c. Single-Bit 7T-SRAM Cell Write Enable condition</small>
    </td>
</table>

3. **Write Operation**

When both write enable and wordline signals are active: `WE = 1, WL = 1, PC = 1, SAE = 0, ISO = 1`

The SRAM cell captures the input data from the bitlines and stores it in the internal latch.

<table align="center">
    <td align="center">
          <img width="1910" height="811" alt="Memory_we_wl" src="https://github.com/user-attachments/assets/0c28dad2-0753-4f7c-ab38-75f39d4aebcd" /><br/>
      <small>Fig 20c. Single-Bit 7T-SRAM Cell Write conditions</small>
    </td>
</table> 

Result: `Q = DATA_IN`

4. **Read Operation**

For read operation: `WE = 0, WL = 1, PC = 1, SAE = 1, ISO = 0`

The SRAM cell connects to the bitlines and transfers the stored data. BL reflects the stored value of node Q.

<table align="center">
    <td align="center">
          <img width="1910" height="811" alt="Memory_web_wl" src="https://github.com/user-attachments/assets/e78add3e-1141-40f5-83d9-d8eba7130740" /><br/>
      <small>Fig 20d. Single-Bit 7T-SRAM Cell Read condition </small>
    </td>
</table> 

Output: `DATA_OUT = Stored SRAM value`

### Simulation Result

The transient waveform confirms that:

• The precharge circuit correctly charges the bitlines.  
• The write driver successfully writes input data into the SRAM cell.  
• The stored data remains stable inside the latch.  
• The isolation circuit successfully isolates write and read phase.  
• The read operation retrieves the stored value correctly.  
• The sense amplifier produces a clean digital output signal.

### Conclusion

The successful integration of the **7T SRAM cell with peripheral circuits** verifies the correct functionality of the proposed SRAM architecture. The simulation demonstrates reliable:

• Data write operation  
• Data retention  
• Data read operation

This validates the feasibility of implementing the **complete SRAM array using the proposed 7T SRAM cell design**.

---
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

---

## 16×8 7T SRAM Array Testing with Peripheral Circuits

The complete **16×8 7T SRAM array** was tested after integrating the row decoder, write driver, precharge circuit, isolation circuit, and sense amplifier to verify correct system-level operation.

### Test Setup

The integrated SRAM system consists of:

- Inverter
- 4×16 Row Decoder  
- Write Driver  
- Precharge Circuit  
- Isolation Circuit  
- Sense Amplifier  
- 16×8 7T SRAM Cell Array  

<table align="center">
    <td align="center">
          <img width="2315" height="1000" alt="image" src="https://github.com/user-attachments/assets/137f84b0-28bb-4a3c-8284-26b0ce754d65" /><br/>
      <small>Fig 21. Complete SRAM array testing setup </small>
    </td>
</table>

### Control Signals

The array operation is controlled using:

- **A[3:0]** – row address  
- **DATA_IN[7:0]** – input data  
- **WE / WEB** – write control (gives out **BL / BLB**)
- **PC** – precharge control  
- **ISO** – isolation control  
- **SAE** – sense amplifier enable  

---

<table align="center">
    <td align="center">
          <img width="1500" height="1026" alt="Complete SRAM array transient waveform" src="https://github.com/user-attachments/assets/4da7e501-93da-4fc5-9260-aadf60027a6f" /><br/>
      <small>Fig 21a. Complete SRAM array transient waveformy</small>
    </td>
</table>

---

### Precharge Phase

**Condition:** `WE = 0, PC = 0, WL = not required, SAE = 0, ISO = 1`

Before every read cycle:

- **PC = 0** turns ON the precharge transistors  
- Both **BL and BLB** are charged to **VDD**
- Equalization maintains identical bitline voltage  

This prepares the bitlines for accurate sensing.

---

### Write Operation

**Condition:** `WE = 1, PC = 1, WL = enable, SAE = 0, ISO = 1`

- The decoder activates the selected row  
- The write driver applies complementary data on **BL** and **BLB**
- The selected memory cells store the input data
- The isolation circuit disconnects the sense amplifier during write  

The waveform confirms that the selected row stores the applied data while the output remains inactive.

---

### Read Operation

**Condition:** `WE = 0, PC = 1, WL = enable, SAE = 1, ISO = 0`

- The selected wordline is enabled
- One bitline discharges slightly based on stored data
- The isolation circuit connects the bitlines to the sense amplifier
- The sense amplifier converts the small differential voltage into full output data  

The waveform shows correct retrieval of the stored data at the output.

---

### Waveform Observation

From the transient simulation waveforms, the following behavior is verified:

- Proper sequential row selection by the decoder  
- Correct bitline precharging before read  
- Successful 8-bit data writing into the selected row  
- Accurate data retrieval during read operation  
- Stable control of the isolation path during read and write  
- Correct output generation without read/write overlap  

**Figure:** Complete SRAM array transient waveform

### Conclusion

The waveform analysis confirms that the proposed **16×8 7T SRAM array** operates correctly with coordinated peripheral circuit action and reliable memory performance.

---
---

## Layout Design and Physical Verification

After schematic verification, the complete SRAM design was implemented at the **layout level** to obtain the physical structure required for fabrication. The layouts were developed using a **full-custom design approach**, and each block was verified for correctness.

### Layout Design Flow

The physical implementation includes:

1. Transistor placement  
2. Poly and diffusion formation  
3. Metal interconnection routing  
4. Power and ground routing  
5. Design Rule Check (DRC)  
6. Layout Versus Schematic (LVS)  

### Layout Blocks Implemented

The following blocks were completed at layout level:

- CMOS Inverter  
- 4-Input AND Gate  
- 4×16 Row Decoder  
- 6T SRAM Cell  
- Proposed 7T SRAM Cell  
- Precharge Circuit  
- Isolation Circuit  
- Write Driver  
- Sense Amplifier  
- 16×8 7T SRAM Array with Peripheral Integration  

### Layout Figures

- **Fig. 2c** – 6T SRAM Cell Layout
- **Fig. 5b** – Proposed 7T SRAM Cell Layout
- **Fig. 11c** – CMOS Inverter Layout  
- **Fig. 12c** – 4-Input AND Gate Layout  
- **Fig. 13c** – 4×16 Row Decoder Layout  
- **Fig. 14d** – Precharge Circuit Layout
- **Fig. 15d** – Write Driver Layout
- **Fig. 16d** – Sense Amplifier Layout
- **Fig. 17d** – Isolation Circuit Layout  
- **Fig. 18b** – Proposed 7T SRAM Cell Array Layout   
- **Fig. 19c** – 16×8 SRAM Array with Peripheral Layout  

### Physical Verification

Two verification steps were performed:

**DRC:**  
Confirms that the layout satisfies fabrication design rules.

**LVS:**  
Confirms that the extracted layout matches the original schematic.

### Result

- All layout blocks are **DRC clean**
- All circuits are **LVS verified**
- The complete SRAM system is physically validated for implementation
