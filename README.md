### COMMONAPI SOMEIP DEMO

可作为CommonAPI SomeIP的使用示例

版本信息

| 名称                 | 版本信息 |
| -------------------- | -------- |
| vsomeip              | v3.3.0   |
| capicxx-core-runtime | v3.2.0   |
| capicxx-core-tools   | v3.2.0.1 |
| capicxx-someip-tools | v3.2.0.1 |

说明：

本demo以本机通信为主，并非双机通信，此外部分信息，被写在代码中，灵活性不足。

#### Dependencies

安装依赖：

```bash
sudo apt-get install cmake cmake-qt-gui libexpat-dev expat default-jre
```

ubuntu 安装boost

```bash

sudo apt-get update
sudo apt-get install libboost-all-dev
```

源码编译可以参考https://blog.csdn.net/qq_41854911/article/details/119454212

创建目录：

```Shell
mkdir  someip
```

编译和安装 vsomeip：

依赖：

`sudo apt-get install asciidoc source-highlight doxygen graphviz`

```bash
git clone https://github.com/GENIVI/vsomeip.git
cd vsomeip
mkdir build
cd build
#CMakeList.txt中要注释掉benchmark,不需要此部分
cmake -DENABLE_SIGNAL_HANDLING=1 -DDIAGNOSIS_ADDRESS=0x10 ..
make
sudo make install
```

编译和安装 CommonAPI Core Runtime：

```bash
git clone https://github.com/GENIVI/capicxx-core-runtime.git
cd capicxx-core-runtime/
mkdir build
cd build
cmake ..
make
sudo make install
```

编译和安装 CommonAPI SomeIP Runtime：

```bash
git clone https://github.com/GENIVI/capicxx-someip-runtime.git
cd capicxx-someip-runtime/
mkdir build
cd build
cmake -DUSE_INSTALLED_COMMONAPI=OFF ..
make
sudo make install
```

切换JAVA版本到Oracle jdk1.8：

https://blog.csdn.net/du402448285/article/details/122217873

```bash
 sudo add-apt-repository ppa:openjdk-r/ppa
输入你的sudo密码继续
2. 升级系统资源包并安装openjdk1.8：
sudo apt-get update
sudo apt-get install openjdk-8-jdk
3. 在多个JDK版本中切换JDK
sudo update-alternatives --config java
选择你需要的JDK版本：
设置一个默认JAVA：
sudo update-alternatives --config javac
4. 检查JDK版本：
java -version
输出以下信息表示成功
openjdk version “1.8.0_01-internal”
OpenJDK Runtime Environment (build 1.8.0_01-internal-b04)
OpenJDK 64-Bit Server VM (build 25.40-b08, mixed mode)

```

或者下载 jdk-8u311-linux-x64.tar.gz

[ jdk-8u311-linux-x64.tar.gz]([Java Archive Downloads - Java SE 8u211 and later (oracle.com)](https://www.oracle.com/java/technologies/javase/javase8u211-later-archive-downloads.html))

```shell
cd / 
sudo mkdir data
sudo cp -r   jdk-8u311-linux-x64.tar.gz /data
sudo tar -xzvvf  jdk-8u311-linux-x64.tar.gz

sudo gedit /etc/profile
#添加如下
export JAVA_HOME=/data/jdk1.8.0_311 
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```



编译CommonAPI Core Runtime代码生成工具：**中国大陆地区不要考虑此方法（网络太慢）**

可以使用购买腾讯云北美云服务器

```bash
git clone https://github.com/GENIVI/capicxx-core-tools.git
cd capicxx-core-tools/org.genivi.commonapi.core.releng
mvn -Dtarget.id=org.genivi.commonapi.core.target clean verify
```

解压得到代码生成工具：

```bash
cd someip
unzip -d ./commonapi_core_generator ./capicxx-core-tools/org.genivi.commonapi.core.cli.product/target/products/commonapi_core_generator.zip
chmod +x ./commonapi_core_generator/commonapi-core-generator-linux-x86_64
```

编译CommonAPI SomeIP Runtime代码生成工具： **中国大陆地区不要考虑此方法（网络太慢）**

可以使用购买腾讯云北美云服务器

```bash
git clone https://github.com/GENIVI/capicxx-someip-tools.git
cd capicxx-someip-tools/org.genivi.commonapi.someip.releng/
mvn -DCOREPATH=/home/lxl/Develop/capicxx-core-tools -Dtarget.id=org.genivi.commonapi.someip.target clean verify
```

解压得到代码生成工具：

```bash
org.genivi.commonapi.someip.cli.product/target/products/commonapi_someip_generator.zip
cd someip
unzip -d ./commonapi_someip_generator ./capicxx-someip-tools/org.genivi.commonapi.someip.cli.product/target/products/commonapi_someip_generator.zip
chmod +x ./commonapi_someip_generator/commonapi-someip-generator-linux-x86_64
```

#### Compilation

创建工程目录：

```bash
cd someip
git clone https://github.com/lixiaolia/commonapi_someip_demo.git
```

生成代码：

```bash
./../commonapi_core_generator/commonapi-core-generator-linux-x86_64 -sk ./fidl/HelloWorld.fidl
./../commonapi_someip_generator/commonapi-someip-generator-linux-x86_64 ./fidl/HelloWorld.fdepl
```

编译工程：

```bash
mkdir build
cd build
cmake ..
make
```

备注：

1.将会提供在腾讯云ubuntu 20.04上编译完整的包

[飞书文档](https://t3z3v2fg00.feishu.cn/docx/VeJMdVEeFotPMax7u5xctbKlnhg?from=from_copylink)

[123文档](https://www.123pan.com/s/WnbtVv-Kk0I.html)  提取码:X4l2

2.以下截图来自doc/commsomeip.pdf

Compile Runtime

有多个选项



