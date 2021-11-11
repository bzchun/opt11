# CSE 220 Fall 2021

Brevan Chun

Project Opt11: Implement RISC-V draft in dromajo.

<br>

## Description

This is a description of the project.


<br>

### Project Steps:
1. Get dromajo running some simple baremetal
2. Get QEMU to compile and run some baremetal 
3. Get QEMU to run some simple ACLINT
4. Bring the QEMU ACLINT implementation to QEMU(?) In dromajo, check the CLINT (riscv_machine.cpp)

Implement the ACLINT used in qemu in dromajo and figure out a way to verify it.
Put the ACLINT in and ifdef




<br>

## Install

1. [RISC-V GNU Toolchain](https://github.com/riscv/riscv-gnu-toolchain)

    ```
        $ sudo apt-get install autoconf automake autotools-dev curl python3 libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev

        $ cd ~/projects/CSE220/
        $ git clone https://github.com/riscv/riscv-gnu-toolchain
        $ cd riscv-gnu-toolchain
        $ ./configure --prefix=~/projects/CSE220/riscv
        $ make 

        $ cd ..
    ```


2. [RISC-V Tests](https://github.com/riscv/riscv-tests)
    
    
    ```
        $ export RISCV=~/projects/CSE220/riscv
        $ export PATH=$RISCV/bin:$PATH

        $ git clone https://github.com/riscv/riscv-tests
        $ cd riscv-tests
        $ git submodule update --init --recursive
        $ autoconf
        $ ./configure --prefix=$RISCV/tests
        $ make
        $ make install

        $ cd ..
    ```

    

3. [Dromajo](https://github.com/bzchun/dromajo.git)

    ```
        $ git clone https://github.com/bzchun/dromajo.git
        $ cd dromajo
        $ mkidr build_release
        $ cd build_release
        $ cmake -DCMAKE_BUILD_TYPE=Release ..
        $ make

        $ cd ../..

    ```
  
4. QEMU
   
    ```
        $ sudo apt install qemu-riscv64-system
        ...
    ```


<br>

## Notes

* Set environment variables (must do on terminal startup(?)):

    ```
        $ export RISCV=~/projects/CSE220/riscv 
        $ export PATH=$RISCV/bin:$PATH
    ```



<br>


* Run baremetal:

    ``` 
        $ ./dromajo/build_release/dromajo --trace 0 riscv/tests/share/riscv-tests/isa/rv64ua-p-amoadd_d 
    ```
    
    ```
        $ cd <dromajo>/run
        $ riscv64-unknown-elf-gcc -march=rv64g -mabi=lp64 -static -mcmodel=medany -nostdlib -nostartfiles uart_test.c crt.S -lgcc -T test.ld -o uart_test
        $ ../build/dromajo ./uart_test
    ```

<br>


* [Simple function build:](https://mindchasers.com/dev/rv-getting-started)

    ``` 
        $ riscv32-unknown-elf-gcc -g tst.c -o tst
        $ riscv32-unknown-elf-objdump -d tst
    ```

    \*where `test.c` is a simple function in c and make sure $PATH is set


<br>

* Files:
    - riscv_machine.cpp
    - riscv_cpu.cpp
    - dromajo_main.cpp
    - setup.md

    ```$ grep -rnw '/home/bzchun/projects/CSE220/dromajo/' -e "clint" ```



