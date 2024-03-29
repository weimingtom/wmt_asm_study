# wmt_asm_study
My ASM study

## TODO  
* arm7, pic32, avr, stc89c52  

## mips, Assemblers, Linkers, and the SPIM Simulator
* https://pages.cs.wisc.edu/~larus/HP_AppA.pdf  
* https://pages.cs.wisc.edu/~larus/spim.html  

## mips  
* edumips64:  
https://edumips.org  
* winmips64:    
http://indigo.ie/~mscott/  
* https://github.com/kchasialis/QtMips-Di  
* qtspim  
https://pages.cs.wisc.edu/~larus/spim.html  

## qtspim, MIT 6.828 操作系统工程导读  
https://zhuanlan.zhihu.com/p/368954250  

## dasmfw, 68hc11?      
https://github.com/Arakula/dasmfw  

## ref  
* https://github.com/compiler-explorer/compiler-explorer  
* https://godbolt.org  
* https://cppinsights.io  
* https://redasm.io/  

## armcc, LPC2138最简闪烁灯汇编, 自制  
* search baidupan, work_arm_hello_lpc2138_v2.rar  
```
		ARM
		AREA reset,CODE,READONLY
		ENTRY
start 	
		LDR      r0,=0x00ffff00
		LDR      r1,=0xe0028000
		STR      r0,[r1,#8]
		B        |L1.76|
|L1.44|		
		MOV      r2,#0x100
		LDR      r0,=0xe0028000
		STR      r2,[r0,#0xc]
		BL       delay
		
		RSB      r0,r2,r2,LSL #16
		LDR      r1,=0xe0028000
		STR      r0,[r1,#4]
		BL       delay
|L1.76|		
		B        |L1.44|	;b start
		
delay	PROC
		MOV      r0,#0
		B        |L1.12|
|L1.8|
		ADD      r0,r0,#1
|L1.12|
		LDR      r1,=0x001e8480
		CMP      r0,r1
		BCC      |L1.8|
		BX       lr
        ENDP

		;import   delay2
		;BL      delay2
		
		END
```
* c language version, also see work_arm_hello_lpc2138_v2.rar  
```
#include <LPC213x.H>

void delay (void) {                     /* Delay function                     */
  unsigned int cnt;

  for (cnt = 0; cnt < 2000000; cnt++);
}

int main (void) {
  unsigned int n;

  IODIR0 = 0x00FFFF00;                  /* P0.8..23 defined as Outputs        */

  while (1) {                           /* Loop forever                       */
    //for (n = 0x00000100; n <= 0x00800000; n <<= 1) {
      n = 0x00000100; //P0.8 ON
		  /* Blink LED1 .. LED16                                                  */
      IOCLR0 = n;                       /* Turn on LED                        */

      delay();                          /* Delay                              */
      IOSET0 = 0x00FFFF00;              /* Turn off LEDs                      */

			//this code is from E:\Keil_v4\ARM\Boards\Embedded Artists\LPC2138 QSB\Blinky
		  delay(); //added, for blink
		  //P0.8->pin 33
    //}
  }
}
```

## 《ARM嵌入式应用开发技术白金手册》  

## ghidra, mips decompile, arm反汇编工具    
* https://github.com/NationalSecurityAgency/ghidra/releases  

## microdigitaled, ARM汇编书, Keil, 树莓派arm汇编,    
* http://www.microdigitaled.com/ARM/ASM_ARM/Code/ARM_ASM_codes.htm  
search baidupan, arm_asm_code.zip  
* https://nicerland.com/raspberry-pi/  
search baidupan raspberry-pi_asm  
* https://github.com/weimingtom/wmt_ai_study/blob/master/asm_001.md  

## Proteus 7 samples, basic interpreter      

## asm11, sim68xx    
* http://www.aspisys.com/asm11.htm  
* http://www.oocities.org/thetropics/harbor/8707/simulator/sim68xx/  

