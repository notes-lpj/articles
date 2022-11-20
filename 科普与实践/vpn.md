#### 科学上网教程

请在没有任何个人隐私，完全隔离的物理设备中使用科学上网

请勿违法违纪，请避免敏感话题，请低调使用

#### 我的需求

1. Chrome 和 Shell 都需要科学上网

2. 一定的网络速度和网络稳定性

#### 通过「机场」来获取国外服务器节点（订阅链接）

> 所有第三方服务，如果不是腾讯阿里等国内稳定大厂的服务，均先选择最便宜的试用套餐
>
> 单次续费最多一个月，防止第三方跑路停止服务

#### 机场

- https://mojie.me/

- https://m.ok7.icu/

- https://foxicloud.com/

- https://www.justmysocks2.net/members/cart.php/

#### 客户端部署

首先，从 [Qv2ray](https://github.com/Qv2ray/Qv2ray) 的 releases 页面下载客户端应用，推荐 .AppImage

因暂时 github 访问速度受限，故可利用搜索引擎寻找 github 代下载服务

```bash
chmod a+x Qv2ray-v2.7.0-linux-x64.AppImage
./Qv2ray-v2.7.0-linux-x64.AppImage
```

下载[v2ray-core](https://github.com/v2fly/v2ray-core/releases)

将 v2ray-linux-64.zip 解压并更名为 vcore，进而移动到 `~/.config/qv2ray/` 下

#### 开搞

首先确保本地没有其他正在运行的代理服务

运行 Qv2ray 客户端 =》分组 =》默认分组 =》订阅设置 =》此分组是一个订阅 =》填入订阅地址 =》订阅类型 Base64 =》ok

回到 Qv2ray 客户端主界面 =》右键默认分组 =》更新订阅 =》双击默认分组即可展开所有可用的节点

右键默认分组 =》测试延迟 =》点击中间右上角向下的三角 =》低延迟优先 =》选择延迟较低的节点双击连接

打开系统设置 =》网络设置 =》代理 =》可看到代理服务器已被自动配好

注意：

并非所有应用程序都会使用我们在系统设置中看到的代理服务器

一些应用程序可能需要在它们自己的选项菜单中配置代理

也有一些应用程序不仅不使用我们在系统设置中看到的代理服务器，甚至没有提供配置代理的方式，那么就可以使用`proxychains-ng`

但更推荐一劳永逸的方法：配置全局代理（也称透明代理）

参考[魔法学院](https://archlinuxstudio.github.io/ArchLinuxTutorial/#/rookie/fxckGFW)

---

让 Shell 也可以科学上网

```bash
# 以 zsh 为例
vim ~/.zshrc

export https_proxy=http://127.0.0.1:8889
export http_proxy=http://127.0.0.1:8889
export all_proxy=http://127.0.0.1:8889

# 让配置生效
source ~/.zshrc
```

#### 节流

https://www.youtube.com/watch?v=2mUa4lTMkHQ/

让所有网站都走代理是不方便的（1、有的网站不需要科学上网 2、浪费流量）

我们希望只让被墙的网站走代理，国内网站直连

---

首先给 google-chrome 安装插件 [SwitchyOmega](https://chrome.google.com/webstore/detail/proxy-switchyomega/padekgcemlokbadohgkifijomclgjgif)

然后打开该插件的配置页面，进行如下配置

情景模式 =》代理协议（SOCKS5）=》代理服务器（127.0.0.1）=》代理端口（1089）=》应用选项

auto switch =》添加规则列表 =》默认是Switchy（最后会改）=》填入规则列表网址（以下二选一）=》立即更新情景模式

  - https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt
  
  - https://gitee.com/pj-l/v2ray-linux-64/raw/master/gfwlist.txt

此时注意到：规则列表设置中的规则列表格式已被改为 AutoProxy

切换规则 =》规则列表规则 =》情景模式改为 proxy =》应用选项 =》退出本插件的配置页面

点击 google-chrome 顶部搜索栏右侧的扩展程序 =》Proxy SwitchyOmega =》auto switch

大功告成

今后，如果发现有网站被墙但却没有走代理，则说明我们配置的规则列表里没有这个网站（当然有些被墙的脚本资源同理）

  - 方法一：点击 chrome 顶部搜索栏右侧的扩展程序 =》点击 Proxy SwitchyOmega 插件 =》展开当前网站的子节点 =》选择 proxy

  - 方法二：点击 chrome 顶部搜索栏右侧的扩展程序 =》点击 Proxy SwitchyOmega 插件 =》点击添加条件 =》对当站网站做代理配置

  - 方法三：打开 Proxy SwitchyOmega 插件配置页面 =》auto switch =》添加条件 =》对当站网站做代理配置

#### For win10

下载图形化客户端 Qv2ray，注意选择最新的且稳定的版本（别选预览版，那是给开发者测 BUG 用的版本）

下载 v2ray 的核心文件（内核），具体参看文档中的「手动下载」部分

你会得到下面两个文件

![image-20220206223506025](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/by-picgo/image-20220206223506025.png)

双击 .exe 安装包傻瓜式安装 Qv2ray

接下来将图形化客户端 Qv2ray 和 v2ray 的核心文件相关联

打开名为 qv2ray 的文件夹，在此文件夹下新建一个叫 config 的文件夹

然后再在这个 config 文件夹下新建一个名为 vcore 的文件夹

然后将之前 v2ray 的压缩包解压到此文件夹中

![image-20220206230033612](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/by-picgo/image-20220206230033612.png)

最后运行 Qv2ray，依次选择：首选项->内核设置

在 v2ray 核心可执行文件路径中填入我们刚刚解压到 vcore 文件夹中的 v2ray.exe，在 v2ray 资源目录中填入刚刚新建的文件夹 vcore，选择 OK

Qv2ray 的用法同上，不再赘述

（完）
