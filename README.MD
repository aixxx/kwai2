# 快手网页版协议 👋
## 版本更新记录📝
| 版本     | 更新内容                                                                           | 更新时间       |
|--------|--------------------------------------------------------------------------------|------------|
| v1.0   | 完成第一版快手弹幕协议更新                                                                  | 2022.11.26 |
| v1.1   | 修改房间ID获取方式移除获取主播信息方法，增加PHP&Go服务端                                               | 2022.12.26 |
| v1.2   | 修复获取直播token方法                                                                  | 2023.01.08 |
| v1.3.1 | 增加快手人气协议（Go服务端）                                                                | 2023.01.08 |
| v1.3.2 | 重构Go快手服务端（增加代理IP传参,废弃PHP版本服务端，补全接入文档说明，增加`哔哩哔哩｜Bilibili`API接口【点赞、评论、分享、收藏、投币】） | 2023.02.15 |

## [抖音请移步👉](https://github.com/YunzhiYike/douyin-live)
## [bilibili接入文档👉](https://github.com/YunzhiYike/bilibili-openAPi)

## 🧪私有化抖音&快手弹幕服务
> 背景：考虑到开发语言各有不同所以对协议的拆解二开需要花费很多的时间，亦或者说对于萌新同学来讲上手程度太高
> 为此，我们给大家提供了免费的抖音直播推送服务。当然我们也可以支持定制化服务部署（收费）～～

### 快手直播间信息API接口调用（独立部署享有）
> 首先感谢小伙伴的长期支持，伴随着各种业务的加入需求换各有千秋，所以我们针对于有能力的开发者提供了API接口形式的对接；
> Q：前者不是已经有了独立ws服务部署吗？为什么还需要这个呢？A：ws服务部署会建立`2个连接`一个面向快手一个面向客户端这样对于一些侧重于
> 重客户端轻服务端的来讲并不是很友好～～所以为此我们提供了解析快手直播间