## MARS, mips  

## 51单片机（8051）的汇编方法：  
（1）生成二进制的方法：用Keil C51 uvision2（或者keil 4），A51和L51，待考；或者用as31和sdcc（在www.pjrc.com/tech/8051），方法是as31 -l -Fbin test.asm。或者sdas8051 -l test.asm（需要改成0x表示十六进制常量，但输出二进制可能不正确）。asx8051似乎编译失败  
（2）示例代码：stc-isp有IO的汇编示例（不过太长了）；或者找《8051 单片机P1口实验》MOV P1；或者找这个《Blinking LED using 8051》用CPL P1.0取反（只支持P1的位取反，似乎不支持整个P1字节取反）：www.circuitstoday.com/blinking-led-using-8051  
* 51单片机资料_我的光盘.iso, 单片机资料  
```
MAIN: MOV	P1, #00000000B	
     	  ACALL 	KK				
		  MOV	 P1, #11111111B	
		  ACALL	KK				
		  SJMP	MAIN			
    KK : MOV	R5, #04		
    K1:  MOV	R6, #0FFH
    K2:  MOV	R7, #80H
    K3:  DJNZ 	R7, K3
     	 DJNZ  	R6, K2
     	 DJNZ 	R5, K1
     	 RET			
```
* p1, https://www.circuitstoday.com/blinking-led-using-8051    
```
START: CPL P1.0
       ACALL WAIT  
       SJMP START

WAIT:  MOV R4,#05H
WAIT1: MOV R3,#00H
WAIT2: MOV R2,#00H
WAIT3: DJNZ R2,WAIT3
        DJNZ R3,WAIT2
        DJNZ R4,WAIT1
        RET
```
* p2, https://www.circuitstoday.com/blinking-led-using-8051  
```
START: CPL P1.0
       ACALL WAIT  
       CPL P1.0
       CPL P1.1
       ACALL WAIT
       CPL P1.1  
       SJMP START

WAIT:  MOV R4,#05H
WAIT1: MOV R3,#00H
WAIT2: MOV R2,#00H
WAIT3: DJNZ R2,WAIT3
        DJNZ R3,WAIT2
        DJNZ R4,WAIT1
        RET
```


## 6502的汇编方法：  
（1）生成二进制的方法：用cc65，方法是ca65 test.asm和ld65 -t none test.o（如果需要列表文件，可能要da65反汇编或者在ca65中生成，但可能缺少跳转地址）。或者用dasm，可能会在头部两字节添加偏移，需要自己去掉，或者生成list文件。注意cc65和dasm的伪指令可能不兼容
（2）示例代码：参考www.instructables.com/6502-6522-Minimal-Computer-With-Arduino-MEGA和它的前篇（可以把jmp后面的常量改成标号）。或者参考free6502的测试汇编  
* 6502 & 6522 Minimal Computer (with Arduino MEGA) Part 2  
* program1  
```
LDA#$55
NOP
ROL
STA$1010
JMP$1000
The ROL rotates the contents of the accumulator one bit left which means the $55 now becomes $AA.
In machine code (hex): A9 55 EA 2A 8D 10 10 4C 00 10
```
* program2  
```
LDA#$01
STA$8100
ADC#$03
STA$8100
JMP$1005
In machine code (hex):  A9 01 8D 00 81 69 03 8D 00 81 4C 05 10
```



## TD4的汇编方法：  
（1）生成二进制的方法：在网页上vanya.jp.net/td4/，只支持单指令汇编。另一个命令行版本：wuxx/TD4-4BIT-CPU/software/td4as.exe。  
（2）示例代码：（TD-4GP02A）vanya.jp.net/td4/，或者参考wuxx/TD4-4BIT-CPU/software/test/test_0_output.s  


## arm gdb arm-linux-run and qemu-arm  
* see mips and arm asm samples in gdb source  
* 以前提到过，如果源码编译arm目标的gdb代码，会生成一个arm-linux-run工具（具体运行的汇编示例参考gdb源码），所以gdb代码也有汇编例子。其实qemu也有一个类似的，叫用户模式qemu，就是除了qemu-system-arm，还有一个叫qemu-arm的命令，可以运行arm-linux-gnueabi-gcc -static静态生成的elf文件。原理大概是拦截最底层的控制台输出，arm的话不清楚，但mips是有专门的syscall指令用于控制台输出  

## bsvc, 68kasm, for m68k, 68000    
* https://github.com/BSVC/bsvc  
* for ubuntu 140432  
* cd src; make -f Makefile.Linux; sudo make -f Makefile.Linux install  
* bsvc (then select samples, 68000, .setup)   
* 68kasm -l xxx.asm (see samples, 68000; don't use 68kasm ./xxx.asm)    
* http://nanja.net/asm/  
* https://www.kkaneko.jp/cc/as/jikken/index.html  
* windows:  
* search bsvc-bin.7z  
* https://github.com/pIlIp-d/BSVC_with_TCL  

## EASy68K  
* http://www.easy68k.com  

## GNUSim8085  
* https://github.com/GNUSim8085/GNUSim8085  

## mips, 反编译cs3410.jar代码，带汇编器    
* https://zhuanlan.zhihu.com/p/105777438  
* https://www.cs.cornell.edu/courses/cs3410/2018fa/logisim/components.html  

## emu8080  
* https://www.tramm.li/i8080/index.html  
* search baidupan, emu8080_v2.rar  

## 龙芯汇编语言程序设计  
* https://www.bilibili.com/video/BV1zx411G7y3  

## 使用GNU工具链进行嵌入式裸机开发  
* https://www.cnblogs.com/thammer/p/10596429.html  
* https://sourcery.sw.siemens.com/GNUToolchain/subscription56984  
下载2018-q1  
* https://www.plm.automation.siemens.com/global/en/products/embedded-software/sourcery-codebench-lite-downloads.html  
下载Nios2 gcc  
* https://sourcery.sw.siemens.com/GNUToolchain/subscription56984  
* https://sourcery.sw.siemens.com/GNUToolchain/subscription42545  
* https://sourcery.sw.siemens.com/GNUToolchain/subscription57164  
* https://www.it1352.com/2577875.html  
* https://www.shuzhiduo.com/A/6pdDPq4Xdw/  
search connex qemu  

## (TODO) 微机原理教学实验板, 8088, 8086开发板  
* 微机原理教学实验板_8088开发板  

## (IMP) Assembly Programming and Computer Architecture for Software Engineers  
* https://github.com/brianrhall/Assembly  
* 汇编程序设计与计算机体系结构：软件工程师教程
* (TODO) X86 and I64 masm differences and gas and nasm  

## [MIPS汇编语言程序设计].MIPS.Assembly.Language.Programming.(2003)  
* MIPS.Assembly.Language.Programming.(2003)  

## C# i8080 emulator  
* https://github.com/BluestormDNA/i8080-Space-Invaders  

## js i8080 emulator  
* https://github.com/begoon/i8080-js  

## C++ i8080 emulator, with TinyBasic source ASM program      
* https://github.com/maly/arduino8080basic  
* arduino8080basic_v1_win_success.rar  

## 8080a-8085 Assembly Language Programming  
* Leventhal-8080a-8085AssemblyLanguageProgramming  

## tinyasm  
* https://github.com/nanochess/tinyasm
* https://github.com/pts/mininasm  

## Retro-Computers  
* https://github.com/douggilliland/Retro-Computers  

## (TODO) Z80汇编语言程序设计  
csdn download  
TODO  

## NES-Hello-World, 6502  
* https://github.com/pedroafabri/NES-Hello-World  

## bootBasic, bootOS  
https://blog.csdn.net/weixin_42169971/article/details/116949435  
https://github.com/nanochess/bootOS  
