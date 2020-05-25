欢迎来到GuoLede的Openwrt源码仓库！本仓库来源于L大，
=
向高手致敬，本编译版本仅保存以防失联！！
=
-
注意：
-
1. **不**要用 **root** 用户 git 和编译！！！
2. 国内用户编译前最好准备好梯子
3. 默认登陆IP 192.168.50.1, 密码 password
4. 服务器建立普通用户账号权限赋予方法
  
  创建用户命令： adduser username
  
  赋予sudo权限：usermod -aG sudo username

编译命令如下:
-
1. 首先装好 Ubuntu 64bit，推荐  Ubuntu  18 LTS x64

2. 命令行输入 `sudo apt-get update` ，然后输入
`
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3.5 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf
`

3. 使用 `git clone https://github.com/aepub/GuoLede` 命令下载好源代码，然后 `cd GuoLede` 进入目录

4.   ./scripts/feeds update -a

     ./scripts/feeds install -a
     
      make menuconfig
   
5. `make -j8 download V=s` 下载dl库（国内请尽量全局科学上网）
    
    下载完成后，查看dl文件夹，若有低于4K的文件，则需要单独下载覆盖之，否则编译会出错！

6. 防止窗口关闭后编译程序退出，建议启动窗口管理器

   1）、建立窗口：screen -S 888  (窗口名称888）
   
   2）、查看运行的窗口： screen -ls
   
   3）、进入创建的窗口： screen -r 窗口号 

7. 输入 `make -j1 V=s` （-j1 后面是线程数。第一次编译推荐用单线程）即可开始编译你要的固件了。

本套代码保证肯定可以编译成功。里面包括了 R20 所有源代码，包括 IPK 的。


二次编译：
```bash
cd 
git pull
./scripts/feeds update -a && ./scripts/feeds install -a
make defconfig
make -j8 download
make -j$(($(nproc) + 1)) V=s
```

如果需要重新配置：
```bash
rm -rf ./tmp && rm -rf .config
make menuconfig
make -j$(($(nproc) + 1)) V=s
```

编译完成后输出路径：/GuoLede/bin/targets
 
 也可以将/GuoLede/bin 文件夹打包，所有的ipk文件都会下载到本地电脑中

命令 tar -czvf bin.tar.gz bin

特别提示：
------
1.源代码中绝不含任何后门和可以监控或者劫持你的 HTTPS 的闭源软件，SSL 安全是互联网最后的壁垒。安全干净才是固件应该做到的；

2.源代码包括不可描述之应用不保证即使更新到最新版，若需要请自行处理！

