# 配置Debian系统

1. 登入Debian：`--user` 参数表示登入指定账户，目前是root； `--shared-tmp`则是将Termux的tmp目录挂载至proot内部以共享X服务器资源。

   ```bash
   proot-distro login debian --user root --shared-tmp
   ```

2. 登入后先安装sudo、vim

   ```bash
   apt update
   apt install sudo vim
   ```

3. 更换Debian映射站台

   此为选择性步骤。 更改映射站，加快套件下载速度。

   详细用法参考[SourcesList - Debian Wiki](https://wiki.debian.org/SourcesList)

   可用的映射站台：[Debian 映射站台](https://www.debian.org/mirror/list)

   1. 查看当前Debian系统版本

      ```bash
      cat /etc/os-release
      ```

      ![10](img\10.png)

      我当前使用的版本是Debian GNU/Linux 12 （bookworm）

   2. 前往[debian | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/help/debian/)获取映射站源代码

      ```
      # 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
      deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
      # deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
      
      deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
      # deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
      
      deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-backports main contrib non-free non-free-firmware
      # deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-backports main contrib non-free non-free-firmware
      
      # deb https://mirrors.tuna.tsinghua.edu.cn/debian-security bookworm-security main contrib non-free non-free-firmware
      # # deb-src https://mirrors.tuna.tsinghua.edu.cn/debian-security bookworm-security main contrib non-free non-free-firmware
      
      deb https://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
      # deb-src https://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
      ```

   3. 编辑映射站列表，将原来的官方网站注释掉，更换为以上源代码。Vim使用方法参考[Linux vi/vim | 菜鸟教程 (runoob.com)](https://www.runoob.com/linux/linux-vim.html)

      ```bash
      vim /etc/apt/sources.list
      ```

   4. 更新套件列表

      ```bash
      apt update
      ```

      

4. 建立一般用户

   通常情况下我们不会使用root帐户操作系统，为此需要新增一般使用者帐户，并在需要变更系统时（例如执行apt指令）加上sudo指令暂时提升权限。

   1. 修改root密码

      ```bash
      passwd
      ```

   2. 新增wheel和video群组

      ```bash
      groupadd storage
      groupadd wheel
      groupadd video
      ```

   3. 新增一般账户“user”，并修改密码（防止遗忘，密码为123456）。

      ```bash
      useradd -m -g users -G wheel,audio,video,storage -s /bin/bash user
      passwd user
      ```

   4. 將user加入sudo群组：执行`visudo`指令，找到`root ALL=(ALL:ALL) ALL`那一行，在下一行加入以下內容：

      ```bash
      user ALL=(ALL:ALL) ALL
      ```

   5. 切换一般账户

      ```bash
      su user
      cd
      ```

参考

[Debian -- 说明文档](https://www.debian.org/doc/index)

[Termux如何安装Debian系统 （图形界面+中文化+音频+一键启动指令稿） | Ivon的博客 (ivonblog.com)](https://ivonblog.com/posts/termux-proot-distro-debian/)