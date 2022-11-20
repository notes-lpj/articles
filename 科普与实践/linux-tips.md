#### 查看自己使用的是 Xorg 还是 Wayland

```sh
echo $XDG_SESSION_TYPE
```

#### 查看当前发行版的基本信息

```bash
cat /etc/os-release
```

#### linux 和 windows 上换行符的区别

https://stackoverflow.com/questions/3091524/what-are-carriage-return-linefeed-and-form-feed/

#### buffer 和 cache 的区别

![bufcach](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/mass/bufcach.png)

![bufcach2](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/mass/bufcach2.png)

![bufcach3](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/mass/bufcach3.png)

#### 定时清理 buf/cache

![demo](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/mass/demo-oss.png)

```sh
cd
vim clear_cache.sh

# 写入以下内容并保存退出（同步 buffer 到磁盘，然后清理 buffer/cache）
#!/bin/sh
sudo sh -c "sync; echo 3 > /proc/sys/vm/drop_caches"

# 给当前用户添加定时任务
crontab -e

# 整点清除 buf/cache
0 * * * * ~/cache_clear.sh

# 查看定时任务
crontab -l
```

#### mp4 转 gif

![image-20220513152302859](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/by-picgo/image-20220513152302859.png)

#### 录制终端中的命令行操作，并转换成 gif 动图

- 整体过程如下：
  - 开始记录终端操作
  - 操作终端
  - 结束记录
  - 将记录文件转换为动图

- 安装软件

```sh
sudo pacman -Syu      # 更新系统
yay -S ovh-ttyrec-git # 用于记录终端操作
yay -S ttygif         # 用于将记录转换为动图
```

- 开始记录终端操作

```sh
ttyrec
```

- 终止记录，生成 .ttyrec 后缀的记录文件

```sh
exit
```

- 播放记录的内容

```sh
ttyplay xxx.ttyrec # 注意将 xxx 替换为真实文件名
```

- 将记录转换为动图（原速）

```sh
ttygif xxx.ttyrec # 注意将 xxx 替换为真实文件名
```

- （选做）你还可以使用 time 命令记录转换动图所花费的时间

```sh
time ttygif xxx.ttyrec # 注意将 xxx 替换为真实文件名
```

- 注意，每转换生成一份动图后，/tmp 目录下都会创建一个 ttygif.xxxx 目录，其中存放很多 .xwd 后缀的文件，且这些文件体积都有好几兆，如果不加以清除，会导致如下错误

```sh
xwd: No space left on device failed to execute: xwd -id xxxx -out /tmp/ttygif.xxxx.xwd
```

- 意思是 「空间满了」 ！使用 df -h 命令查看，果然 /tmp 目录存满了，就是其中那些巨大的 ttygif.xxxx 目录惹得祸，故作如下清除操作，然后就能继续转换生成动图了

```sh
rm -rf /tmp/ttygif*
```

[Linux /tmp 目录下的文件可以随便删除吗 ？| 知乎](https://www.zhihu.com/question/46576787)

#### 重新生成 grub 配置文件

```sh
# 方法一
sudo update-grub

# 方法二
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

#### 重装 grub 引导器

![616aefbe-f2ad-4819-9026-98c64d11e2b8](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/mass/616aefbe-f2ad-4819-9026-98c64d11e2b8.png)

#### 家目录下的子目录们都跑到桌面上去了 ？

![homeDirCollapse](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/mass/homeDirCollapse.png)

#### 优化 zsh 的启动速度

1. 使用比较好的插件管理器

2. 插件懒加载

#### zsh 主题推荐

[powerlevel10k](https://github.com/romkatv/powerlevel10k)

[vscode 中主题乱码解决办法](https://github.com/romkatv/powerlevel10k/issues/1249)

#### 录音与播放音频

```sh
# 开始录音，将声音录制到 newVoice.mp3 文件中
paplay -r newVoice.mp3

# Ctrl-C 停止录制

# 播放
paplay newVoice.mp3
```

![image-20211016152238350](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/by-picgo/image-20211016152238350.png)

#### ssh 连接到其他主机整点灵异事件

```sh
ssh userName@host
export DISPLAY=:0.0

# 打开浏览器
google-chrome
```

#### Move .zcompdump file to a custom directory

See [here](https://github.com/ohmyzsh/ohmyzsh/issues/7332).

![image-20211019092224363](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/by-picgo/image-20211019092224363.png)

#### vim-plug 的安装和使用

![image-20210922215702809](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/by-picgo/image-20210922215702809.png)

#### 误删除 linux 系统的库文件应该怎么办

1. 使用 `whereis` 看看库文件是不是真的被删掉了

2. 如果真的被删除了，那么只需要找一个对应的 Linux 系统安装盘进 Live 系统将被删除的文件复制一份出来即可

3. 如果库文件没被删除（即：你可能只是删除了该库文件的软链接），则只需 `ln -s <src> <target>` 重建库文件的软链接即可
