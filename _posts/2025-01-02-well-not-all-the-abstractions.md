---
title:  "Well not all the Abstractions"
mathjax: false
layout: post
categories: media
---

Welcome to Tear Down All The Abstractions, a project that I've wanted to undertake for quite a long time. This first post will describe what the project is, some motivation behind _why_ I'm doing this project, and what I hope to get out of it.


## What is Tear Down All The Abstractions?
Tear Down All The Abstractions (TDATA) is ultimately going to be a fully-custom single-board computer running on an FPGA. Now "fully-custom single-board computer" could mean anything from an implementation of a simple 8-bit microprocessor running Pong to a 64-bit superscalar x86 CPU running Ubuntu 22.04, so the goals of the project are:
 - Fully-custom RISC Instruction-Set Architecture (ISA) heavily based on RISC-V, called R-ISC-ZN
 - Fully-custom scalar CPU for R-ISC-ZN implemented in Verilog running on an FPGA
 - Basic GPU capable of text-rendering and basic shape rasterization, programmed in some yet undetermined shader language (admittedly, I don't know much about GPUs and how they work, which is part of the purpose of this project)
 - Custom General-Purpose OS called RZN-OS that will run on the custom CPU.
 - Custom Object-Oriented High-Level Language called RZN that will be used to write applications for RZN-OS
 - A translation layer similar to Apple's Rosetta to be able to run applications on my custom hardware (this may or may not be possible)

While this is a huge to-do list, I really have no time horizon for completion. I anticipate that I'll be working on this for years and years. However, to make make this project manageable and actually be able to finish _something_, I won't quite be tearing down _all_ the abstractions.

## Wait, so _not_ all the abstractions?
If I was truly tearing down all the abstractions, I'd have to start with vacuum tubes and punchcards, but I don't have enough space for a vacuum tube computer :). So I'll have to start at some base level of abstraction, although I'll try to tear down as many as I can. The base abstractions are:
 - All code will be written on a modern computer running a modern OS, in a modern language, and compiled with a modern compiler.
 - All hardware will be designed at the Register Transfer Level, not the Gate, Switch, or Transistor Level. I'll also be using an FPGA, not making the CPU by placing transistors on a breadboard ;). However, I do want to explore PCB Design a little, and so I may _eventually_ get around to making a custom Wi-Fi board for the computer, because as far as I know there aren't any existing [PMOD](https://en.wikipedia.org/wiki/Pmod_Interface) Wi-Fi Receivers out there.

## So what's the point?
Modern computer engineering is _built_ on abstractions. Even something as simple as turning on a personal computer has so many steps and interactions that I don't understand, from the bootloader to driver activations to BIOS configurations. The motivation behind TDATA is that I want to be able to understand exactly what's happening in every part of a computer system.

I learn best by doing, and so TDATA will be my attempt to Tear Down All The Abstractions and write a fully-custom computer system from as low a level as possible, in order to try and implement what I learn in university about Computer Architecture, Compilers, Operating Systems, and Data Structures and Algorithms. I finally feel that I've built a good enough foundation through school that I'm ready to tackle this project.

## What's the goal?
The ultimate goal of TDATA will be to write a post on this blog from a web browser written in RZN, running on RZN-OS, running on a custom CPU for the R-ISC-ZN ISA that is implemented on my FPGA. Whether that takes 1 year or 20, I hope to one day be able to do it.

## Development in Layers
Attacking this project head-on and trying to do everything from scratch immediately would be far too difficult, and knowing myself, would result in me abandoning the project pretty quickly. As a result, I'm going to try and complete the project in a _layered_ manner, which means I'm going to start components at a higher-level, and then upon completion, re-work them to start at a lower-level. A good example is my first subproject - an LLVM Frontend for my custom language, RZN. If I was truly tearing down all of the abstractions, I wouldn't use LLVM, and would instead do everything myself. However, I don't quite feel ready to tackle the optimization and codegen steps that LLVM performs myself, and so I'll be starting by implementing an LLVM Frontend in OCaml. This also allows me to not have to start with the ISA design and the custom CPU, nor do I have to work on an emulator for R-ISC-ZN, as I can simply use the x86 backend for LLVM and test the language features on my computer. With this approach, if I encounter any bugs, I'll know that they are a result of my langugage frontend, and not my ISA or my CPU implementation. This layered approach also allows me to mostly work on the component I want to work on at any given time, and minimizes (but does not eliminate) dependencies between different components, which will ease debugging immensely.

## Plan for this Blog
I hope to publish weekly on updates throughout the development process. With that, stay tuned for next week where I'll have started an LLVM Frontend for RZN in OCaml.
