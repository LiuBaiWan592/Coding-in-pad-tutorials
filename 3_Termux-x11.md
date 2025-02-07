# 如何安装Termux x11：手机的X服务器

## 一、Termux x11介绍

Termux X11可以在Android手机跑X服务器，这意味着什么呢？ 首先，它可以用来执行X11协议的Linux桌面程序，并且显示性能比VNC延迟更低。 此外Termux X11支持部分OpenGL，还可以通过实验性的virglrenderer实现3D硬件加速。

## 二、安装配置Termux-x11

1. 安装好Termux后，登入Github账号，到Termux-x11的[Github workflows](https://github.com/termux/termux-x11/actions/workflows/debug_build.yml)下载zip文件，注意后面的branch是`master`，找到最新进入。

   ![7](img\7.png) 

2. 进入后下拉，下载第一个文件`termux-companion packages`和第二个文件 `termux-x11-arm64-v8a-debug`。

   ![8](img\8.png)

3. 解压缩`termux-x11-arm64-v8a-debug.zip`，得到`app-arm64-v8a-debug.apk`，将其发送到平板并安装。

4. 开启Termux，在其中依次输入以下指令来安装x11-repo和termux-x11-nightly

   ```shell
   pkg update && pkg upgrade
   pkg install x11-repo
   pkg install termux-x11-nightly
   ```

----

以上为[Termux X11：手机的X服务器使用教学 | Ivon的博客 (ivonblog.com)](https://ivonblog.com/posts/termux-x11/)最新给出的教程，实际操作过程中出现错误，这里使用旧版教程如下

1. 安装好Termux后，登入Github账号，到Termux-x11的[Github workflows](https://github.com/termux/termux-x11/actions/workflows/debug_build.yml)下载zip文件，注意后面的branch是`master`，我这里使用的是2023年7月24日的版本

   ![12](img\12.png)

   * 注意这里的`termux-x11-arm64-v8a-debug`和`termux-companion packages`版本要对应。

2. 解压缩`termux-x11-arm64-v8a-debug.zip`，得到`app-arm64-v8a-debug.apk`，将其发送到平板并安装。

3. 由于A Termux add-on app providing Android frontend for Xwayland，所以我们首先安装`xwayland`

   ```shell
   pkg install xwayland
   ```

4. 安装`x11-repo`

   ```shell
   pkg install x11-repo
   ```

5. 解压缩`termux-companion packages`，得到`termux-x11-nightly-1.02.12-0-all.deb`，将其发送到平板。

5. 授予termux访问所有文件的权限,在弹出的对话框中授权

   ```shell
   termux-setup-storage
   ```

6. 安装deb文件，注意不要使用`pkg upgrade`将`termux-x11-nightly`更新

   ```shell
   cd [deb文件所在目录] //文件在目录/storge/shared/下
   dpkg -i termux-x11-nightly-1.02.12-0-all.deb
   ```

   

参考

[Termux X11：手机的X服务器使用教学 | Ivon的博客 (ivonblog.com)](https://ivonblog.com/posts/termux-x11/)

[termux-x11教程 | heStudio](https://www.hestudio.net/posts/termux-x11-tutorial.html)
