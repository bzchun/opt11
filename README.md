# CSE 220 Fall 2021

Brevan Chun

Project Opt11

<br>

## Description

This is a description of the project.

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
        $ echo "hello world!"
    ```


<br>

## Notes

Set environment variables (must do on terminal startup(?)).

> `$ export RISCV=~/projects/CSE220/riscv `

> `$ export PATH=$RISCV/bin:$PATH `



<br>


Run baremetal:

> `$ ./dromajo/build_release/dromajo --trace 0 riscv/tests/share/riscv-tests/isa/rv64ua-p-amoadd_d`




<br>



