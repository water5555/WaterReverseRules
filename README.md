# WaterReverseRules
逆向分析规则定义（Reverse Engineering Conventions）



## LOAD: start（reference block）

```asm
LOAD:00000072D239A584 EXPORT start
LOAD:00000072D239A584 start DCD 0x5BAD8433                    ; DATA XREF: LOAD:00000072D2450678↓o
LOAD:00000072D239A588 DCD 0x21585055
LOAD:00000072D239A58C DCD 0x2A0D06F8
LOAD:00000072D239A590 DCD 0
LOAD:00000072D239A594 DCD 0x119C28
LOAD:00000072D239A598 DCD 0x119C28

```


### 1. 取地址（Address of）

**符号：**
&

**用法：**
&symbol → 获取符号的 Virtual Address 地址

**示例：**
&start -> 00000072D239A584

### 2. 内存访问（memory access）

**符号：**
type []

**用法：**
type [symbol] -> 小端方式读取symbol地址 size(type)字节

**示例：**
byte [start] -> 0x33


### 3. page（page align）

**符号：**
page

**用法：**
page(symbol, 4|16）-> 获取符号地址所在内存页以 4|16 kb对齐方式的起始地址

**示例：**
page(start, 4) -> 0x72D239A584 & ~(0x1000 - 1) = 0x72D239A000
page(start, 16) -> 0x72D239A584 & ~(0x4000 - 1) = 0x72D2398000



### 3. pageoff（page offset）

**符号：**
pageoff

**用法：**
pageoff(symbol, 4|16）-> 获取符号地址所在内存页以 4|16 kb对齐方式的偏移地址

**示例：**
pageoff(start, 4) -> 0x72D239A584 & (0x1000 - 1) = 0x584
pageoff(start, 16) -> 0x72D239A584 & (0x4000 - 1) = 0x2584






