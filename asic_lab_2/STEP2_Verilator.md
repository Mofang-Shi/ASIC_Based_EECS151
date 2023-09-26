# `Verilator`

教程来自：[Verilator User’s Guide](https://verilator.org/guide/latest/index.html)

## 简介

`Verilator`是一款将`Verilog`和`SystemVerilog`硬件描述语言（HDL）设计转换为`C++`或`SystemC`的**编译器**，编译后的文件可以执行。

`Verilator`的特点如下：

- `Verilator`像`GCC`或其他模拟器（如`Cadence Verilog-XL`/`NC-Verilog`或`Synopsys VCS`）一样通过参数调用。

- 对于模拟，需要用户编写一个小小的`C++包装文件`。此包装器（wrapper）定义了`C++`标准函数“main()”，它将`Verilated模型`实例化为`C++/SystemC`对象。

- `C++包装文件`、`Verilator`创建的文件、`Verilator`提供的“运行时的库”，如果适用，则使用`C++`编译器编译`SystemC`库以创建模拟可执行文件（simulation executable）。

- 生成的可执行文件将在“模拟运行时（simulation runtime）”期间执行实际模拟。

- 如果适当启用，可执行文件还可以生成可以查看设计的波形痕迹（waveform traces of the design）。它还可能为后分析创建覆盖范围分析数据。

## 安装

要构建或运行Verilator，需要先安装以下标准软件包：

```
sudo apt-get install git help2man perl python3 make
sudo apt-get install g++  # Alternatively, clang
sudo apt-get install libgz  # Non-Ubuntu (ignore if gives error)
sudo apt-get install libfl2  # Ubuntu only (ignore if gives error)
sudo apt-get install libfl-dev  # Ubuntu only (ignore if gives error)
sudo apt-get install zlibc zlib1g zlib1g-dev  # Ubuntu only (ignore if gives error)
```

我的系统是`Ubuntu 22.04.3`，在实际安装过程中`libgz`、`zlibc`库无法被正常安装。

以下是可以选择安装的，但应安装后可以获得良好的性能：

```
sudo apt-get install ccache  # If present at build, needed for run
sudo apt-get install mold  # If present at build, needed for run
sudo apt-get install libgoogle-perftools-dev numactl
sudo apt-get install perl-doc
```

使用`git`从`GitHub`上拷贝源代码：

```
git clone https://github.com/verilator/verilator
```

转到复制下来的`verilator`文件夹，并检查是否是最新的：

```
cd verilator
git pull        # Make sure we're up-to-date
git tag         # See what versions exist
#git checkout master      # Use development branch (e.g. recent bug fix)
#git checkout stable      # Use most recent release
#git checkout v{version}  # Switch to specified release version
```

完成后创建配置脚本：

```
autoconf        # Create ./configure script
```

在其Git目录原位安装`Verilator`：

```
export VERILATOR_ROOT=`pwd`   # if your shell is bash
setenv VERILATOR_ROOT `pwd`   # if your shell is csh
./configure
# Running will use files from $VERILATOR_ROOT, so no install needed
```

进行编译、测试：

```
make -j `nproc`  # Or if error on `nproc`, the number of CPUs in system
make test
```

一切顺利的话，运行结束后会在倒数第三行看见：

```
Tests passed!
```

**真不容易！**

## 示例

在安装时，我们从源代码处安装了`Verilator`，并希望从编译`Verilator`的地方运行`Verilator`，则我们需要指向路径：

```
export VERILATOR_ROOT=你的安装路径
export PATH=$VERILATOR_ROOT/bin:$PATH
```

现在，让我们创建一个`Verilog`和`C++包装文件`示例：

```
mkdir test_our
cd test_our

cat >our.v <<'EOF'
  module our;
     initial begin $display("Hello World"); $finish; end
  endmodule
EOF

cat >sim_main.cpp <<'EOF'
  #include "Vour.h"
  #include "verilated.h"
  int main(int argc, char** argv) {
      VerilatedContext* contextp = new VerilatedContext;
      contextp->commandArgs(argc, argv);
      Vour* top = new Vour{contextp};
      while (!contextp->gotFinish()) { top->eval(); }
      delete top;
      delete contextp;
      return 0;
  }
EOF
```

然后运行verilator：

```
verilator --cc --exe --build -j 0 -Wall sim_main.cpp our.v
```


- `--cc`：获取`C++`输出。

- `--exe`以及`sim_main.cpp`包装文件：`build`将创建一个可执行文件（an executable ），而不仅仅是一个库（library）。

- `--build`：将不需要手动调用`make`作为单独的步骤。也还可以编写自己的编译规则。

- `-j 0`使用机器尽可能多的CPU线程进行验证（Verilate）。

- `-Wall`：启用了更强的**绒毛警告**（lint warnings，不知道如何翻译）。

`Verilator`创建了名为`obj_dir`的文件夹，里面有很多文件。

接下来让我们运行：

```
obj_dir/Vour
```

**我们成功得到了正确的输出！！！！**

```
shimofang@shimofang-virtual-machine:~/test_our$ obj_dir/Vour
Hello World
- our.v:2: Verilog $finish
```
