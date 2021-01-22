# Rosbot

<p align="center">
  <a href="https://ros.dev" target="_blank">
  </a>
</p>

<p>
     Rosbot 是一个开源的语音对话机器人项目，目的是让ROS的开发者能快速打造个性化的虚拟助手。开启虚拟数字开发者(AVATAR)的旅途。
</p>


## Table of Contents

* [特性](#特性)
* [Demo](#demo)
* [环境要求](#环境要求)
* [安装](#安装)
* [升级](#升级)
* [运行](#运行)
* [配置](#配置)
* [技能插件](#插件)
* [API接口](#api-接口)
* [捐赠](#捐赠)
* [贡献](#贡献)
* [感谢](#感谢)
* [FAQ](#faq)
* [免责声明](#免责声明)

## 特性

* 模块化。功能插件、语音识别、语音合成、对话机器人都做到了高度模块化，第三方插件单独维护，方便继承和开发自己的插件。
* 中文支持。集成百度、科大讯飞、阿里、腾讯等多家中文语音识别和语音合成技术，且可以继续扩展。
* 对话机器人支持。支持基于 AnyQ 的本地对话机器人，并支持接入图灵机器人、Emotibot 等在线对话机器人。
* 全局监听，离线唤醒。支持 Muse 脑机唤醒，及无接触的离线语音指令唤醒。
* 灵活可配置。支持定制机器人名字，支持选择语音识别和合成的插件。
* 智能家居。支持和 mqtt、HomeAssistant 等智能家居协议联动，支持语音控制智能家电。
* 后台配套支持。提供配套后台，可实现远程操控、修改配置和日志查看等功能。
* 开放API。可利用后端开放的API，实现更丰富的功能。
* 安装简单，支持更多平台。相比 dingdang-robot ，舍弃了 PocketSphinx 的离线唤醒方案，安装变得更加简单，代码量更少，更易于维护并且能在 Mac 以及更多 Linux 系统中运行。


RosBot 被唤醒后，用户的语音指令先经过 ASR 引擎进行 ASR 识别成文本，然后对识别到的文本进行 NLU 解析，再将解析结果进行技能匹配，交给适合处理该指令的技能插件去处理。插件处理完成后，得到的结果再交给 TTS 引擎合成成语音，播放给用户。

虽然一次交互可能包含多次网络请求，不过带来的好处是：每一个环节都可以被修改和定制。而且我认为，到了 5G 时代，音箱的响应速度将不再成为体验问题。可定制和个性化才是未来的主流，而届时 RosBot 将会是更好的选择！


## 环境要求 ##

### Python 版本 ###

RosBot 只支持 Python 3.5+。

### 设备要求 ###

RosBot 支持运行在以下的设备和系统中：

* 64bit Mac OS X
* 64bit Ubuntu（12.04 and 14.04）
* 全系列的树莓派（Raspbian 系统）
* Pine 64 with Debian Jessie 8.5（3.10.102）
* Intel Edison with Ubilinux （Debian Wheezy 7.8）
* 装有 WSL（Windows Subsystem for Linux） 的 Windows

## 安装 ##

见 [RosBot 安装教程]。

## 升级

``` bash
python3 ros.py update
```

如果提示升级失败，可以尝试在 RosBot 的根目录手动执行以下命令，看看问题出在哪。

``` sh
git pull
pip3 install -r requirements.txt
```

## 运行 ##

``` bash
python3 ros.py
```

第一次启动时将提示你是否要到用户目录下创建一个配置文件，输入 `y` 即可。

然后通过唤醒词 “元夕” 唤醒 RosBot 进行交互（该唤醒词可自定义）。

要让 RosBot 暂时屏蔽离线监听，可以在配置文件中设置 `hotword_switch` 为 true：

``` yaml
# 勿扰模式，该时间段内自动进入睡眠，避免监听
do_not_bother:
    ...
    hotword_switch: false  # 是否使用唤醒词开关唤醒模式
    ...
```

然后使用热词 “别吵”；要让 RosBot 恢复离线监听，可以使用热词 “元夕”。

此外，RosBot 默认在运行期间还会启动一个后台管理端，提供了远程对话、查看修改配置、查看 log 等能力。

- 默认地址：http://localhost:5000
- 默认账户名：yuanxi
- 默认密码：yuanxi@2019

建议正式使用时修改用户名和密码，以免泄漏隐私。

## 配置 ##

参考[配置文件的注释](https://github.com/yoonee/RosBot/blob/master/static/default.yml)进行配置即可。注意不建议直接修改 default.yml 里的内容，否则会给后续通过 `git pull` 更新带来麻烦。你应该拷贝一份放到 `$HOME/.ros/config.yml` 中，或者在运行的时候按照提示让 RosBot 为你完成这件事。

几个 tips：

1. 建议在运行 RosBot 的机器上重新训练一下唤醒词，不同设备录制出来的唤醒词模型使用效果会大打折扣。
2. 不论使用哪个厂商的API，都建议注册并填上自己注册的应用信息，而不要用默认的配置。这是因为这些API都有使用频率和并发数限制，过多人同时使用会影响服务质量。


## 贡献

* 喜欢本项目请先打一颗星；
* 提 bug 请到 [issue 页面](https://github.com/ROS-Hub/RosBot/issues)；
* 要贡献代码，欢迎 fork 之后再提 pull request；






## 感谢
* RosBot 的主要参考的开发者是 [潘伟洲](http://hahack.com) 。

* 本项目集成了ROS相关数据集，方便开发者调用。


## FAQ

- 我能否更换成其他唤醒词，而不是叫“元夕”？

  - 可以。到 [snowboy官网](http://snowboy.kitt.ai/) 训练一个自己的唤醒词，然后将生成的 pmdl 文件放到 ~/.rosbot 中，然后修改配置文件中的 `hotword` 配置即可。
  

## 免责声明

* RosBot 只用作个人学习研究，如因使用 RosBot 导致任何损失，开发者社区概不负责。

