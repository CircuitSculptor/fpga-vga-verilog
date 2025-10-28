---
layout: home
title: FPGA VGA Driver Project using the Xilinx Basys 3
tags: fpga vga verilog
categories: demo
---

Blog Created on 20/10/25

Updated at 19:35 on 28/10/25

In this blog I will walk you through setting up a Vivado project, adding or creating some files and finally uploading your completed project on the Basys 3 FPGA.

## **Template VGA Design**
### **Project Set-Up**

I setup a new Vivado Project using its setup wizard. 
First step is creating a name for the project and selecting a storage location of your choosing.
Here is where I encountered my first problem with the Vivado Design Suite. The software does not like when you create a project on your Onedrive. 
To fix this, I had to create a folder on the C drive of the computer I will be working from for the rest of the semester.

Then I needed to select the project type. I selected the first option, RTL Project. RTL stands for Register-Tranfer Level and its used in creating the logic for your project using a Hardware Description Language such as Verilog.

When finshed you should have something similar to mine.

<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjCreationSum.png" alt="Project Creation"> 

## Lab Work 20/10/2025
I got template code to setup a vga output for the Basys 3 FPGA.
It included 6 files. 
- ### VGATop.v
  
  This file is used to references other files and any variables used within each one. That is why it has a fitting name, as it is at the top of the project structure.
- ### VGASync.v

  Here all the VGA timing sygnals are generated from a 25Mhz clock that was scaled down from the 100Mhz on board oscillator. To run a VGA display you need those specific timing information. In this case it is set to 640x480 resolution. The timing data can be found in the Basys 3 Reference Manual on <a href="https://cdn.jsdelivr.net/gh/circuitsculptor/fpga-vga-verilog@main/docs/4520445.PDF#page=23" target="_blank">pages 21-23</a>
- ### VGAColourCycle.v

  Here is where it gets interesting as now I can write some code to change the colour depending on the row and column value.
- ### VGAColourStripes.v

  Same here, I modified the example code to create different patterns. Below is some of my output.
  
  <img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjStartup.jpg" alt="VGA Startup Output" width="500">
  <img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjTemplate.jpg" alt="VGA Template Output" width="500">
  <img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjFlagPL.jpg" alt="VGA Poland Flag" width="500">
- ### Testbench.v

  This file is special as it allows the user to test some of their code like the sync generator code before uploading to the board as that is a lengthy process. This file will contain any required paramenters to create the correct timing signals and view them on a signal analyser built into Vivado. It may come in very useful to someone experimenting with the sync signals. Notable signal is the reset, everything starts on the rising edge of the clock.

  <img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjSignals.png" alt="Signal Analyser Output">
- ### Basys3_Master.xdc

  This is the constraints file used to set the output pins of the VGA connector and other peripherals. The template constraints file for the Basys 3 can be viewed <a href="https://github.com/Digilent/digilent-xdc/raw/master/Basys-3-Master.xdc" target="_blank">here</a>. The VGA pinout diagram can be viewed <a href="https://cdn.jsdelivr.net/gh/circuitsculptor/fpga-vga-verilog@main/docs/4520445.PDF#page=20" target="_blank">here</a>.









# Above is mostly finished, below is template code


This is my project summary after a successful bitstream generation.

<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjSumBD.png" alt="My Project Summary" width="500">

## **Template Code**
Outline the structure and design of the Verilog code templates you were given. What do they do? Include reference to how a VGA interface works. Guideline: 2/3 short paragraphs, consider including screenshot(s).
### **Simulation**
Explain the simulation process. Reference any important details, include a well-selected screenshot of the simulation. Guideline: 1/2 short paragraphs.
### **Synthesis**
Describe the synthesis and implementation processes. Consider including 1/2 useful screenshot(s). Guideline: 1/2 short paragraphs.
### **Demonstration**
Perhaps add a picture of your demo. Guideline: 1/2 sentences.

## **My VGA Design Edit**
Introduce your own design idea. Consider how complex/achievabble this might be or otherwise. Reference any research you do online (use hyperlinks).
### **Code Adaptation**
Briefly show how you changed the template code to display a different image. Demonstrate your understanding. Guideline: 1-2 short paragraphs.
### **Simulation**
Show how you simulated your own design. Are there any things to note? Demonstrate your understanding. Add a screenshot. Guideline: 1-2 short paragraphs.
### **Synthesis**
Describe the synthesis & implementation outputs for your design, are there any differences to that of the original design? Guideline 1-2 short paragraphs.
### **Demonstration**
If you get your own design working on the Basys3 board, take a picture! Guideline: 1-2 sentences.

## **More Markdown Basics**
This is a paragraph. Add an empty line to start a new paragraph.

Font can be emphasised as *Italic* or **Bold**.

Code can be highlighted by using `backticks`.

Hyperlinks look like this: [GitHub Help](https://help.github.com/).

A bullet list can be rendered as follows:
- vectors
- algorithms
- iterators

Images can be added by uploading them to the repository in a /docs/assets/images folder, and then rendering using HTML via githubusercontent.com as shown in the example below.

<img src="https://raw.githubusercontent.com/melgineer/fpga-vga-verilog/main/docs/assets/images/VGAPrjSrcs.png">
