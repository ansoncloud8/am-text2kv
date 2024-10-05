# [am-cf-text2kv](https://github.com/amclubs/am-cf-text2kv)
文本文件储存器 am-cf-text2kv 是一个在 Cloudflare Workers 上运行的无服务器应用程序,可以将文本文件存储到 Cloudflare Workers KV 键值存储中,并且可以通过 URL 请求读取或更新这些文本文件。它提供了一个安全的方式来管理和访问您的文本文件,同时利用了 Cloudflare 的全球分布式网络。

#
▶️ **新人[YouTube](https://youtube.com/@AM_CLUB)** 需要您的支持，请务必帮我**点赞**、**关注**、**打开小铃铛**，***十分感谢！！！*** ✅
</br>🎁 不要只是下载或Fork。请 **follow** 我的GitHub、给我所有项目一个 **Star** 星星（拜托了）！你的支持是我不断前进的动力！ 💖
</br>✅**解锁更多技术请点击进入 YouTube频道[【@AM_CLUB】](https://youtube.com/@AM_CLUB) 、[【个人博客】](https://am.809098.xyz)** 、TG群[【AM科技 | 分享交流群】](https://t.me/AM_CLUBS) 、获取免费节点[【进群发送关键字: 订阅】](https://t.me/AM_CLUBS)

#
- 部署视频教程：[小白教程](https://www.youtube.com/watch?v=dzxezRV1v-o)
- 视频教程：[所有教程](https://www.youtube.com/playlist?list=PLGVQi7TjHKXbrY0Pk8gm3T7m8MZ-InquF)


## 一、功能特性

- **文本文件存储**: 您可以将任何文本文件存储到 Cloudflare Workers KV 键值存储中,包括纯文本、JSON、XML 等格式。
- **通过 URL 读取文件**: 只需通过构造合适的 URL,就可以读取存储在 KV 中的文本文件内容。
- **通过 URL 更新文件**: 您可以使用 URL 查询参数将新的文本内容上传到 KV,从而实现文件的更新。
- **Base64 编码支持**: 支持使用 Base64 编码的方式上传和下载文件,以应对某些特殊字符场景。
- **安全访问控制**: 通过设置 token 参数,可以限制只有拥有正确密钥的请求才能访问您的文件。
- **辅助工具脚本**: 提供了 Windows 批处理文件和 Linux Shell 脚本,用于方便地从本地上传文件到 KV。

## 二、使用说明 

1. **部署到 Cloudflare Workers**

  将项目代码部署到您的 Cloudflare Workers 服务。您需要先在 Cloudflare 上创建一个 Workers 项目,然后将 `_worker.js` 文件的内容复制粘贴到 Workers 编辑器中。

2. **创建 KV 命名空间**

  在您的 Cloudflare Workers 和 Pages 项目中的KV选项,创建一个新的 `KV` 命名空间,用于存储文本文件。记下这个 KV 命名空间的名称,因为您需要将它绑定到 Workers 上。

3. **设置 TOKEN 变量**

  - 为了增加安全性,您需要设置一个 TOKEN 变量,作为访问文件的密钥。在 Cloudflare Workers 的环境变量设置中,添加一个名为 `TOKEN` 的变量,并为其赋予一个安全的值。
  - 默认 TOKEN 为：`pwd`
  - 在变量找到 "KV 命名空间绑定"项, 点添加绑定,添加一个名为 `KV` 的变量,并选中一个KV 命名空间,这个就选择上面第2步中创建的KV 命名空间的名称

4. **访问配置页面**

例如 您的workers项目域名为：`txt.anson.workers.dev` , token值为 `pwd`；

  - 访问 `https://您的Workers域名/config?token=您的TOKEN` 或 `https://您的Workers域名/您的TOKEN`，您将看到一个配置页面，其中包含了使用说明和下载脚本的链接。

  - 你的项目配置页则为：

    ```url
    https://txt.anson.workers.dev/config?token=pwd
    或
    https://txt.anson.workers.dev/pwd
    ```

5. **使用辅助脚本上传文件**

  - Windows 用户可以下载 `update.bat` 脚本,然后执行 `update.bat 文件名` 来上传本地文件到 KV。
  - Linux 用户可以下载 `update.sh` 脚本,执行 `./update.sh 文件名` 来上传本地文件。
  - **注意：因为URL长度限制，如果保存内容过长则只能通过直接编辑`KV`对应文件内容来实现大文件的修改保存。**

6. **通过 URL 访问文件**

例如 您的workers项目域名为：`txt.anson.workers.dev` , token值为 `test` , 需要访问的文件名为 `ip.txt`；

  - 构造 URL 的格式为 `https://您的Workers域名/文件名?token=您的TOKEN`。您就可以在浏览器中查看该文件的内容了。
  - 你的访问地址则为： `https://txt.anson.workers.dev/ip.txt?token=test`。

7. **简单的更新文件内容**

  要更新某个文件的内容,可以使用 URL 查询参数 `text` 或 `b64` 来指定新的文本内容或 Base64 编码后的内容。URL 的格式为:

  ```url
https://您的Workers域名/文件名?token=您的TOKEN&text=新文本内容
或
https://您的Workers域名/文件名?token=您的TOKEN&b64=Base64编码的新文本内容
  ```


## 三、变量说明

| 变量名    | 示例                                                        | 必填 | 备注                                                         |
| --------- | ----------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| TOKEN     | uc0bZblkbO3gKxhn13t                    |❌| `GH_TOKEN`和`TOKEN`同时存在的时候会作为访问鉴权，单独赋值时的效果与`GH_TOKEN`相同 |


 # 
<center><details><summary><strong> [点击展开] 赞赏支持 ~🧧</strong></summary>
*我非常感谢您的赞赏和支持，它们将极大地激励我继续创新，持续产生有价值的工作。*
  
- **USDT-TRC20:** `TWTxUyay6QJN3K4fs4kvJTT8Zfa2mWTwDD`
  
</details></center>

#
免责声明:
- 1、该项目设计和开发仅供学习、研究和安全测试目的。使用者在下载和使用该项目时，必须遵守当地法律和规定。使用者有责任确保他们的行为符合其所在地区的法律、规章以及其他适用的规定。
- 2、作者对任何人或团体使用该项目进行的任何非法活动不承担责任。使用者使用该项目时产生的任何后果由使用者本人承担。
- 3、作者不对使用该项目可能引起的任何直接或间接损害负责。作者保留随时更新本免责声明的权利，且不另行通知。