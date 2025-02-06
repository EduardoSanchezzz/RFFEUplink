# LTE RF Uplink
## Design and Analysis of LTE transceiver link using SystemVue simulation engine
- [LTE RF Uplink](#lte-rf-uplink)
  - [Design and Analysis of LTE transceiver link using SystemVue simulation engine](#design-and-analysis-of-lte-transceiver-link-using-systemvue-simulation-engine)
  - [Overview](#overview)
    - [Project Characteristics](#project-characteristics)
    - [System Requirements](#system-requirements)
  - [Base Station Receiver Design](#base-station-receiver-design)
    - [Front End Block Diagram](#front-end-block-diagram)
    - [Rx Characteristics](#rx-characteristics)
    - [Components](#components)
    - [Design](#design)
    - [Simulations](#simulations)

## Overview
This project involves modelling a LTE RF uplink using SystemVue simulation. This includes the design of the mobile device transmitter and base station receiver as well as modelling the uplink channel path loss.
### Project Characteristics
- **Operating Frequency:** 1.95 GHz
- **Channel Bandwidth:** 5 MHz
- **Duplex Model:** FDD
- **Link Distance:** 100m
- **Modulation Type:** 64 QAM
### System Requirements
- **EVM:** <6%
- **Rx Dynamic Range:** >40dB
- **Rx Sensitivity:** -70dBm

## Base Station Receiver Design
### Front End Block Diagram
![alt text](<Images/Rx Block Diagram.png>)
### Rx Characteristics
- **Rx Frequency:** 1.95 GHz
- **IF Frequency:** 100 MHz
- **IF Output Power:** -5 dBm
- **Antenna Noise Temperature:** 270K
  
### Components
- **Duplexor Filter**
  - 5th order Butterworth Band Pass Filter with Insertion Loss of 1dB
- **LNA** 
  - Design Variables: Noise Figure(NF), Gain, IIP3
- **Mixer** 
  - Design Variables: NF, Conversion Gain, IIP3
- **Voltage Controlled Oscillator(VCO)**
  - Design Variables: Phase noise
- **IF Variable Gain Amplifier(VGA)** 
  - AD8367 from Analog Devices
  - Parameters taken from datasheet
  - Design Variables: NF, Gain, IIP3

### Design
1. Initial System Model
     - Developed equations to relate individual component parameters (e.g., gain, noise figure, linearity) to overall receiver system requirements.
     - Derived relationships such as cascaded noise figure (using Friis' formula) and system gain to ensure the design met key performance metrics like sensitivity and dynamic range.
2. Optimizing FOM using MATLAB
   - Introduced FOM equations to increase practicality of component design
   - Utilized MATLAB optimization functions to determine component parameters that meet system requirements while minimizing FOM
3. Final Simulations in SystemVue
   - Simulated Rx performance in SystemVue and tuned parameters to meet requirements
   - Validated design meets system requirements

### Simulations
**Rx Output at min sensitivity**
*Pin = -70dBm*

*Measurements*
- **Output Power:** -4.84 dBm
- **EVM:** 4.683%
- **ACPR:** 31.56dB
- **PAPR:** 7.053dB
  
*Constellation*
![alt text](Images/RxOnlyMinPConstellation.png)
*Spectrum*
![alt text](Images/RxOnlyMinPSpectrum.png)

**Rx Output at high end of dynamic range**
*Pin = -30dBm*

*Measurements*
- **Output Power:** -0.684 dBm
- **EVM:** 3.385%
- **ACPR:** 37.42dB
- **PAPR:** 5.472dB
  
*Constellation*
![alt text](Images/RxOnlyMaxPConstellation.png)
*Spectrum*
![alt text](Images/RxOnlyMaxPSpectrum.png)
