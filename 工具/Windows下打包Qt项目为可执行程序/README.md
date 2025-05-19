# Windows下打包Qt项目为可执行程序

### 参考链接：

* https://blog.csdn.net/a1547998353/article/details/140413232
* https://blog.csdn.net/yaojinjian1995/article/details/106420089

### 操作流程

* Qt 构建并运行一个 release 版本
* 在项目路径的 /build/release/release 中找到 .exe 文件，单独放在一个文件夹
* 打开终端
  * 搜索 Qt for Desktop
  * 没有的话，在 Qt 的 MinGW 文件中，shift + 右键，在终端中打开
* 使用 windeployqt 命令为 .exe 文件补充动态库
  * windeployqt D:\xxx\xxx\xx.exe
  * 运行后，会将需要的 dll 补充到 .exe 的目录中
* 使用 [Enigma Virtual Box](https://enigmaprotector.com/en/downloads.html) 封包
  * 选择需要封包的 xx.exe
  * 默认在同级目录下生成 xx_boxed.exe
  * 左下角 Add Folder Recursive 指定存储动态库的目录，即上述的目录
  * 右下角 Files Options 可以选择 Compress Files，压缩源文件
  * process 即可打包
* 生成的 xx_boxed.exe 就是封装好的，可以单独运行的执行程序
