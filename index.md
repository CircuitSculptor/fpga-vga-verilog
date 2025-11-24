---
layout: home
title: FPGA VGA Driver Project using the Xilinx Basys 3
tags: fpga vga verilog
categories: demo
---

Blog Created on 20/10/25

Updated at 17:30 on 10/11/25

# FPGA VGA Driver Project

In this blog I will walk you through setting up a Vivado project, adding or creating some files and finally uploading your completed project on the Basys 3 FPGA.

## **Template VGA Design**
### **Project Set-Up**

This is my project summary after a successful bitstream generation.

<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjSumBD.png" alt="My Project Summary" width="500">

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

## Lab Work 03/11/2025

This week I got a VGA caputre card to capture my output in a greater resolution compared to photos taken with a phone.

Below are some crisp images of my output with my new setup.

<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjSelfTestHiRes.png" alt="Self Test Hi Res Output" width='500'>
<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjColourStripesHiRes.png" alt="Colour Stripes Hi Res Output" width='500'>
<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjPolandFlagHiRes.png" alt="Colour Stripes Hi Res Output" width='500'>

Here is a link to a video showing my flag sweep demo, [opens in a new tab](https://www.youtube.com/watch?v=iuI142aaKDM)

To get this to work I got a VGA to HDMI adapter that goes into a HDMI capture card. The card is then connected to my laptop and is viewed in OBS Studio.

<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjHDMIcapture.jpg" alt="HDMI Capture setup" width='500'>
<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjOBSstudio.png" alt="OBS Studio" width='500'>

To add to the convinience of having the ability to record your work, I am using a USB Stick to load the bitstream rather than using Vivado and the Hadrware Manager.

My process of getting it working is that I first looked through any documentation for the Basys 3 board. I found everything I needed in the Reference Manual <a href="https://cdn.jsdelivr.net/gh/circuitsculptor/fpga-vga-verilog@main/docs/4520445.PDF#page=12" target="_blank">on page 12</a>. 

From their I looked for a suitable USB Stick. I had a 4GB one that I had to format to FAT32 file system per the documentation. So now I was ready to upload my first bit file and see it working.

My setup with the USB Stick

<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjUSB.jpg" alt="USB Stick setup" width="500">

But it didn't work at first and I wasn't sure why. So I asked ChatGPT for some assistance and it delivered. It told me that I was using the wrong file name for my bit file. I wanted to use the default name of VGATop.bit but the Basys 3 was expecting a file called config.bit. 

So now I created a network of folders on my laptop so that I can store the bit files of each of my projects like my colour stripes and the flags demo. This will greatly speed up protoyping as I can now have many bit files created outside of lab time and when I come back I can run them all in a short amount of time to see which work and show what I thought I coded in. I did install the Vivado design suite on my laptop as it had the required 80GB of storage available.

Nearing the end of this project, I have found that the Basys 3 board started accepting the default bit file name of VGATop. I don't have an explanation for why it is, but that means I don't have to change the file name, all I need is to run the bitstream generation or get it from my folder.

## Lab Work 10/11/2025

This work is from class work I did. It features the project pinout diagram in blocks, with all the internal and external connections. 

To get this work into this blog, I didn't want to take a photo of it after looking back on the effort I took to get the VGA output recorded.

<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjPinoutDiagramNotes.jpg" alt="Pinout Diagram from Class Notes" width="400"> <img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjSignalsNotes.jpg" alt="Signals from Class Notes" width="400"> 


## Lab Work 17/11/2025

### **What is Simulation?**
<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjRunSim.png" alt="Vivado Run Simulation" width="400"> 
Before running your code on the board itself as that takes time, it is good to simulate your code to see if it behaves the way you have coded it. In Vivado I can run a behavioural simulation which is the most common one for this application. This simulation is thanks to the Testbench that was written to simulate the hardware on the board.

In industry, I might be very expensive to take a board from a working system and upload the code to it, which might result in unwanted results.
<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjSignals.png" alt="Simulation signals">

### **What is Synthesis?**
In the synthesis process, Vivado will start converting your code into the building blocks that form the Basys 3.

First it will create schematics of your design. After you do any checks from the simulation output, you can visualise then in the schematics like shown below.

<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjBasicSchematic.png" alt="Basic Schematic" width="600"> <img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjAdvSchematic.png" alt="Advanced Schematic" width="600">

Then Vivado will create an implementation of the code. In the imnages below, Vivado shows how each block is connected together.

<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjImpl1.png" alt="Implementation1" width="300"> <img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjImpl5.png" alt="Implementation5" width="300">

Here is some more images of the internal connections.

<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjImpl3.png" alt="Implementation3" width="600">
<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjImpl4.png" alt="Implementation4" width="600">


<img src="https://raw.githubusercontent.com/circuitsculptor/fpga-vga-verilog/main/docs/assets/images/VGAPrjImpl2.png" alt="Implementation2" width="500">

## **My VGA Design Edit**
I have decided to create a slide show of all the flags in the European Union. I have selected all the flags that are made up from vertical and horizontal stripes only. 

The flags are shown in the following order: Poland, Ireland, Germany, France, Italy, Ukraine, Luxemburg, Romania, Bulgaria, Austria, Bulgraia, Estonia, Latvia, Lithuania, Monaco and the Netherlands.

### **Code Adaptation**
To display my flags, I have modified the rows and column numbers to split up the screen to display each flag. It was a fun experience, seeing a completed flag with the right parameters.

        POLAND: begin
            // WHITE #FFFFFF
            if(row >= 11'd0 && row <11'd240) begin
                red_next  <= 4'b1111;
                green_next <= 4'b1111;
                blue_next  <= 4'b1111;
            end
            // RED #DC143C
            else if(row >= 11'd240 && row <11'd480) begin
                red_next   <= 4'b1101;
                green_next <= 4'b0000;
                blue_next  <= 4'b0000;
            end 
            if(count == COUNT_TO) begin
                state_next = IRELAND;
            end
        end

Briefly show how you changed the template code to display a different image. Demonstrate your understanding. Guideline: 1-2 short paragraphs.
### **Simulation**
Show how you simulated your own design. Are there any things to note? Demonstrate your understanding. Add a screenshot. Guideline: 1-2 short paragraphs.
### **Synthesis**
Describe the synthesis & implementation outputs for your design, are there any differences to that of the original design? Guideline 1-2 short paragraphs.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## **Template Code**
Outline the structure and design of the Verilog code templates you were given. What do they do? Include reference to how a VGA interface works. Guideline: 2/3 short paragraphs, consider including screenshot(s).
