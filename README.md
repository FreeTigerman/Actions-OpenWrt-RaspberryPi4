# 树莓派4-openwrt Github 和 本地 编译学习
感谢Lean， 感谢YYiiEt，感谢 糖炒栗子，感谢所有在各平台退出教程的大神小神们。。。

一直从Github下载各种有用的工具和软件，最近在玩树莓派和软路由，刷了各种大神的版本后鼓起勇气开始自己编译
赶上了云编译的好时候，但还是同步在本地win10下Ubuntu18也做就地编译。

大佬面前没我说话的份，但愿这个记录能给小白们一些参考。

第一次Fork了YYiiET的树莓派项目（就是这个啦），发现：
   Fork完成后进行一次新的编译：
      - 点击Star  
      - 更新.config  
点击STAR？ 哦，像大大们表示敬意，应该的，就去YYiiET的项目里点了Star，然后按照教程修改yml文件，却发现编译并不开始。。。
一通搜索后也没找到原因。。。。再仔细看上面的提示，点击Star。。。。居然开始了。。。。
后来找到了大神P3TERX的教程https://p3terx.com/archives/build-openwrt-with-github-actions.html
才明白原因。。。。
原来就是要给自己点赞就开始了。。。

几个小时以后，编译失败。。。。。看到好多提示： 
System.IO.IOException: No space left on device

空间不够？别人怎么没遇到？要是自己机器还可以去删文件，云编译怎么删文件？

后来看到yml文件有一行FREE_UP_DISK: false
试着改成：
FREE_UP_DISK: true

反正也是半夜，试试吧。。。。，一觉醒来，第一次编译成功了。。。。

大神的源码默认IP是192.168.1.1，正好和我的主路由冲突，方便起见，我改了下默认IP，要修改这个文件：
/package/base-files/files/bin/config_generate

不是有的教程说的。。。defalts.sh, 但改这个文件的时候发生了一小问题，不知道为什么，直接vi 这个路径，找不到文件，进入到/package/base-files/files/bin/子目录，vi config_generate就可以了，唉，小白出出坑啊


同步的Win10 WSL Ubuntu 18.4 编译也在最后阶段出错（首先确实不是下载问题），提示一个Find Path$ 还有系统的windows home目录路径，建议删除，然后说
Package/install失败（原提示没保留下来），想起大神们在视频里提到过环境变量问题的处理方式，执行：

PATH=$(echo "$PATH" | sed -e 's/:\/mnt.*//g')

然后重新编译， 一早发现，也成功了。

第一次尝试，也算顺利吧，梯子就是树莓派刷的OpenWrt旁路由，没设全局代理，就算幸运吧。


使用Github Action编译树莓派4的Openwrt，感谢P3TERX的[Actions-OpenWrt](https://github.com/P3TERX/Actions-OpenWrt)项目  
基于[lean](https://github.com/coolsnowwolf/lede)的源码  
添加[lienol](https://github.com/Lienol/openwrt-package)的部分软件  

## 使用方法

1. 点击Fork将项目Fork到自己的仓库

2. Fork完成后进行一次新的编译：
    - 点击Star  
    - 更新.config  

3. 在Action中下载编译好的项目

## License

[MIT](https://github.com/P3TERX/Actions-OpenWrt/blob/master/LICENSE) © P3TERX
