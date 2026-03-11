# FSM-Based Digital Voting Machine (Verilog HDL on FPGA)

A hardware-based **Digital Voting Machine (DVM)** implemented using **Verilog HDL** and deployed on an FPGA platform.  
The system uses a **Finite State Machine (FSM)** to control the voting process, ensuring that only **one vote is counted per enable cycle** while preventing switch bounce and duplicate vote counting.

The design was simulated and tested on FPGA hardware to verify correct operation and reliable vote counting.

---

## Features

- FSM-based control logic
- Support for **3 candidates**
- **One vote per enable cycle**
- Debounce protection to avoid multiple counts
- Binary vote count display on FPGA LEDs
- Verified through simulation and hardware testing

---

## System Overview

The voting system operates using four FSM states:

| State | Description |
|------|-------------|
| Idle | System waits after reset until voting is enabled |
| Vote | Candidate inputs are monitored and votes are counted |
| Hold | Short delay prevents multiple counts from a single press |
| Finish | Voting stops and final counts remain displayed |

State transition flow:

`Idle → Vote → Hold → Vote → Finish`

---

## Inputs

| Signal | Description |
|------|-------------|
| `clk` | System clock |
| `rst` | Reset signal |
| `i_en` | Enable signal allowing a vote |
| `i_candidate_1` | Vote input for Candidate 1 |
| `i_candidate_2` | Vote input for Candidate 2 |
| `i_candidate_3` | Vote input for Candidate 3 |
| `i_voting_over` | Ends the voting session |

---

## Outputs

| Signal | Description |
|------|-------------|
| `o_count1[5:0]` | Vote count for Candidate 1 |
| `o_count2[5:0]` | Vote count for Candidate 2 |
| `o_count3[5:0]` | Vote count for Candidate 3 |

Vote totals are displayed in **binary format on FPGA LEDs**.

---

## Operation

1. Reset initializes the system and clears all counters.
2. Voting is enabled using the enable signal.
3. A voter selects one candidate switch.
4. The vote is counted for the selected candidate.
5. The system enters a short hold state to prevent multiple counts.
6. Voting continues until the **Voting Over** signal is activated.
7. Final vote counts remain displayed on the LEDs.

---

## Simulation and Testing

The design was verified using simulation and FPGA hardware testing.

Testing confirmed:

- Correct FSM transitions
- Accurate vote counting
- Reset functionality
- Prevention of multiple vote increments

---

## Possible Improvements

- Add **7-segment display output** for easier readability
- Integrate **RFID or biometric authentication**
- Store results in **non-volatile memory**
- Add **wireless result transmission**

---

## Technologies Used

- Verilog HDL  
- FPGA (Cyclone IV or similar)  
- Intel Quartus Prime  
- ModelSim
