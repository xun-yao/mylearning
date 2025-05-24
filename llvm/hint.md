# llvm学习


## 中间代码基本概念：
- 中间代码的意义：降低各种源语言译为机器码工作量（mn->m+n）。
- 分类：
1.  后缀表示，即将语法树后序遍历。
2.  语法树（DAG）
3.  三地址码（TAC）:最多涉及三个地址，即两个操作数，一个结果
基本语法示例：
```
    factional:
        n = param1  #从参数栈取第一个参数
        if n <= 1 goto L1
        t1 = n - 1
        param = t1
        call factional
        t2 = RET
        t3 = t2 * n
        RET = t3
        return
    L1:
        RET = 1
        return
    main :
        n = 5
        call factional
        fact = RET
```
注：三地址码类似汇编 (add ax,bx),能更好的转化为机器码，但其又与硬件无关，即作为中间语言。

4.  静态单赋值形式（SSA）：
（1） 要求每个变量只被赋值一次,便于后续优化代码：
    - 由于每个变量赋值后不变，有利于常量传播:
    ```
    简化前：
     int a = 5;
     if(a > 0)
        b = 10;
     else
        b = 5;
    
    简化后:
        int a = 5;
        int b = 10;
    ```
（2） 若某个变量被赋值后没被使用，可以消除死代码.


## 基本块

1. 基本块的意义：用基本块为节点，生成流图，可以更好的表示当前执行到的位置。

2. 基本块的划分：一条首指令到下一条首指令或结尾。

确定首指令原则：
  - 第一条三地址指令
  - 转移指令的目标指令
  - 转移指令的下一个指令


## llvm IR

1. llvm IR 特点：
    - risc风格的三地址
    > %2 = add i32 %0,%1

注：risc（reduced instruction set computer） 精简，只完成一个基本操作。

   - 具有无限**虚拟**寄存器的SSA形式  
   - 强类型系统 —— 即不允许int + string 这样的隐式转化。

## light IR：精简的llvm IR

基本语法：

- 基本类型
   > ia: a位宽的整数
   > float
   > label ：基本快的类型

- 组合类型
   > ia* ：指针
   > [n * < type >] ： 数组
   > < ret-type > @ (< arg-type >...) ： 函数


注： '@'用于全局标识符（函数），'%'用于局部标识符（寄存器）

- 终止指令：基本块只有一个入、出口。基本快最后一条指令为**终止指令**
   > ret 指令
   > br 指令

- 二元运算指令
例：
   > %2 = sub i32 %1,%0
   > %2 = fdiv float %1,%0

注：有a、s、m、d种。

- 内存操作指令
    > < result > = load < type >, < type >* < pointer >
    > store < type > < value >,< type >* < pointer >

- 类型转换
    > < result > = zext | fptosi | sitofp < type > < value > to < new_type >
    
- 比较指令
    > < result > = icmp | fcmp < cond > < type > < value1 >, < value2 >
注： cond:eq、ne、sgt、ugt、sge、uge、slt、ult、sle、ule

- 函数调用
    > 

- getelementptr
    >
