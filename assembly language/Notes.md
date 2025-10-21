AVR的三块储存空间
program memory
	以16 bit为基本单位（1 cell）
data memory
	以8 bit为基本单位（1 cell）
EEPROM
	unknown

data space
0x00 ~ 0x1F, 先是32个通用寄存器R0 ~ R31
0x20 ~ 0x5F, 通用IO寄存器区（64个）
0x60 ~ 0xFF, 拓展IO寄存器区 （只是举例）
0x100 ~ 开始是内部SRAM





汇编语言的format
	1.label
		给指令或者数据起名字，用于取用和跳转，写在首行
	2.opcode
		要干的事，比如jmp
	3.operand
		操作的对象，比如寄存器，地址等
	4.comment
		做解释，不翻译

Directive（给汇编器assember的指令，用于操作汇编器，只用于帮助汇编过程，不翻译成机器语言）
	.cseg/.dseg/.eseg
		用于切换到不同的segment
	.db/.dw
		在program memory和EEPROM中放常量，常用于制作lookup table，来编写比如涉及sin(x)这种avr中没有的计算操作的程序
	.byte
		变量占位，不放值，也不能在此处放初始值
	.def/.equ/.set...
		等一系列其他的assember指令

Memory Segment
	code(Flash)
		放程序指令或者有时候放常量（比如如上提到的.db/.dw）
	Data(SRAM)
		放变量，但只能占位，不能写初始值
	EEPROM
		放永久的常量，哪怕掉电之后也保存值

汇编需要进行两遍，也就是所谓的Two-pass
	假如说把编译比作快递员给街区投快递件，那么第一遍编译就是把一整个街区的房子都标号名字，然而第二遍编译才是具体地把快递件投到对应的名字去

Forward reference
	一些情况，比如源代码第一行写着jmp RESET（这种的指令的操作数一般是一个地址）的时候，此时并不知道需要操作的目标地址，无法把指令中的目标地址的机器码写对，所以这是向前引用问题，需要靠Two-pass来解决

Symbol是什么
	Symbol是广义的，地址（比如label，像门牌号）、常量值、寄存器别名（被.def之后的寄存器的名字，便于记忆）

Label是什么
	Label是地址的值，所以Label也是Symbol的一种

Location counter
？？？
代码段和数据段各有一个location counter？？
为什么不占地址？
