# VS Code 配置 C++ 开发环境指南

## 1. 安装 MSYS2 环境
### 步骤说明
1. **下载 MSYS2**  
   - 首次安装仅包含终端
   - 在 MSYS2 终端执行：
     ```bash
     pacman -S mingw-w64-ucrt-x86_64-toolchain
     ```

2. **获取关键目录**  
   - 工具链安装后，在 `ucrt64` 文件夹中可找到：
     - `bin/`：包含 `gcc.exe` 等解释器
     - `include/`：标准头文件目录

## 2. 配置 VS Code
### 修改 C++ 配置文件
1. 打开配置（`Ctrl+Shift+P` 搜索 `Edit Configurations (JSON)`）
2. 修改关键参数：
   ```json
   {
     "includePath": [
       "E:/environment/msys64/ucrt64/include/**"
     ],
     "compilerPath": "E:/environment/msys64/ucrt64/bin/gcc.exe"
   }
   ```
  > **注意**：`**` 表示递归包含子目录,includepath为头文件路径，compilerpath为解释器路径

## 3. 设置系统环境变量
### 必要操作
- 将解释器路径加入用户 PATH：
  ```
  E:/environment/msys64/ucrt64/bin
  ```

## 4. 常见问题解决
### 临时文件路径错误
**错误现象**：  
```
Fatal error: can't create C:\Users\��Ѻ�\AppData\Local\Temp\ccsC0B6M.o: No such file or directory
```

**解决方案**：
1. **原因分析**：
   - 中文用户名导致路径识别异常
   - 编译器默认使用 `%TEMP%` 存放临时文件

2. **修改步骤**：
   - 更改系统、用户环境变量：
     - `TEMP`: 指向新目录（如 `D:\Temp`）
     - `TMP`: 同步修改
   - 验证修改：
     ```cmd
     echo %TEMP%
     echo %TMP%
     ```

**附加优势**：  
可节省 C 盘空间，避免系统盘臃肿
