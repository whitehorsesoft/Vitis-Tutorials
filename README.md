# Forked and modified for personal notes
Ref [here](https://github.com/Xilinx/Vitis-Tutorials) for upstream (original) source.
# General information
- 
# Vitis (includes Vivado) Installation steps
1. Ubuntu instance
1. All commands are run from Bash shell
1. Install [required packages](https://www.xilinx.com/html_docs/xilinx2020_1/vitis_doc/aqm1532064088764.html)
1. Download and install Vivado software (which includes Vitis)
    - If using AWS SDK, use [a version supported by AWS SDK/HDK](https://github.com/aws/aws-fpga/blob/master/supported_vivado_versions.txt)
1. Setup Vitis (ref [here](https://www.xilinx.com/html_docs/xilinx2020_1/vitis_doc/rbk1547656041291.html))
    1. run `source <Vitis_install_path>/Vitis/2019.2/settings64.sh`
    1. download and install [Xilinx Runtime Library (XRT)](https://www.xilinx.com/products/design-tools/vitis/xrt.html#overview)
        - need to check if this can use files in AWS git repo found [here](https://github.com/aws/aws-fpga/tree/master/Vitis/aws_platform/xilinx_aws-vu9p-f1_shell-v04261818_201920_2)
    1. `export PLATFORM_REPO_PATHS=<path to platforms>`

# AWS FPGA Installation / Setup
1. Optional, but make sure to run all Vitis installation steps first
    - For importance of setting up Vitis first, ref especially [here](https://www.xilinx.com/html_docs/xilinx2020_1/vitis_doc/uxq1573167801088.html)
1. Clone AWS from [here](https://github.com/aws/aws-fpga)
1. Source one of the various `setup_.sh` scripts in the AWS FPGA repo dir
    - for Vitis, run `source vitis_setup.sh`

<p align="right">
<a>English</a> | <a href="/docs-jp/README.md">日本語</a>
</p>

<table width="100%">
  <tr width="100%">
    <td align="center"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>2020.1 Vitis™ Application Acceleration Development Flow Tutorials</h1>
    <a href="https://github.com/Xilinx/Vitis-Tutorials/branches/all">See 2019.2 Vitis Application Acceleration Development Flow Tutorials</a>
    </td>
 </tr>
 </table>

## Getting Started

Learn how to [develop accelerated applications using the Vitis™ core development kit](/docs/vitis-getting-started/README.md).

[![Pathways](/docs/vitis-getting-started/images/pathway.png)](docs/vitis-getting-started/README.md)

## Intermediate

  <table style="width:100%">
 <tr>
 <td width="35%" align="center"><b>Tutorial</b>
 <td width="15%" align="center"><b>Kernel</b>
 <td width="50%" align="center"><b>Description</b>
 </tr>
 <tr>
 <td align="center"><a href="/docs/getting-started-rtl-kernels/README.md">Getting Started with RTL Kernels</a></td>
 <td align="center">RTL</td>
 <td>This tutorial demonstrates how to use the Vitis core development kit to program an RTL kernel into an FPGA and build a Hardware Emulation using a common development flow.</td>
 </tr>
 <td align="center"><a href="/docs/vitis_hls_analysis/README.md">Vitis HLS Analysis and Optimization</a></td>
 <td align="center">C</td>
 <td>This tutorial demonstrates how you can use the Vitis HLS tool GUI to build, analyze, and optimize a hardware kernel.</td>
 </tr>
 <tr>
 <td align="center"><a href="/docs/mixing-c-rtl-kernels/README.md">Mixing C and RTL</a></td>
 <td align="center">C and RTL</td>
 <td>This tutorial demonstrates working with an application containing RTL and OpenCL™ kernels to familiarize yourself with the Vitis core development kit flow, along with various design analysis features.</td>
 </tr>
 <tr>
 <td align="center"><a href="/docs/using-multiple-cu/README.md">Using Multiple Compute Units</a></td>
 <td align="center">C and RTL</td>
 <td>This tutorial demonstrates the flexible kernel linking process to increase the number of kernel instances on an FPGA, which improves the parallelism in a combined host-kernel system.</td>
 </tr>
 <tr>
 <td align="center"><a href="/docs/host-code-opt/README.md">Host Code Optimization</a></td>
 <td align="center">C and RTL</td>
 <td>This tutorial demonstrates applying host code optimization techniques to your design.</td>
 </tr>
 <tr>
 <td align="center"><a href="/docs/mult-ddr-banks/README.md">Using Multiple DDR Banks</a></td>
 <td align="center">C and RTL</td>
 <td>This tutorial demonstrates how using multiple DDRs can improve data transfer between kernels and global memory.</td>
 </tr>
 </table>

## Advanced

 <table style="width:100%">
 <tr>
 <td width="35%" align="center"><b>Tutorial</b>
 <td width="15%" align="center"><b>Kernel</b>
 <td width="50%" align="center"><b>Description</b>
 </tr>
 <tr>
  <td align="center"><a href="/docs/controlling-vivado-impl/README.md">Controlling Vivado Implementation</a></td>
 <td align="center">RTL</td>
 <td>This tutorial demonstrates how you can control the Vivado® tools flow when implementing your project.</td>
 </tr>

 </table>

<hr/>
<p align="center"><sup>Copyright&copy; 2020 Xilinx</sup></p>
