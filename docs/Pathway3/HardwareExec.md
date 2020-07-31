﻿<table class="sphinxhide">
 <tr>
   <td align="center"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>2020.1 Vitis™ Software Development Platform Application Acceleration Development Flow Tutorials</h1>
   <a href="https://github.com/Xilinx/Vitis-Tutorials/branches/all">See 2019.2 Vitis Application Acceleration Development Flow Tutorials</a>
   </td>
 </tr>
 <tr>
 <td>
 </td>
 </tr>
</table>

# 4. Executing in Hardware

>**IMPORTANT:** This lab requires the use of an Alveo Data Center accelerator card to run the compiled kernel binary, `.xclbin`. If you do not have access to a machine with an Alveo card installed, you will not be able to complete this lab.

## Introduction

In hardware execution, the host program runs on the host machine, and the kernel code runs on an accelerator card using a Xilinx device, such as the Alveo card. The performance data you get from hardware execution is the actual performance from the actual hardware. The Run Summary, with the Profile Summary and Timeline Trace reports described in the previous lab are also produced.

>**TIP:** Turning on device profiling for the system build (`-t hw`) is intrusive and can negatively affect overall application performance. This feature should only be used for performance debugging on the hardware, and should be disabled in the production build.

## Before You Begin

Review and run the [Building an Application](./BuildingAnApplication.md), [Running Software and Hardware Emulation](./Emulation.md) and [Generating Profile and Timeline Trace Reports](./ProfileAndTraceReports.md) labs before running this lab. This lab uses the source files and options as in these previous labs, though all the necessary commands to build the host and hardware platform are shown in this lab.

## Building the Design

Before running applications in Xilinx boards or devices, it is necessary to build the design with `-t hw` option passed to the `v++` command while building the hardware.

The [Building an Application](./BuildingAnApplication.md) lab describes building the host software and hardware and how to specify the *<build_target>*.

>**IMPORTANT:** Before running any of the examples, ensure you have sourced the runtime script.
>
>  ```bash
>  #Setup runtime. XILINX_XRT will be set in this step
>  #Note that it's only necessary to setup runtime before deployment on hardware.
>  source /opt/xilinx/xrt/setup.sh
>  ```
>
>**TIP**: Also, ensure the environment variable XCL_EMULATION_MODE is not set. In previous labs, it might have been set to `sw_emu` or `hw_emu`.

Run the following command.

   ```bash
   unset XCL_EMULATION_MODE
   ```

## Building the Application

With the host program and hardware platform (`xclbin`), you can run the application on Xilinx boards or devices. If you have not built the host program and hardware platform, you can use the following commands.

>**IMPORTANT**: Due to the synthesis and implementation of the FPGA binary file, compiling and linking for the hardware target can take significant time.

  ```bash
  source /opt/Xilinx/Vitis/2019.2/settings64.sh
  source /opt/xilinx/xrt/setup.sh
  #make sure working path is in reference-files/run
  g++ -I$XILINX_XRT/include/ -I$XILINX_VIVADO/include/ -Wall -O0 -g -std=c++11 ../src/host.cpp  -o 'host'  -L$XILINX_XRT/lib/ -lOpenCL -lpthread -lrt -lstdc++
  v++ -t hw --config design.cfg -c -k mmult -I'../src' -o 'mmult.hw.xilinx_u200_xdma_201830_2.xo' '../src/mmult.cpp'
  v++ -t hw --config design.cfg -l -o 'mmult.hw.xilinx_u200_xdma_201830_2.xclbin' mmult.hw.xilinx_u200_xdma_201830_2.xo
  ```

## Running the Application

  ```bash
  ./host mmult.hw.xilinx_u200_xdma_201830_2.xclbin
  ```

After successfully running the application, you will see a similar output in the Console view.

  ```
  Loading: 'mmult.hw.xilinx_u200_xdma_201830_2.xclbin'
  TEST PASSED
  ```

## Using xbutil to Check Board Status

Using `xbutil` is an optional but convenient tool to do analysis and debug related to Xilinx boards. For example, run the following command to check the board status.

  ```bash
  xbutil query
  ```

The board status, compute unit status, and so on display. For more information about `xbutil`, refer to the [Vitis Environment Reference Materials](https://www.xilinx.com/cgi-bin/docs/rdoc?v=2020.1;t=vitis+doc;d=yxl1556143111967.html) in the Application Acceleration Development flow of the Vitis Unified Software Platform Documentation (UG1416).

## Next Steps

You should understand the steps required for building and running an application using the Vitis core development kit. These include coding the software program and kernel, building the application, running software and hardware emulation, viewing reports, and running the application on an accelerator card. The next steps will be to use this understanding to [build your first program](../my-first-program/README.md).
</br>
<hr/>
<p align="center" class="sphinxhide"><b><a href="/docs/vitis-getting-started/README.md">Return to Getting Started Pathway</a> — <a href="./README.md">Return to Start of Tutorial</a></b></p>

<p align="center" class="sphinxhide"><sup>Copyright&copy; 2020 Xilinx</sup></p>
