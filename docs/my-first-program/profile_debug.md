﻿<table class="sphinxhide">
 <tr>
   <td align="center"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>2020.1 Vitis™ Application Acceleration Development Flow Tutorials</h1>
   <a href="https://github.com/Xilinx/Vitis-Tutorials/branches/all">See 2019.2 Vitis Application Acceleration Development Flow Tutorials</a>
   </td>
 </tr>
 <tr>
 <td>
 </td>
 </tr>
</table>

# 4. Profiling the Application

The Vitis™ core development kit generates various reports on the kernel resource and performance during compilation. It also collects profiling data during application execution in emulation mode and on the FPGA acceleration card. This lab describes how to generate the reports and collect, display, and read the profiling results in the Vitis integrated design environment (IDE).

## Profile Summary

XRT automatically collects profiling data on host applications. After the application finishes execution, the Profile Summary report is saved in HTML, CSV, and Google Protocol Buffer formats in the solution report or working directory. These reports can be reviewed in a web browser, spreadsheet viewer, or the integrated Profile Summary view in the Vitis IDE.

1. To enable profile monitoring, create the `xrt.ini` file with `profile=true`. This file should be in the execution directory.
   >**TIP**: For details on creating the `xrt.ini` file, refer to the [Profile and Trace Reports](../Pathway3/ProfileAndTraceReports.md) lab. 

   ```
   [Debug]
   profile=true
   timeline_trace=true
   data_transfer_trace=fine
   ```

2. To generate the Profile Summary report for hardware emulation, use the `--profile_kernel` option to build the kernel during the hardware linking stage. This enables the gathering of performance data during emulation. This option can be added in `design.cfg` file.

   ```
   platform=xilinx_u200_xdma_201830_2
   debug=1
   profile_kernel=data:all:all:all

   [connectivity]
   nk=vadd:1:vadd_1
   ```

   ```
   v++ -t hw_emu --config design.cfg -c -k vadd -I'../src' -o'vadd.xilinx_u200_xdma_201830_2.xo' './src/vadd.cpp'
   v++ -t hw_emu --config design.cfg -l -o'vadd.xilinx_u200_xdma_201830_2.xclbin' vadd.xilinx_u200_xdma_201830_2.xo
   ```

3. To view the Profile Summary report in the IDE, use the Vitis analyzer.

   >**TIP**: For details on using the Vitis analyzer, refer to the [Profile and Trace Reports](../Pathway3/ProfileAndTraceReports.md) lab.

   ```bash
   vitis_analyzer ./vadd.hw_emu.xclbin.run_summary
   ```

   ![](./images/profile_summary_vitis.png)

   The Profile Summary includes several useful statistics for any application. Important metrics are highlighted in the preceding figure. This will provide you with a general idea of the functional bottlenecks in your application.

4. Look at the Kernel to Global Memory section of the report. Notice the total number of data transfers and average bytes per transfer.

5. Look at the Duration column under the Top Kernel Execution section. Notice the time it took to execute the kernel in hardware emulation/hardware.

6. Next, click the **OpenCL APIs** tab in the Profile Summary report. Notice the details provided on the various OpenCL API calls, including the number of calls and the duration of the calls.

   ![](./images/profile_summary_vitis_2.png)

The preceding figure is a captured from hardware emulation, which uses high-level simulation models for data transfers. Notice that the  highlighted calls `clFinish`, `clCreateProgramWithBinary`, and `clReleaseContext` are consuming most of the application time. It is best practice to observe the statistics highlighted in the figure when run on hardware.

## Application Timeline

The Application Timeline collects and displays host and device events on a common timeline to help you understand and visualize the overall health and performance of your systems. These events include:

* OpenCL API calls from the host code.
* Device trace data including AXI transaction start/stop, kernel start/stop, etc.

1. To enable Timeline Trace information gathering, create the `xrt.ini` file with `timeline_trace=true` and `data_transfer_trace=fine`.

   ```
   [Debug]
   profile=true
   timeline_trace=true
   data_transfer_trace=fine
   ```

2. To generate the Timeline Trace report for hardware emulation, build the kernel using the `--profile_kernel` option during the hardware linking stage (if you have not done this already).

   ```
   v++ -t hw_emu --config design.cfg -c -k vadd -I'../src' -o 'vadd.xilinx_u200_xdma_201830_2.xo' './src/vadd.cpp'
   v++ -t hw_emu --config design.cfg -l -o 'vadd.xilinx_u200_xdma_201830_2.xclbin' vadd.xilinx_u200_xdma_201830_2.xo
   ```

3. To view the Timeline Trace, use the Vitis analyzer to view it in the IDE.

   ```bash
   vitis_analyzer ./vadd.hw_emu.xclbin.run_summary
   ```

   The following figure shows the generated Timeline Trace report.

   ![](./images/timeline_trace_vitis.png)

4. Hover the cursor over the bars showing the Read/Write data transfers in the Application Timeline view to get more information such as burst length, DDR memory resource, and duration of transfer.

## Guidance

The Guidance view provides feedback throughout the development process. It presents all issues encountered from building the actual design all the way through runtime analysis in a single location.

The Vitis analyzer can be used to open these specific reports or can directly open the compile_summary, link_summary, or run_summary generated by the compile, link, and run stage. When these summary reports are opened, the Vitis analyzer automatically opens the relevant reports.

   ```bash
   vitis_analyzer ./vadd.hw_emu.xclbin.run_summary
   ```

The following figure shows the Guidance view for the VADD example.

![](./images/guidance_report_vitis.png)

## Kernel Reports (HLS)

After compiling a kernel using the Vitis compiler, the Vitis compiler runs the Vitis High-Level Synthesis (HLS) tool to synthesize the OpenCL C/C++ code to RTL code. During the process, the HLS tool automatically generates reports, which include details about the performance and logic usage of the custom-generated hardware logic from your kernel code. These reports are available when the Vitis compiler is called with the `--save-temps` option.

   ```
   v++ -t hw_emu --config design.cfg --save-temps -c -k vadd -I'../src' -o 'vadd.xilinx_u200_xdma_201830_2.xo' './src/vadd.cpp'
   ```

To view the Kernel report, use the following command to open the Vitis HLS project, and open the HLS Synthesis Report for the VADD kernel.

   ```bash
   vitis_hls -p _x.hw_emu/vadd/vadd.hw_emu/vadd/vadd
   ```

The following figure shows the HLS report for the VADD example kernel.

![](./images/hls_kernel_report_1.png)

## Optimization

From the reports and images, you can see that there is a scope for improving the performance of the application. There are different optimization techniques which can be employed. For more information refer to the next step of the pathway, the [Optimizing Accelerated FPGA Applications: Convolution Example](../convolution-tutorial/README.md) and [Optimizing Accelerated FPGA Applications: Bloom Filter Example](../bloom/README.md) tutorials.

## Conclusion

Congratulations! You have successfully completed all the labs of this tutorial.

1. You successfully converted standard C++ code into a Vitis core development kit kernel.
2. You built a host program that deploys and talks to the kernel on the FPGA.
3. You used the command line to compile and link the kernel to an `xclbin`.
4. You executed the design in software and hardware emulation modes before running it on an Alveo Data Center accelerator card.
5. You familiarized yourself with the reports generated during application build and execution.
</br>
<hr/>
<p align="center" class="sphinxhide"><b><a href="/docs/vitis-getting-started/README.md">Return to Getting Started Pathway</a> — <a href="docs/my-first-program/README.md">Return to Start of Tutorial</a></b></p>

<p align="center" class="sphinxhide"><sup>Copyright&copy; 2020 Xilinx</sup></p>
