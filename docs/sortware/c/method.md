## 1. 输入回显并退格清除

Q：无论是在windows系统CMD还是linux系统终端中，用户输入字符或数字都会在窗台(stdout)上回显用户输入的内容，如果输入错误可按退格键进行删除重新输入，那如果在裸机程序框架下中编写shell交互如何实现回显和退格的功能？

A：
  - 回显：利用串口特性即每次只传输个字节(1个字符)，自定义gets、getchar和putchar功能函数同时判断串口寄存器状态，当寄存器为空则通过puts函数将缓冲区的字符串依次通过putchar存放到串口寄存器中传输；
  - 回退：

```c
putchar('\b');     //将光标后退一格
putchar('');       //输出空字符替换原先字符，效果相当于清除功能
putchar('\b');     //再次将光标后退一格，等待重新输入
```

N：如果是在windows下使用串口，则需要考虑换行符(\n\r)。