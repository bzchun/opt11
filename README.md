# CSE 220 Fall 2021

Brevan Chun



## Description


Project Opt11: Implement the ACLINT RISC-V specification in dromajo. This implementation is not complete. Once completed, the altered files should be merged with Dromajo. The QEMU RISC-V ACLINT was used as a guide for the implementation found here. Other resources were also used.


<br>

### Project Steps:
1. Get dromajo running some simple baremetal
2. Get QEMU to compile and run some baremetal 
3. Get QEMU to run some simple ACLINT
4. Bring the QEMU ACLINT implementation to QEMU(?) In dromajo, check the CLINT (riscv_machine.cpp)

- Implement the ACLINT used in qemu in dromajo and figure out a way to verify it.
Put the ACLINT in and ifdef




<br>

## Environment Setup

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
  
4. [QEMU](https://github.com/qemu/qemu)
   
    ```
        $ sudo apt install qemu-riscv64-system
        ...
    ```
    - See QEMU installation directions

<br>


## Files

* riscv_machine.cpp

    - added 4 functions similar to the QEMU implementation.
    - call these functions instead of the default clint functions

* clint_lines.txt
    
    - output of a grep to find everwhere in Dromajo where the word "clint" is used

<br>


## Notes

* Set environment variables (must do on terminal startup):

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

    \*where `tst.c` is a simple program in c and make sure $PATH is set

<br>

\*This project was completed in a VM VirtualBox running Ubuntu 20.04.3LTS

<br>


## Relevant Links

- [RISC-V ACLINT Spec](https://github.com/riscv/riscv-aclint/blob/main/riscv-aclint.adoc)
- [RISC-V Priveledged Spec](https://github.com/riscv/riscv-isa-manual/releases/tag/draft-20211201-f65ddcf)
- [QEMU RISC-V ACLINT](https://github.com/qemu/qemu/blob/2c3e83f92d93fbab071b8a96b8ab769b01902475/hw/intc/riscv_aclint.c)
- [SiFive CLINT Spec](https://static.dev.sifive.com/FU540-C000-v1.0.pdf)
- [WD Presentation](https://linuxplumbersconf.org/event/11/contributions/1098/attachments/805/1584/Next_gen_riscv_interrupt_support_v3.pdf)
- [OpenSBI](https://github.com/riscv-software-src/opensbi)


