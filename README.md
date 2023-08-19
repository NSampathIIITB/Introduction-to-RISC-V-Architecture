# RISC-V-Architecture

This github repository summarizes the progress made in the ASIC class about RISC-V Architecture . Quick links:

[Day-0 : Insatallation of RISC-V toolchain](#day-0)

[Day-1 : Introduction to RISC-V ISA And GNU compiler toolchain](#day-1)

[Day-2 : Introduction to Application Binary Interface And Basic Error Flow](#day-2)

[Day-3 : Digital Logic with TL-Verilog and Makerchip](#day-3)

[Day-4 : Basic RISC-V CPU micro-architecture](#day-4)

[Day-5 : Complete Pipelined RISC-V CPU micro-architecture](#day-5)

## Day-0

<details> 
<summary> Installation </summary>
**Steps to install RISC-V toolchain (linux)

```
git clone https://github.com/kunalg123/riscv_workshop_collaterals.git
cd riscv_workshop_collaterals
chmod +x run.sh
./run.sh

```

 Once you run it you will get **make** error. ignore it  and type the following commands

 ```

cd ~/riscv_toolchain/iverilog/
git checkout --track -b v10-branch origin/v10-branch
git pull 
chmod 777 autoconf.sh 
./autoconf.sh 
./configure 
make
sudo make install

```

- To set the PATH variable in .bashrc

```
source .bashrc
gedit .bashrc
#Instead of **nsaisampath** put your **username**
export PATH="/home/nsaisampath/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH" #Type at last line # save and close the bashrc and type
source .bashrc

```
</details>


[Acknowledgement](#acknowledgement)

[Reference](#reference)


