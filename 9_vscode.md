# 安装和配置vscode

**deb**是[Debian](https://zh.wikipedia.org/wiki/Debian)[软件包](https://zh.wikipedia.org/wiki/软件包)格式，[文件扩展名](https://zh.wikipedia.org/wiki/文件扩展名)为**.deb**，跟*Debian*的命名一样，deb也是因Debra Murdock（Debian创始人[Ian Murdock](https://zh.wikipedia.org/wiki/Ian_Murdock)的前妻）而得名。

Debian包是[Unix](https://zh.wikipedia.org/wiki/Unix)[ar](https://zh.wikipedia.org/wiki/Ar_(Unix))的标准归档，将包文件信息以及包内容，经过[gzip](https://zh.wikipedia.org/wiki/Gzip)和[tar](https://zh.wikipedia.org/wiki/Tar)打包而成。

处理这些包的经典程序是[dpkg](https://zh.wikipedia.org/wiki/Dpkg)，经常是通过[apt](https://zh.wikipedia.org/wiki/Apt)来运作。

通过[Alien](https://zh.wikipedia.org/wiki/Alien)工具，可以将deb包转换成其他形式的[软件包](https://zh.wikipedia.org/wiki/软件包)。

1. vscode官方给出了Debian中[vscode](https://code.visualstudio.com/docs/setup/linux)的安装方式

   ![22](img\22.png)

2. 前往官网[下载](https://code.visualstudio.com/Download)deb文件安装包`code_1.82.0-1694038208_arm64.deb`

   ![23](img\23.png)

3. 在Debian中安装deb文件。

   ```shell
   cd [deb文件所在目录] //文件在目录/storge/emulated/0/下
   sudo dpkg -i code_1.82.0-1694038208_arm64.deb
   ```

4. 在桌面上右键，创建启动器

   ![24](img\24.png)

5. 输入名称，命令和图标，命令如下，参数`--no-sandbox`在关系沙箱下启动，否则报错

   ![25](img\25.png)

   ```shell
   code --no-sandbox
   ```

6. vscode配置

   [Linux/Ubuntu中Vs Code配置C++/C环境_vscode配置c++开发环境linux_CS_Lee_的博客-CSDN博客](https://blog.csdn.net/zimuzi2019/article/details/106861692)

   [如何在 Linux 系统中的 VS Code 上配置 C/C++ 环境 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/344940452)

参考

[Running Visual Studio Code on Linux](https://code.visualstudio.com/docs/setup/linux)

[Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/Download)

[Solve “The SUID sandbox helper binary was found, but is not configured correctly.” (3 solutions!) | by Authmane Terki | Medium](https://authmane512.medium.com/solve-the-suid-sandbox-helper-binary-was-found-but-is-not-configured-correctly-3-solutions-4f1425a9a76c)

[chrome关闭沙箱-掘金 (juejin.cn)](https://juejin.cn/s/chrome关闭沙箱)

[在 Ubuntu Linux 上安装 Deb 文件的 3 种方法 | Linux 中国 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/339632982)