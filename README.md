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
When the **wordline (WL) = 0**, the access transistors are OFF and the cell is isolated from the bitlines. The cross-coupled inverters maintain the stored value using positive feedback.

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

Proper transistor sizing is essential for stable SRAM operation. The sizing of pull-up, pull-down, and access transistors determines the **read stability, write ability, and overall reliability** of the memory cell. The sizing constraints are derived using **MOSFET current equations and Kirchhoff current relations**.

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

---

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

---

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
- 1 Additional Bottom NMOS transistor(w=1.2um)

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

SNM is typically analyzed using the **butterfly curve method**, which is obtained by plotting the voltage transfer characteristics of the two cross-coupled inverters.

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

## Comparison Between 6T and 7T SRAM

To evaluate the effectiveness of the proposed design, a comparison is performed between the conventional **6T SRAM cell** and the proposed **7T SRAM cell** based on important design parameters such as stability, power consumption, area, and delay.

| Parameter | 6T SRAM | 7T SRAM |
|-----------|--------|--------|
| Number of Transistors | 6 | 7 |
| Cell Stability | Moderate | Improved |
| Static Noise Margin (SNM) | 674.375 mV | 849.6 mV |
| Leakage Power | Higher | Reduced |
| Average Power Consumption | 0.9135 µW | 0.63612 µW |
| Area Utilization | Smaller | Slightly Larger |
| Write Delay | Faster | Slightly Higher due to extra transistor |
| Read Stability | Moderate | Higher |
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

---

### Write Operation

During the write operation, the data input is forced onto the bitlines through the write driver and stored in the SRAM cell.

Operation conditions: `WE = 1, WL = 1 ` 

Working principle:

• The write driver receives the input data signal (DATA_IN).  
• Complementary signals are driven onto the bitlines: `BL = DATA, BLB = DATA̅ ` 

• When the **wordline (WL)** becomes HIGH, the access transistors turn ON.  
• The internal storage nodes of the cross-coupled inverter latch are overwritten by the bitline values.

Result: The SRAM cell successfully captures the input data and stores it at the internal node **Q**.

---

### Read Operation

The read operation retrieves the stored data from the SRAM cell without intentionally modifying the stored value.

Operation conditions: `WE = 0, WL = 1` 

Working principle:

• Before the read operation, both **BL and BLB are precharged to VDD**.  
• When the wordline becomes HIGH, the access transistors connect the internal nodes to the bitlines.

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

## Peripheral Circuits of the SRAM Array

In addition to the SRAM cell array, several **supporting peripheral circuits** are required to perform reliable read and write operations. These circuits control the addressing, data transfer, and signal amplification within the memory system. The major peripheral circuits used in the proposed SRAM architecture are:

1. Row Decoder  
2. Precharge Circuit  
3. Write Driver  
4. Sense Amplifier

These circuits work together with the **16×8 SRAM array** to enable proper memory operation.

---

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

---

### 2. Precharge Circuit

The precharge circuit prepares the bitlines before every read operation.

#### Working Principle

• When **PC = 0**, the precharge transistors charge both **BL and BLB to VDD**.  
• The equalization transistor ensures both bitlines remain at the same voltage level.  
• This ensures accurate sensing during the read operation.

Precharging the bitlines reduces sensing delay and improves reliability of the memory read process.

---

### 3. Write Driver

The write driver circuit is responsible for forcing data onto the bitlines during write operations.

#### Working Principle

• The write driver receives **DATA_IN** from the input.  
• Based on the **Write Enable (WE)** signal, the driver sets the bitlines.

Operation:

• If **WE = 1**,  `BL = DATA, BLB = DATA̅  `
• When **WL = 1**, the SRAM cell captures the data from the bitlines and stores it internally.

This circuit ensures strong drive capability to overwrite the previously stored value inside the SRAM cell.

---

### 4. Sense Amplifier

The sense amplifier is used to detect and amplify the small voltage difference between the bitlines during read operation.

#### Working Principle

• During read operation, one bitline discharges slightly depending on the stored data.  
• This creates a small voltage difference between **BL and BLB**.  
• The sense amplifier detects this difference and amplifies it to produce a full digital output.

The output is then provided as **DATA_OUT**. Sense amplifiers significantly improve the **speed and reliability of read operations** in SRAM arrays.

