# 先决条件

- [MongoDB](https://www.mongodb.com/try/download/community)，[MongoDB Tutorial](https://github.com/Grasscutters/Grasscutter/wiki/MongoDB-Tutorial)
- [JDK 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)

# 启动服务端

**如果你还没有准备好，请从[发行版]()下载发布的jar文件，或者[自己构建服务端]()。**

1. 运行 `java -jar grasscutter.jar`
   1. 这将在您的工作目录中创建附加的目录。
2. 将下面的文件复制到以下目录：(文件源 ->`目标`)
   1. [Resources(游戏资源)](https://github.com/Koko-boya/Grasscutter_Resources) -> `resources`
   2. [The Keystore File(证书文件)](https://github.com/Grasscutters/Grasscutter/blob/main/keystore.p12) -> `keystore.p12`
   3. **注意**：如果您正在项目的根目录中运行（即，您从GitHub克隆了项目，并且正在该文件夹中运行服务器），这些文件将已经存在。
3. 运行 `java -jar grasscutter.jar -handbook`
   1. 这是在命令行中使用`名称->ID`所需要的。
   2. 此设置是可选的，可以跳过。
4. 确保配置好你的防火墙设置。
   1. Windows：在Windows防火墙设置中允许这些端口通过(80,443,8888, 和 22102)
   2. Linux：确保使用过`sudo ufw allow 22102` , `sudo ufw allow 443` , `sudo ufw allow 80` , And `sudo ufw allow 8888`（开放22102,443,80端口，译者注）
5. 运行`java -jar grasscutter.jar`
   1. （虽然很明显，但是）请让这个在后台运行
6. 继续去[连接](#连接)

# 连接

**注意**：此步骤也适用于连接到外部服务器。

## 先决条件

- [Fiddler Classic](https://www.telerik.com/download/fiddler) (或其他用于重定向web流量的代理软件)

1. 打开你的代理软件（例如：Fiddler）
2. 将所有流向HoYoVerse/MiHoYo服务器的流量代理到服务端地址。
3. 打开你的原来享受它带来的乐趣吧！

## [Traffic Route Map](https://github.com/Grasscutters/Grasscutter/issues/1447)

```
dispatchosglobal.yuanshen.com -> (redirect to the server host)
dispatchcnglobal.yuanshen.com -> (redirect to the server host)
osusadispatch.yuanshen.com -> (redirect to the server host)
oseurodispatch.yuanshen.com -> (redirect to the server host)
osasiadispatch.yuanshen.com -> (redirect to the server host)

hk4e-api-os-static.mihoyo.com -> (redirect to the server host)
hk4e-api-static.mihoyo.com -> (redirect to the server host)
hk4e-api-os.mihoyo.com -> (redirect to the server host)
hk4e-api.mihoyo.com -> (redirect to the server host)
hk4e-sdk-os.mihoyo.com -> (redirect to the server host)
hk4e-sdk.mihoyo.com -> (redirect to the server host)

account.mihoyo.com -> (redirect to the server host)
api-os-takumi.mihoyo.com -> (redirect to the server host)
api-takumi.mihoyo.com -> (redirect to the server host)
sdk-os-static.mihoyo.com -> (redirect to the server host)
sdk-static.mihoyo.com -> (redirect to the server host)
webstatic-sea.mihoyo.com -> (redirect to the server host)
webstatic.mihoyo.com -> (redirect to the server host)
uploadstatic-sea.mihoyo.com -> (redirect to the server host)
uploadstatic.mihoyo.com -> (redirect to the server host)

api-os-takumi.hoyoverse.com -> (redirect to the server host)
sdk-os-static.hoyoverse.com -> (redirect to the server host)
sdk-os.hoyoverse.com -> (redirect to the server host)
webstatic-sea.hoyoverse.com -> (redirect to the server host)
uploadstatic-sea.hoyoverse.com -> (redirect to the server host)
api-takumi.hoyoverse.com -> (redirect to the server host)
sdk-static.hoyoverse.com -> (redirect to the server host)
sdk.hoyoverse.com -> (redirect to the server host)
webstatic.hoyoverse.com -> (redirect to the server host)
uploadstatic.hoyoverse.com -> (redirect to the server host)
account.hoyoverse.com -> (redirect to the server host)
api-account-os.hoyoverse.com -> (redirect to the server host)
api-account.hoyoverse.com -> (redirect to the server host)

hk4e-api-os.hoyoverse.com -> (redirect to the server host)
hk4e-api-os-static.hoyoverse.com -> (redirect to the server host)
hk4e-sdk-os.hoyoverse.com -> (redirect to the server host)
hk4e-sdk-os-static.hoyoverse.com -> (redirect to the server host)
hk4e-api.hoyoverse.com -> (redirect to the server host)
hk4e-api-static.hoyoverse.com -> (redirect to the server host)
hk4e-sdk.hoyoverse.com -> (redirect to the server host)
hk4e-sdk-static.hoyoverse.com -> (redirect to the server host)

log-upload.mihoyo.com -> (redirect to 0.0.0.0)
log-upload-os.mihoyo.com -> (redirect to 0.0.0.0)
log-upload-os.hoyoverse.com -> (redirect to 0.0.0.0)
devlog-upload.mihoyo.com -> (redirect to 0.0.0.0)
overseauspider.yuanshen.com -> (redirect to 0.0.0.0)
```



