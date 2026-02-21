# LED Light Regulator (Linear Constant Current Driver)

## Project Overview
This project presents the design and implementation of a **linear LED light regulator** intended for driving high‑power LEDs using a **constant current topology**. The system was developed as a final engineering project and includes:

- Electrical design of LED voltage and current regulation
- Implementation of a linear regulator used as a constant current driver
- Thermal considerations for power dissipation
- Parallel LED branch configuration
- Custom designed 3D printed enclosure
- Passive airflow cooling

The goal of the system is to provide a stable current supply for high‑power LEDs (~350 mA per LED branch), ensuring reliable luminous output while protecting LEDs from thermal runaway and overcurrent conditions.

![Completed Device1](docs/images/device_1.jpg)

---

## Theory of Operation

### Linear Regulators
A linear regulator controls output voltage or current by dissipating excess electrical energy in the form of heat through a pass element operating in its linear region.

**Advantages:**
- Simple implementation
- Low electrical noise
- High reliability
- Minimal electromagnetic interference (EMI)

**Disadvantages:**
- Low efficiency at higher power levels
- Power loss proportional to voltage drop across regulator
- Requires thermal management

![Linear Regulator Concept](docs/images/slide_05_08.png)

### Switching Regulators (Reference)
While not used in the final design, switching regulators were analyzed during the research phase. They regulate voltage or current by rapidly switching a transistor on and off and transferring energy through inductive or capacitive elements. This project intentionally uses a **linear regulation approach** due to simplicity and predictable behavior in constant current LED applications.

![Switching Regulator Concept](docs/images/slide_05_07.png)

---

## Circuit Design & Regulation

### Full System Schematic
The complete circuit utilizes multiple linear regulators to drive specific branches of the LED array, powered by a 12V DC source.

![Full Circuit Schematic](docs/images/slide_02_02.png)

### LED Voltage Requirements
Each high‑power LED used in this system requires approximately ~3.5V forward voltage. To obtain the required operating voltage, two LEDs are connected **in series**, resulting in a total drop of approximately **7V** per branch.

### Current Regulation Topology
High‑power LEDs must be driven using **constant current** rather than constant voltage to prevent thermal runaway. A linear regulator (LM317 family) is configured as a precision current source. 

The output current is determined by the reference voltage ($V_{ref} \approx 1.25V$) and a sense resistor ($R_1$):

$$ I_{out} = \frac{V_{ref}}{R_1} $$

![Constant Current Configuration](docs/images/slide_02_03.png)

**Configuration:**
- **Target Current:** ~350 mA per branch
- **Topology:** Two identical LED series branches connected in parallel
- **Total Current:** ~700 mA

---

## Thermal Management

Since this is a linear system, the power dissipated by the regulator is calculated as:

$$ P_{loss} = (V_{in} - V_{led}) \times I $$

This excess energy is converted into heat. To handle this, the design includes:
1.  **Heatsinking:** Regulators are mounted to dissipating surfaces.
2.  **Enclosure Ventilation:** Strategic openings allow inherent convection.
3.  **Passive Cooling:** The layout promotes airflow without requiring active fans.

---

## Enclosure Design

 The custom enclosure was designed using CAD software (Tinkercad) specifically for this electronics assembly.

![3D CAD Design](docs/images/slide_04_04.png)

**Features:**
- Separate removable top cover with hex-mesh ventilation
- Screw‑mounted lid geometry
- Precision cutouts for LED mounting
- Integrated power input opening
- Passive airflow channels

**Manufacturing:**
- **Process:** FDM 3D Printing
- **Material:** PETG/PLA (Heat resistant recommended)
- **Top Cover:** Printed in white/translucent material for light diffusion considerations.
- **Base:** Printed in black for structural contrast.

![Top View of LED Array](docs/images/device_2.jpg)

---

## Electrical Configuration Summary

| Parameter | Value |
|-----------|--------|
| **Input Voltage** | 12 V DC |
| **LED Forward Voltage** | ~3.5 V |
| **LEDs per Series Branch** | 2 |
| **Voltage per Branch** | ~7 V |
| **Branch Current** | 350 mA |
| **Number of Branches** | 2 |
| **Total Current** | 700 mA |
| **Regulation Type** | Linear Constant Current |

---

## Assembly Steps

1.  **LED Grouping:** Connect LEDs in series pairs.
2.  **Branching:** Connect both series pairs in parallel configuration.
3.  **Sense Resistors:** Install current sense resistors ($R_{sense}$) calculated for 350mA.
4.  **Heatsink Mounting:** Secure the voltage regulators to the heatsink.
5.  **Integration:** Insert electronics into the 3D printed enclosure.
6.  **Wiring:** Route power supply wiring through the rear port.
7.  **Finalizing:** Secure the enclosure lid using screws.

---

## Future Improvements

- **Efficiency:** Implementation of a switching regulator (Buck converter) to reduce heat.
- **Cooling:** Addition of a dedicated active cooling fan.
- **Control:** PWM dimming control implementation.
- **Safety:** Integrated temperature monitoring and auto-shutdown.
- **Production:** Conversion from perfboard to a custom PCB.

---

## License

This project is released for educational and research purposes.
