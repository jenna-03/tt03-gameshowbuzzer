![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg) ![](../../workflows/wokwi_test/badge.svg)

# What is Tiny Tapeout?

TinyTapeout is an educational project that aims to make it easier and cheaper than ever to get your digital designs manufactured on a real chip!

Go to https://tinytapeout.com for instructions!

## How to change the Wokwi project

Edit the [info.yaml](info.yaml) and change the wokwi_id to match your project.

## How to enable the GitHub actions to build the ASIC files

Please see the instructions for:

* [Enabling GitHub Actions](https://tinytapeout.com/faq/#when-i-commit-my-change-the-gds-action-isnt-running)
* [Enabling GitHub Pages](https://tinytapeout.com/faq/#my-github-action-is-failing-on-the-pages-part)

## How does it work?

When you edit the info.yaml to choose a different ID, the [GitHub Action](.github/workflows/gds.yaml) will fetch the digital netlist of your design from Wokwi.

After that, the action uses the open source ASIC tool called [OpenLane](https://www.zerotoasiccourse.com/terminology/openlane/) to build the files needed to fabricate an ASIC.

## Resources

* [FAQ](https://tinytapeout.com/faq/)
* [Digital design lessons](https://tinytapeout.com/digital_design/)
* [Learn how semiconductors work](https://tinytapeout.com/siliwiz/)
* [Join the community](https://discord.gg/rPK2nSjxy8)

## What next?

* Share your GDS on Twitter, tag it [#tinytapeout](https://twitter.com/hashtag/tinytapeout?src=hashtag_click) and [link me](https://twitter.com/matthewvenn)!

# **Game Show Buzzer System**

This project implements a simple game show buzzer system using Verilog. It allows multiple contestants to buzz in, and it locks out additional inputs once the first contestant has buzzed in.

## **Features**

- **Multiple Contestant Inputs:** Supports up to 6 contestants.
- **Lockout Mechanism:** Once a contestant buzzes in, further inputs are ignored until the system is reset.
- **Clock and Reset Inputs:** Utilizes a clock signal for synchronization and a reset signal to clear the lockout.

## **Hardware Requirements**

- **FPGA or Simulation Environment:** Suitable for running Verilog code.
- **Input Pins:** 8 total; 6 for contestant buzzers, 1 for clock, and 1 for reset.
- **Output Pins:** 8 total; 6 to indicate which contestant buzzed in first.

## **Software Requirements**

- **Verilog Compiler or FPGA Development Environment:** Examples include Xilinx Vivado or Intel Quartus.

## **Module Overview**

### **Ports**

- **io_in [7:0]:** Input port array.
  - **io_in[0]:** Clock signal (clk).
  - **io_in[1]:** Reset signal (rst).
  - **io_in[7:2]:** Contestant buzzer inputs (buzzer_inputs).
- **io_out [7:0]:** Output port array.
  - **io_out[5:0]:** Indicates which contestant buzzed in first (buzzer_lockout_reg).

### **Internal Signals**

- **buzzer_inputs [5:0]:** Internal wire for contestant buzzer inputs.
- **clk:** Internal wire for the clock signal.
- **rst:** Internal wire for the reset signal.
- **buzzer_lockout_reg [5:0]:** Register to store the state of the buzzer lockout mechanism.

### **Functionality**

- **Clock and Reset:** The module uses the `clk` signal for synchronization and the `rst` signal to reset the lockout register.
- **Buzzer Inputs:** Monitors the `buzzer_inputs` for contestant buzzers. When a contestant buzzes in, the corresponding bit in the `buzzer_lockout_reg` is set, locking out further inputs until reset.
- **Lockout Mechanism:** Once the `buzzer_lockout_reg` is set (i.e., not equal to `6'b000000`), no additional buzzer inputs are accepted until the system is reset.

## **Usage**

### **Connect Inputs:**
- Connect the `io_in` pins to the appropriate signals: 6 contestant buzzers, a clock signal, and a reset signal.

### **Observe Outputs:**
- The `io_out` pins will indicate which contestant buzzed in first by setting the corresponding bit in the `buzzer_lockout_reg`.

---

By following the instructions above, you can implement and test the Game Show Buzzer System to manage contestant inputs in a competitive environment.

