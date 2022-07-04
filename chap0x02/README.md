# 第二章：linux服务器系统使用基础（实验）

## 实验环境

- 当前课程推荐的 Linux 发行版本
- - 本地环境（Ubuntu）
  - 云环境（CentOS）
- 在[asciinema](https://asciinema.org/)注册一个账号，并在本地安装配置好asciinema

## 实验问题

- 使用表格方式记录至少 2 个不同 Linux 发行版本上以下信息的获取方法，使用 [asciinema](https://asciinema.org/) 录屏方式「分段」记录相关信息的获取过程和结果

- 【软件包管理】在目标发行版上安装` tmux `和 `tshark` ；查看这 2 个软件被安装到哪些路径；卸载 `tshark` ；验证` tshark` 卸载结果

- 【文件管理】复制以下代码到终端运行，在目标 Linux 发行版系统中构造测试数据集，然后回答以下问题：

  ```
   cd /tmp && for i in $(seq 0 1024);do dir="test-$RANDOM";mkdir "$dir";echo "$RANDOM" > "$dir/$dir-$RANDOM";done
  ```

  - 找到 `/tmp` 目录及其所有子目录下，文件名包含 `666` 的所有文件
  - 找到 `/tmp` 目录及其所有子目录下，文件内容包含 `666` 的所有文件

- 【文件压缩与解压缩】练习课件中 [文件压缩与解压缩](https://c4pr1c3.github.io/LinuxSysAdmin/chap0x02.md.html#/12/1) 一节所有提到的压缩与解压缩命令的使用方法

- 【跟练】 [子进程管理实验](https://asciinema.org/a/f3ux5ogwbxwo2q0wxxd0hmn54)

- 【硬件信息获取】目标系统的 CPU、内存大小、硬盘数量与硬盘容量

---

## 实验步骤

#### 1.【软件包管理】在目标发行版上安装 `tmux` 和 `tshark` ；查看这 2 个软件被安装到哪些路径；卸载 `tshark` ；验证 `tshark` 卸载结果

1. ##### Ubuntu 20.04.2 LTS

   1.1**tmux**

   在Ubuntu 20.04.2 LTS上，使用命令

   ```bash
   sudo apt install tmux
   ```

   即可安装。安装后查看软件安装路径有两种方法，分别是`find`命令和`dpkg -L`命令，具体命令为

   ```bash
   dpkg -L tmux
   sudo find / -name tmux
   ```

   [![asciicast](https://asciinema.org/a/h2yz8O3aOnQIKaHGBywQYV9H4.svg)](https://asciinema.org/a/h2yz8O3aOnQIKaHGBywQYV9H4)（因录像后面输入命令字母错误，附上截图![image-20220703232424778](C:\Users\wxxiao\AppData\Roaming\Typora\typora-user-images\image-20220703232424778.png)

   1.2 **tshark**

   在Ubuntu 20.04.2 LTS上，使用命令

   ```bash
   sudo apt install tshark
   ```

   即可安装。安装后查看软件安装路径同样有两种方法，分别是`find`命令和`dpkg -L`命令，具体命令为

   ```bash
   dpkg -L tshark
   sudo find / -name tshark
   ```

   卸载安装包的命令为

   ```bash
   sudo apt purge tshark
   ```

   [![asciicast](https://asciinema.org/a/xDS3pRyy7V3cYzU1SdP7lPoJP.svg)](https://asciinema.org/a/xDS3pRyy7V3cYzU1SdP7lPoJP)

#### 2.【文件管理】复制以下代码到终端运行，在目标 Linux 发行版系统中构造测试数据集，然后回答以下问题：

```
 cd /tmp && for i in $(seq 0 1024);do dir="test-$RANDOM";mkdir "$dir";echo "$RANDOM" > "$dir/$dir-$RANDOM";done
```

- #### 找到 `/tmp` 目录及其所有子目录下，文件名包含 `666` 的所有文件

- #### 找到 `/tmp` 目录及其所有子目录下，文件内容包含 `666` 的所有文件

   1.**Ubuntu 20.04.2 LTS**

```bash
cd /tmp && for i in $(seq 0 1024);do dir="test-$RANDOM";mkdir "$dir";echo "$RANDOM" > "$dir/$dir-$RANDOM";done
```

使用如上命令建立测试文件，

使用命令

```bash
sudo find ./ -name "*666*"
```

来找到 `/tmp` 目录及其所有子目录下，文件名包含 `666` 的所有文件。

使用命令

```bash
sudo grep -rn "666" ./ --exclude=*.cast
```

来找到 `/tmp` 目录及其所有子目录下，文件内容包含 `666` 的所有文件。

在使用`asciinema`录屏时，会在当前文件下生成`*.cast`文件影响最终的输出

所以需要使用`--exclude=*.cast`将`asciinema`生成的文件排除在外

[![asciicast](https://asciinema.org/a/HN144MfqC7ZBagFDSXk1cHH1X.svg)](https://asciinema.org/a/HN144MfqC7ZBagFDSXk1cHH1X)

[![asciicast](https://asciinema.org/a/s4wE4psEFGII411OnRAQbou4A.svg)](https://asciinema.org/a/s4wE4psEFGII411OnRAQbou4A)

#### 3.【文件压缩与解压缩】练习课件中 [文件压缩与解压缩](https://c4pr1c3.github.io/LinuxSysAdmin/chap0x02.md.html#/12/1) 一节所有提到的压缩与解压缩命令的使用方法

[![asciicast](https://asciinema.org/a/FSHUTZHtydeg2rddMML0T385C.svg)](https://asciinema.org/a/FSHUTZHtydeg2rddMML0T385C)

[![asciicast](https://asciinema.org/a/8j7GdORYxlGBsandpHw9vQRFY.svg)](https://asciinema.org/a/8j7GdORYxlGBsandpHw9vQRFY)

#### 4.【跟练】 [子进程管理实验](https://asciinema.org/a/f3ux5ogwbxwo2q0wxxd0hmn54)

[![asciicast](https://asciinema.org/a/iyP9QV4jez0nZogxMWFvT7yvD.svg)](https://asciinema.org/a/iyP9QV4jez0nZogxMWFvT7yvD)

#### 5.【硬件信息获取】目标系统的 CPU、内存大小、硬盘数量与硬盘容量

`lshw`可以显示详细的硬件信息，使用`lshw -short`可以通过概要的方式显示硬件信息

1. **Ubuntu 20.04.2 LTS**

[![asciicast](https://asciinema.org/a/g6HrbLlV90ksxG35zamHmaghu.svg)](https://asciinema.org/a/g6HrbLlV90ksxG35zamHmaghu)

#### 6、使用表格方式记录至少 2 个不同 Linux 发行版本上以上信息的获取方法

---

|       版本号        |                    `ubuntu 20.04`                    |                     `CentOS 7.7`                     |
| :-----------------: | :--------------------------------------------------: | :--------------------------------------------------: |
|        安装         |                `sudo apt install XXX`                |                  `yum install xxx`                   |
|      安装路径       |                     `which XXX`                      |                     `which xxx`                      |
|        卸载         |          `sudo apt-get remove --purge XXX`           |                 `yum -y remove xxx`                  |
| 找特定文件名的文件  |             `sudo find ./ -name '*XXX*'`             |             `sudo find ./ -name '*XXX*`              |
|  找特定内容的文件   |               `sudo grep -r 'XXX' ./`                |               `sudo grep -r 'XXX' ./`                |
| gzip的压缩与解压缩  |      `gzip test.txt` and `gzip -d test.txt.gz`       |      `gzip test.txt` and `gzip -d test.txt.gz`       |
| bzip2的压缩与解压缩 |    `bzip2 -z test.txt`and`bzip2 -d test.txt.bz2`     |    `bzip2 -z test.txt`and`bzip2 -d test.txt.bz2`     |
|  zip的压缩与解压缩  |    `zip test.txt.zip /tmp`and`unzip test.txt.zip`    |    `zip test.txt.zip /tmp`and`unzip test.txt.zip`    |
|  tar的压缩与解压缩  | `tar -czvf test.tar test.txt`and`tar -xzvf test.tar` | `tar -czvf test.tar test.txt`and`tar -xzvf test.tar` |
|  7z的压缩与解压缩   |     `7za a test.7z /test.txt`and`7za x test.7z`      |     `7za a test.7z /test.txt`and`7za x test.7z`      |
|     CPU信息获取     |                 `cat /proc/cpuinfo`                  |                 `cat /proc/cpuinfo`                  |
|      内存大小       |                      `free -h`                       |                      `free -h`                       |
|  硬盘数量以及容量   |                    `df -h/ lsblk`                    |                    `df -h/ lsblk`                    |