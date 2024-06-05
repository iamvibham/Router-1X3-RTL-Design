# Router Project

## Introduction

The Router project aims to design and implement a versatile router system for efficient packet routing in network communication. This README provides an overview of the project's key features, including the Router Input Protocol, Router Output Protocol, FIFO Functionality, and Router FSM (Finite State Machine).

## Router Input Protocol

The Router Input Protocol governs how input signals are processed and synchronized to ensure reliable data transmission. All input signals, except low reset, are active high and synchronized to the falling edge of the clock. This synchronization strategy helps maintain setup and hold times. Key aspects of the Router Input Protocol include:

- **Packet Validity:** The `packet_valid` signal is asserted on the clock edge when the header byte is driven onto the input data bus.
- **Address Routing:** The header byte contains the address, determining which output channel (`data_out_0`, `data_out_1`, `data_out_2`) the packet should be routed to.

## Router Output Protocol

The Router Output Protocol defines how output signals are synchronized and processed to ensure efficient data delivery to the receiver. All output signals are active high and synchronized to the rising edge of the clock. Key features of the Router Output Protocol include:

- **Output Port Buffers:** Each output port (`data_out_X`) is internally buffered by a FIFO of size 16x9, ensuring data integrity and efficient data delivery.
- **Data Availability Signaling:** The `vld_out_X` signals (`vld_out_0`, `vld_out_1`, `vld_out_2`) indicate when valid data is available on a particular output data bus, facilitating timely data reception by the receiver.

## FIFO Functionality

The FIFO Functionality ensures efficient data storage and retrieval in the router system. Each output port is equipped with a FIFO of size 16x9, operating on the system clock and reset by a synchronizer active low reset. Key aspects of FIFO Functionality include:

- **Write Operation:** Data is written to the FIFO on the rising edge of the clock when `write_enb` is high, ensuring data integrity and preventing data loss.
- **Read Operation:** Data is read from the FIFO on the rising edge of the clock when `read_enb` is high, ensuring timely data delivery to the output ports.

## Router FSM (Finite State Machine)

The Router FSM manages the router's state transitions and ensures proper data routing and processing. The FSM includes states such as `STATE-DECODE_ADDRESS`, `STATE-LOAD_FIRST_DATA`, `STATE-LOAD_DATA`, `STATE-LOAD_PARITY`, and others, each serving a specific function in the packet routing process.

![Router Finite State Machine](router fsm image.png)
