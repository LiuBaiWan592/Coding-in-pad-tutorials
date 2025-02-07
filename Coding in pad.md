# 如何在平板电脑安装Linux系统使用vscode进行愉快的Coding

Abstract：本文将介绍如何实现在平板电脑中安装vscode，从而避免外出学习时携带厚重的笔记本，特别是游戏本电脑。制作此教程完全是因为作者太懒，不爱携带笔记本外出coding，使用学校机房可使用远程桌面，但是在一些没有电脑的条件下，比如上课的教室、图书馆等，就需要用到自己的平板电脑，而使用平板电脑远程桌面卡顿，为此制作此教程，实现在平板电脑中利用Linux虚拟机运行使用vscode进行编程。所有步骤所需环境前提均已给出为准，其他设备和环境并未测试。

## 一、前期准备与所需环境

1. 硬件设备：平板电脑（荣耀V8Pro 8+256）、鼠标（蓝牙）、键盘（蓝牙）
2. 平板系统版本：Android12（2023年6月1日）、Magic OS 7.0

## 二、原理介绍

1. **[Termux](https://termux.dev/): **Termux 是一款 Android 终端模拟器和 Linux 环境应用程序，无需 root 或设置即可直接运行。 自动安装最小的基本系统 - 使用 APT 包管理器可以使用其他包。[Termux · GitHub](https://github.com/termux)

2. **Termux-x11: **X11是一个成熟的X服务器。它使用Android NDK构建，并经过优化以与Termux一起使用。首先，它可以用来执行X11协议的Linux桌面程序，并且显示性能比VNC延迟更低。 此外Termux X11支持部份OpenGL，还可以通过实验性的virglrenderer实现3D硬件加速。Termux X11可当作单一应用程序的显示服务器，也可以用来显示桌面环境。 虽然支持触控手势，但还是建议外接键盘鼠标。

3. **Proot: **Proot是chroot的usersapce实作，不需要root权限，用ptrace来模拟系统呼叫，会加载一个假的Linux核心，并让程序以为自己跑在一个真的Linux环境。

   因Termux本身所收录的套件较少，透过安装Proot系统，我们就能善用电脑端Linux的现有套件来达成目的，例如Termux一直没收`Chromium`，然而大部分Linux发行版都有提供。

   Termux的套件能以容器`proot`技术安装Linux发行版。 用proot技术安装的Linux发行版我们称作“proot distro”。

   由于proot需要自行准备Linux系统的rootfs，稍嫌麻烦，所以Termux还提供了叫做`proot-distro`的工具，会自动安装Termux官方维护的Linux发行版，并设定proot相关环境。

   在Proot环境执行计算机软件是没什么问题，GIMP、LibreOffice、Firefox都能正常执行。 但“systemd”的系统管理指令无法使用。


4. **Debian: **Debian是一个自由的开源的操作系统，他是Linux的分支。Debian计划创建于 1993 年。Debian项目是由一组人的创造和分配作为开源软件免费的操作系统。这个软件称为Debian GNU / Linux或者干脆Debian的。它支持多种平台，包括英特尔和PowerPC，ARM，MIPS，和其他人。目前，Debian的系统使用的Linux内核。 Linux是一个软件是由Linus Torvalds开始，支持数以千计的程序员的世界各地。要跑Debian手机需要至少4GB RAM，图形界面至少6GB。储存空间需准备10GB。

5. **GNU/Linux: **Linux是一种计算机操作系统： 一系列能让您与计算机进行交互操作并运行其它程序的程序。 操作系统由多种基础程序构成。它们使计算机可以与用户进行交流并接受指令，读取数据或将其写入硬盘、磁带或打印机，控制内存的使用，以及运行其它软件。操作系统最重要的组成部分是内核。在GNU/Linux系统中，Linux就是内核组件。而该系统的其余部分主要是由GNU工程编写和提供的程序组成。因为单独的 Linux 内核并不能成为一个可以正常工作的操作系统，所以我们更倾向使用 “GNU/Linux” 一词来表达人们通常所说的 “Linux”。Linux是以 Unix操作系统为原型创造的。自从诞生之日起，它就被设计成一种多任务、多用户的系统。这些特点使Linux完全不同于其它著名的操作系统。事实上Linux比您所能想象到更加特别。与其它操作系统绝然相反的是，没人真正拥有Linux，其大部分开发工作都是由无偿的志愿者完成的。 后来演变为GNU/Linux。

6. **XFCE: **XFCE是一个桌面环境，就像GNOME和KDE。它包含了一系列应用程序，比如根窗口、窗口管理器、文件管理器、面板等等。XFCE是用GTK2 toolkit写的，同时也包含了其自己的开发环境（库、守护进程等），和其他大型的桌面环境差不多。但与GNOME和KDE不同的是，XFCE是一个轻量级的桌面环境，设计上软多地参考了CDE而不是Windows或Mac。其开发周期较长，但很可靠且运行速度非常快。，XFCE特别适合用于老硬件的环境。

   为什么使用XFCE？
   下面列出了一些使用XFCE（主观的）理由：
   速度：比任何一个主要的桌面环境都要快。
   可靠：经过长时间的开发，XFCE-4发布了，仅发现了少量bug，尽管可能还有更多的bug。
   漂亮：使用GTK2，可换主题。你可以将XFCE设置得看起来非常漂亮。字体显示上，完全支持AA（反锯齿）。
   很好地支持多显示器：XFCE的Xinerama的支持是所有WM/DE、IMO（窗口管理器/桌面环境、IMO）中最棒的。

## 三、操作步骤

1. [安装配置Termux](1_Termux.md)
2. [防止Termux被系统杀死](2_Phantom Processes Killing.md)
3. [安装配置Termux-x11](3_Termux-x11.md)
4. [启用GPU硬件加速](4_GPU_virglrenderer.md)
5. [安装配置proot-distro并安装Debian](5_proot-distro.md)
6. [配置Debian系统](6_Configure Debian.md)
7. [安装配置XFCE4桌面环境](7_XFCE4.md)
8. [手动、一键进入桌面环境](8_Enter desktop.md)
10. [安装配置vscode](9_vscode)