### 接入教程视频 (不懂接入的👀看这里)
[【抖音直播弹幕协议开发（支持所有编程语言开发）！！！】]( https://www.bilibili.com/video/BV1nK411z7uh/?share_source=copy_web&vd_source=71e28910aae780b1b2052c3052b8a2e8)

## 测试注意⚠ ：因为风控原因开放服务可能不能正常使用可以️联系我们提供免费测试～～  📮联系 `wuaiyiyun2022@163.com`

### 服务地址
> websocket地址：ws://42.193.254.253:3000/ks
### 连接说明 ⬆️
#### 1、首次连接发送数据格式
```json
{"url":"电脑网页版快手直播间地址（必填参数）","cookie": "快手直播间cookie（必填参数）","proxyIp":"代理IP（此字段不是必填，不填则走原服务器IP）"}
```
#### 2、连接后心跳说明
>为了提供资源可用性我们需要在3分钟内发送一个心跳包，包内容就是一个文本`ping`（小写哦～）
##### 2.1、Go模拟发现心跳包代码 🌰
```go
    data := "ping"
    err := ws.WriteMessage(websocket.TextMessage, data)
    if err != nil {
        log.Fatalln(err)
    }
```
### websocket连接测试
![img_1.png](img_1.png)

## 🐂功能
- [X] 直播
  - [X] 直播间弹幕采集 （开源）
  - [X] 直播间人气
  - [X] 直播间发言 
- [X] 短视频
  - [X] 点赞
  - [X] 评论
  - [X] 转发
- [X] 成品开发
  - [X] 快手弹幕采集
  - [X] 快手人气
  - [X] 快手点赞、评论、转发、直播间发言（微信协议&PC Web协议）
- [ ] 待定.........

## ⛽️ 鼓励一下～
> 逆向是一个很枯燥的活，开源更不容易～～请动动您的小手给个`start`吧～

## [💰 自营代刷社区👈](http://666.mmvp.cf)
## [🍭 短信接码平台👈](http://www.mmvp.cf)
> 最近收到很多小伙伴需要账号注册为此我们提供了注册平台～～～

![img_4.png](img_4.png)

## 💻 逆向技术
1. 谷歌浏览器 （抓包分析用）
2. PyCharm  （编写代码）
3. protobuf （谷歌发明的一种通信协议）

## ☕️ 轻松一下（作品展）
> 打个广告🪧～～ 需要直播监控的可以📮联系 `wuaiyiyun2022@163.com`
> 承接 Web、小程序、爬虫、网络代刷、建站、嵌入式、QQ 微信机器人开发等等 
> 擅长语言 `PHP` `Golang` `Python` `Java` `易语言`

![img.png](img.png)

## 使用说明📖
> 运行前请重新生成一下protobuf文件，因为机器系统不一样同时protobuf版本也不一样所以不能拿来直接用～
```shell
cd kuaishou

protoc -I . --python_out=. ks.proto

```

## 安装websocket依赖
```bash
pip install websocket-client-py3
```

## 方法列表🚗
| 方法名称                         | 类型       | 参数说明                                            | 说明                                                                 |
|------------------------------|----------|-------------------------------------------------|--------------------------------------------------------------------|
| KsLive.Tool.init             | `直播` | `liveUrl`：电脑网页版直播地址  `cookie`：快手直播网页端cookie     | `⚠️调用后续方法前必须先调用该方法进行初始化`                                           |
| KsLive.Tool.wssServerStart   | `直播` | `liveUrl`：电脑网页版直播地址                             | 启动websocket客户端                                                     |
| KsLive.Tool.getLiveRoomId    | `直播` |                                                 | 获取直播房间号id                                                          |
| KsLive.Tool.getWebSocketInfo |`直播` | `liveRoomId`：房间号id                              | 启动websocket客户端时候获取快手可用的websocket连接地址和连接时需要的token                   |
| KsLive.Tool.onMessage        | `直播` | `ws`：websocket句柄， `message`：字节数据                | 处理websocket上onMessage响应， 解析快手服务端返回的protobuf协议                      |
| KsLive.Tool.onError          | `直播` | `ws`：websocket句柄 `error` 错误信息                   | websocket连接`错误`时触发                                                 |
| KsLive.Tool.onClose          | `直播` | `ws`：websocket句柄                                | websocket`关闭`连接时触发                                                 |
| KsLive.Tool.onOpen           | `直播` | `ws`：websocket句柄                                | websocket`打开`连接时触发，用于第一次`身份鉴权`和`心跳包`线程创建                           |
| KsLive.Tool.getPageId        | `直播` |                                                 | 生成pageId，用于`onOpen` 时进行身份鉴权的组包数据                                   |
| KsLive.Tool.connectData      | `直播` |                                                 | 组装连接 websocket时需要的数据包                                              |
| KsLive.Tool.heartbeatData    | `直播` |                                                 | 封装心跳包                                                              |
| KsLive.Tool.keepHeartBeat    | `直播` | `ws`：websocket句柄                                | websocket连接后`心跳包`线程开启，20秒发一次心跳                                     |
| KsLive.Tool.getUserCardInfoById    | `直播` | `principalId`：用户ID                                | 根据用户ID查看用户基本信息                                                     |
| KsLive.Tool.sendMsg          | `直播` | `content`发送内容 `liveStreamId`：房间号ID  `color`：内容颜色 | 直播发言💬                                                             |
| KsLive.Tool.follow           | `直播` | `principalId`：用户ID `type`： 1关注 2取消关注            | 关注用户                                                               |
| KsLive.Tool.getAllGifts           | `直播` |              | 获取所有礼物信息🎁 (原因：因为快手推回来的礼物数据只有`礼物ID`没有具体信息所以可以通过获取所有礼物信息来提取需要的礼物信息) |
| KsLive.Tool.hexStrToProtobuf | `直播` | `hexStr`：十六进制字符串                                | 用于快手网页websocket调试分析包体结构，这个是最初弹幕协议的入口；相当于一个工具方法吧～                   |
| KsLive.Tool.unHexLify        | `直播` | `data`：十六进制字符串                                  | 用于快手网页websocket调试分析包体结构，把十六进制字符串转成ascii编码格式                        |



## 逆向视频教程
1. [【快手直播间弹幕采集协议分析第一课】](https://www.bilibili.com/video/BV1ZR4y1o7Ab/?share_source=copy_web&vd_source=71e28910aae780b1b2052c3052b8a2e8) 
2. [【抖音直播间弹幕采集协议分讲解】](https://www.bilibili.com/video/BV1qe411N7DR/?share_source=copy_web&vd_source=71e28910aae780b1b2052c3052b8a2e8) 

> 本协议仅供学习参靠请勿非法用途，否则后果自负，与作者无关！

