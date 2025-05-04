# Module 1 – Foundations of Bare-Metal Programming

# Introduction

Most of us begin embedded programming with Arduino. It's beginner-friendly, but hides how microcontrollers really work. \
 \
This module strips away the abstraction and teaches you to program bare-metal, directly manipulating memory and hardware.

# Learning Goals

- Understand what "bare-metal programming" really means

- Explore the anatomy of a microcontroller

- Learn how to interpret reference manuals

- Get familiar with the toolchain: compiler, linker, debugger

# What is Bare-Metal Programming?

Bare-metal programming means writing code that runs directly on the microcontroller hardware—no OS, no runtime.

define GPIO_PORT (*(volatile unsigned int*)0x40021018)
You're not using digitalWrite(). You're writing directly to registers.

# Bare-Metal vs Arduino vs RTOS

| Feature | Arduino Style | Bare-Metal | RTOS |
|---|---|---|---|
| Abstraction Level | High | Low | Medium |
| Timing Control | Limited | Precise | Scheduled |
| Learning Curve | Easy | Steep | Medium |

# Anatomy of a Microcontroller

- Clock system

- Reset logic

- Memory map

- Registers and SFRs

- Pin multiplexing

- Peripherals (GPIO, UART, ADC, etc.)

(Insert diagram here: MCU block diagram)

# Understanding Datasheets and Reference Manuals

## How to Read a Register Description

***Example from STM32: \
 \
USART_CR1 (Control Register 1) \
Bit 13 - UE: USART enable \
Bit 3  - TE: Transmitter enable \
Bit 2  - RE: Receiver enable***

***To enable TX & RX: \
 \
USART1->CR1 |= (1 << 3) | (1 << 2);***

# Toolchain Overview

## Compilers

- [x] GCC (open source)

- [ ] IAR (commercial)

- [ ] Keil (commercial)

## Linkers, Startup Files, Vector Tables

***ENTRY(Reset_Handler) \
 \
SECTIONS { \
  .text : { \
    *(.isr_vector) \
    *(.text*) \
    *(.rodata*) \
  } \
}***

## Flashing Tools & Debuggers

- ST-Link

- J-Link

- OpenOCD

- PyOCD

# Practice: Blink Without Arduino

define RCC_AHBENR  (*(volatile unsigned int*)0x40021014)
# Additional Notes

- Use the reference manual more than the datasheet when writing bare-metal code

- Your IDE/compiler might auto-generate headers for register addresses

# What’s Next

In the next module, we'll build our first toolchain from scratch and write a startup file manually.

# References

- STM32 Reference Manual (RM0008): https://www.st.com/resource/en/reference_manual/cd00171190.pdf

- GCC for ARM Embedded Processors: https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm
