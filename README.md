# wmt_asm_study
My ASM study

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

## EASy68K  
* http://www.easy68k.com  

## GNUSim8085  
* https://github.com/GNUSim8085/GNUSim8085  
