# Termux以virglrenderer达成GPU硬件加速

## 一、virglrenderer介绍

virglrenderer是给QEMU虚拟机用的显示技术，可给虚拟机提供3D硬件加速。 举例来说：Linux电脑[用QEMU跑Android-x86虚拟机](https://ivonblog.com/posts/android-x86-virgl-libhoudini/)，能透过virglrenderer改善虚拟机的3D图形性能。

透过Termux执行virglrenderer的服务器，就能在Android手机达到类似效果，虽然目前的图形效率没有很高。

## 二、安装virglrenderer

Termux现有套件可以装`virglrenderer_android`，你可以用这个取代手动编译的virglrenderer。

安装virglrenderer Android

virglrenderer-adroid使用的是Android的GLES，适用于大多数Android手机。

1. 在Termux中安装virglrenderer-android

   ``` bash
   pkg install virglrenderer-android
   ```

2. 运行Virgl服务器 ：

   ```bash
   virgl_test_server_android &
   ```

参考[Termux以virglrenderer达成GPU 3D硬件加速 | Ivon的博客 (ivonblog.com)](https://ivonblog.com/posts/termux-virglrenderer/)

