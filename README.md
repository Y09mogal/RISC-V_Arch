# RISC-V_Arch

## Day-0
<details> 
<summary>Installation of RISC-V toolchain</summary>

<br />

**Follow below given steps to install RISC-V toolchain :**

<br />

```bash
git clone https://github.com/kunalg123/riscv_workshop_collaterals.git
cd riscv_workshop_collaterals
chmod +x run.sh
./run.sh

```

<br />

 Upon running it, if you get make error, ignore that and type the following commands :

<br />

 ```bash

cd ~/riscv_toolchain/iverilog/
git checkout --track -b v10-branch origin/v10-branch
git pull 
chmod 777 autoconf.sh 
./autoconf.sh 
./configure 
make
sudo make install

```

<br />

- To set the PATH variable in .bashrc

<br />

```bash
source .bashrc
gedit .bashrc
#Instead of **nsaisampath** put your **username**
export PATH="/home/nsaisampath/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH" #Type at last line # save and close the bashrc and type
source .bashrc

```


</details>

## Day-1
<details>
<summary> Introduction to RISC-V ISA </summary>



</details>

<details>
<summary> Integer number representation </summary>



</details>

<details>
<summary> RISCV gcc compilation and assembly code </summary>



</details>

## Day-2


### Acknowledgments
* Kunal Ghosh, Director, VSD Corp. Pvt. Ltd.

### Contact Information
* Yash Dharemsh Mogal, IMtech 2020, International Institute of Information Technology, Bangalore Yash.Mogal@iiitb.ac.in
* Kunal Ghosh, CEO and Co-founder, VSD Corp. Pvt. Ltd. kunalghosh@gmail.com

## References
* https://github.com/kunalg123/riscv_workshop_collaterals)https://github.com/kunalg123/riscv_workshop_collaterals
* https://en.wikipedia.org/wiki/Toolchain
* https://en.wikipedia.org/wiki/GNU_toolchain
* https://www.vsdiat.com