---

### Integration with SRAM Array

In the complete system:

• The **Row Decoder** activates the required wordline.  
• The **Precharge Circuit** prepares the bitlines before reading.  
• The **Write Driver** writes data into the SRAM cell.  
• The **Sense Amplifier** reads and amplifies the stored data.

These peripheral circuits together enable the **efficient operation of the 16×8 SRAM array**.

---

## Single-Bit SRAM Cell Test with Peripheral Circuits

To validate the complete memory architecture, a **single-bit 7T SRAM cell** was integrated with all the required peripheral circuits and simulated. The test setup includes the following components:

• 7T SRAM Cell  
• Precharge Circuit  
• Write Driver  
• Sense Amplifier  
• Wordline Control  
• Data Input and Output Nodes

All circuits are connected to a common **VDD supply and Ground reference**.

---

### Test Architecture

The peripheral circuits interact with the SRAM cell as follows:

1. **Precharge Circuit** - Before every read operation, the precharge circuit charges both bitlines to logic HIGH.

Condition: `PC = 0 → BL = 1 and BLB = 1`

This ensures both bitlines start from the same voltage level.

---

2. **Write Driver Operation**

The write driver applies input data to the bitlines during write operation.

Condition: `WE = 1 with BL = DATA, BLB = DATA̅`

This prepares the bitlines with the input data value.

---

3. **Write Operation**

When both write enable and wordline signals are active: `WE = 1, WL = 1 `

The SRAM cell captures the input data from the bitlines and stores it in the internal latch.

Result: `Q = DATA_IN`

---

4. **Read Operation**

For read operation: `WE = 0, WL = 1`

The SRAM cell connects to the bitlines and transfers the stored data. BL reflects the stored value of node Q.

---

5. **Sense Amplifier Operation**

The sense amplifier detects the voltage difference between BL and BLB and amplifies it to generate a strong digital output signal.

Output: `DATA_OUT = Stored SRAM value`

---

### Simulation Result

The transient waveform confirms that:

• The precharge circuit correctly charges the bitlines.  
• The write driver successfully writes input data into the SRAM cell.  
• The stored data remains stable inside the latch.  
• The read operation retrieves the stored value correctly.  
• The sense amplifier produces a clean digital output signal.

---

### Conclusion

The successful integration of the **7T SRAM cell with peripheral circuits** verifies the correct functionality of the proposed SRAM architecture. The simulation demonstrates reliable:

• Data write operation  
• Data retention  
• Data read operation

This validates the feasibility of implementing the **complete SRAM array using the proposed 7T SRAM cell design**.

---

## Layout Design and Physical Verification (Work in Progress)

After validating the schematic-level functionality of the SRAM architecture, the next stage of the design flow involves **physical layout implementation and verification**. The layout stage converts the schematic design into a **geometrical representation of transistors, interconnections, and routing layers** suitable for fabrication. The layouts are designed using **Magic VLSI Layout Tool** and verified using **DRC and LVS checks**.

---

### Layout Design Flow

The layout implementation follows the standard VLSI physical design procedure:

1. Transistor placement  
2. Diffusion and poly layer formation  
3. Metal routing for signal connections  
4. Power and ground routing  
5. Design Rule Check (DRC)  
6. Layout Versus Schematic (LVS)

---

### Layout Blocks Designed So Far

The following circuits have been implemented at layout level:

• CMOS Inverter  
• 4-Input AND Gate  
• 4×16 Row Decoder

These blocks serve as the fundamental components for implementing the memory architecture.

---

### Verification Process

Two important verification steps are performed:

**Design Rule Check (DRC)**  
Ensures that the layout follows all manufacturing design rules.

**Layout Versus Schematic (LVS)**  
Confirms that the physical layout matches the original schematic design.

---

### Current Status

The layout implementation of the **basic logic blocks and row decoder** has been completed and verified successfully.

The layout design of the remaining blocks such as:

• SRAM Cell Array  
• Sense Amplifier  
• Write Driver  
• Precharge Circuit

is currently **under development and optimization**.

---

### Future Layout Work

Future work will include:

• Layout implementation of the **7T SRAM cell**  
• Integration of the **16×8 SRAM array**  
• Layout design of peripheral circuits  
• Post-layout simulation and parasitic analysis
