# wmt_asm_study
My ASM study

## ref  
* https://github.com/compiler-explorer/compiler-explorer  
* https://godbolt.org  
* https://cppinsights.io  
* https://redasm.io/  

## armcc, LPC2138最简闪烁灯汇编, 自制  
* search baidupan, work_arm_hello_lpc2138_v2.rar  

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

## 6502的汇编方法：  
（1）生成二进制的方法：用cc65，方法是ca65 test.asm和ld65 -t none test.o（如果需要列表文件，可能要da65反汇编或者在ca65中生成，但可能缺少跳转地址）。或者用dasm，可能会在头部两字节添加偏移，需要自己去掉，或者生成list文件。注意cc65和dasm的伪指令可能不兼容
（2）示例代码：参考www.instructables.com/6502-6522-Minimal-Computer-With-Arduino-MEGA和它的前篇（可以把jmp后面的常量改成标号）。或者参考free6502的测试汇编  
6502 & 6522 Minimal Computer (with Arduino MEGA) Part 2  

## TD4的汇编方法：  
（1）生成二进制的方法：在网页上vanya.jp.net/td4/，只支持单指令汇编。另一个命令行版本：wuxx/TD4-4BIT-CPU/software/td4as.exe。  
（2）示例代码：（TD-4GP02A）vanya.jp.net/td4/，或者参考wuxx/TD4-4BIT-CPU/software/test/test_0_output.s  
