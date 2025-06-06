# Windows环境下配置python

## python基本指令
在cmd下运行：

1. 获取当前解释器和pip包版本
```
    pip --version
    python --version
```
注：pip安装库的路径一般在pythonx.xx.x/Scripts下，

2. 查询当前环境中所有的python解释器

> where python

注：尽量在环境变量中只选中一个解释器和一个pipScripts

3. 切换当前python版本
- 将原版本~\pythonx\ 及 ~\pythonx\Scripts\ 从环境变量删去
- 将新版本python解释器路径和pip路径添加

4. 虚拟环境...待完成