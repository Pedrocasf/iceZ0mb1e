### iceZ0mb1e

iceZ0mb1e aims to build a TV80 based demonstration system-on-chip using complete open source FPGA toolchain flow (http://www.clifford.at/yosys/) including firmware compilation with SDCC.

This is a completely free microcontroller based on customizable open source components.

### iceZ0mb1e consists of following parts
* TV80 CPU (https://opencores.org/project,tv80,overview)
* SoC RTL design, iceZ0mb1e consists of:
    * RAM and ROM (using BRAM or SPRAM)
    * UART 16450 compatible
    * Parallel IO
    * i2C Master
    * SPI Master (all CPOL/CPHA modes supported)
* Top-Level designs for some iCE40 development boards (upduino, HX8K Breakout Board)
* C based firmware, that is embedded into BRAM blocks during build
* API Functions for all hardware interfaces
* Complete make based flow, to be as clean as possible

### Supported FPGAs
* Lattice iCE40 HX8K
* Lattice iCE40 UltraPlus 5K

No special blocks are used, so every comparable FPGA in size would fit.

### Test Firmware
The included test firmware will check the RAM size and write some data to IO ports (blink LEDs). Simple UART access with 9600-8N1 is provided.

### Address Map
* ROM = 0x0000 - 0x1FFF (8192 Byte)
* RAM = 0x2000 - 0x3FFF (8192 Byte)
* 16450 UART Base IO = 0x18
* Parallel Base IO = 0x40
* i2C Master = 0x50
* SPI Master = 060

### Build for Target
* UltraPlus 5K (default target): ```make firmware && make fpga && make flash```
* HX8K: ```make firmware TARGET=8k && make fpga TARGET=8k && make flash TARGET=8k```

### Simulate
* ```make sim TARGET=8k```

### Running SoC
<p align="center">
  <img src="https://raw.githubusercontent.com/abnoname/abnoname.github.io/master/img/iceZ0mb1e/Terminal.png" width="350"/>
  <img src="https://raw.githubusercontent.com/abnoname/abnoname.github.io/master/img/iceZ0mb1e/gtkwave.png" width="350"/>
  <img src="https://raw.githubusercontent.com/abnoname/abnoname.github.io/master/img/iceZ0mb1e/IMG_20180321_220358.jpg" width="350"/>
  <img src="https://raw.githubusercontent.com/abnoname/abnoname.github.io/master/img/iceZ0mb1e/IMG_20180130_003538.jpg" width="350"/>
</p>

### Installing yosys toolchain
Installation of essentials for building and running yosys, icestorm and arachne-pnr toolchain (Ubuntu 16.04):
```
sudo apt-get install build-essential clang bison flex \
                     libreadline-dev gawk tcl-dev libffi-dev \
                     pkg-config python cmake libftdi-dev
```

Get yosys, icestorm and arachne-pnr (latest version supports Lattice UltraPlus) and compile toolchain:
```
git clone https://github.com/cliffordwolf/icestorm.git
cd ./icestorm/
make clean
make -j$(nproc)
sudo make install
```
```
git clone https://github.com/cseed/arachne-pnr.git
cd ./arachne-pnr/
make clean
make -j$(nproc)
sudo make install
```
```
git clone https://github.com/cliffordwolf/yosys.git
cd ./yosys/
make clean
make -j$(nproc)
sudo make install
```

### Installing verilog simulator
```
sudo apt-get install iverilog gtkwave
```

### Installing SDCC toolchain
```
sudo apt-get install sdcc sdcc-doc sdcc-libraries sdcc-ucsim \
                     z80asm z80dasm srecord
```

### Why iceZ0mb1e?
* Because it is inspired by redz0mb1e project from fpgakuechle (http://www.mikrocontroller.net/svnbrowser/redz0mb1e/).
* I ported redz0mb1e to Altera DE1 several years ago (http://abnoname.blogspot.de/2013/07/z1013-auf-fpga-portierung-fur-altera-de1.html).
