***

# Week 2: Fundamentals of SoC Design

## What is a System-on-Chip (SoC)?

<img width="598" height="456" alt="image" src="https://github.com/user-attachments/assets/cfff10e6-2b70-4c67-99c5-4c5459fe9997" />

A System-on-Chip (SoC) is an integrated circuit that consolidates all major components of a computer or electronic system onto a single chip. Instead of discrete components soldered onto a PCB, an SoC brings together processing, memory, connectivity, and specialized hardware to deliver high functionality in compact form. SoCs are pervasive in modern electronics, enabling devices like smartphones, wearables, and embedded systems to deliver high performance, low power consumption, and efficiency.

## Components of a Typical SoC

<img width="1085" height="566" alt="image" src="https://github.com/user-attachments/assets/a31257ec-7db6-40ea-a9b4-625f115f6e95" />

A classic SoC design comprises the following essential building blocks:

- **CPU (Processor Core):** The central unit executing instructions and controlling overall system operation.
- **Memory (RAM, ROM, Flash):** Stores program code, data, and temporary information required by the CPU and peripherals.
- **Peripherals:** Include I/O controllers, communication modules, timers, ADCs, DACs, and other external interface blocks offering system connectivity.
- **Interconnect (Bus/Fabric):** The communication backbone linking CPU, memory, and peripherals. Interconnects (like AMBA, Wishbone) ensure data transfer and synchronization across all components within the SoC.

## Why BabySoC is a Simplified Model for Learning SoC Concepts

<img width="1248" height="698" alt="image" src="https://github.com/user-attachments/assets/b43a16bd-9157-49bc-b846-011fb4aaa9be" />


BabySoC is designed as an educational microcosm of commercial SoC architectures. It simplifies the real-world complexity by:

- Providing minimal but representative CPU, memory, peripheral, and interconnect elements.
- Allowing learners to focus on connections and operations between modules without the distraction of scalability and advanced optimizations.
- Facilitating hands-on experience and experimentation in SoC structure, behavior, and integration, making it accessible for learning foundational principles before tackling industry-scale systems.

## The Role of Functional Modelling Before RTL and Physical Design

<img width="1024" height="561" alt="image" src="https://github.com/user-attachments/assets/d4d3b5c0-7932-4542-bcad-3b585e1dacf0" />

Functional modelling serves as the blueprint for the SoC, capturing high-level behavior and inter-module communication before any low-level detail is committed:

- It clarifies system architecture, functionality, and verification strategy.
- Designers use functional models to validate logic, scheduling, and dataflow, identifying errors and inefficiencies early.
- This stage precedes RTL (Register Transfer Level) implementation, which details cycle-accurate logic, and physical design, which lays out silicon floorplans and physical connections.
- By accurately depicting desired system behavior, functional modelling streamlines subsequent RTL and physical design efforts and mitigates costly redesign cycles.

## How BabySoC Fits Into the SoC Learning Journey

BabySoC bridges the gap between theory and practical design. Its simplicity and modularity make it ideal for:

- Deepening conceptual understanding of SoC system integration, design trade-offs, and validation approaches.
- Experimenting with functional modelling, observing signal flow, and understanding verification methodologies.
- Transitioning knowledge from high-level concepts to RTL coding and eventually physical realization.

Through BabySoC, students build solid foundations in SoC design fundamentals, empowering them to tackle increasingly complex systems confidently.

***
