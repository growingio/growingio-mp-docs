# iOS 证书设置指南

### 创建应用程序 ID <a id="id"></a>

* 登陆 [苹果开发者网站](https://developer.apple.com/) 进入开发者账户。
* 从开发者账户页面左侧入口进入 “Certificates, IDs & Profiles” 页面。
* 创建 App ID，填写 App ID 的 NAME 和 Bundle ID（如果 ID 已经存在可以直接跳过此步骤）。
* 为 App 开启 Push Notification 功能。如果是已经创建的 App ID 也可以通过设置开启 Push Notification 功能。
* 填写好以上属性后，点击 “Continue”，确认 AppId 属性的正确性，点击 “Register”，注册 AppId 成功。

#### 1、项目配置

* 在项目工程中打开后台推送权限设置，如下图所示

![](https://uploader.shimo.im/f/SWzAMh9iaCQusbiR.png!thumbnail)

* 打开推送开关，如下图所示

![](https://uploader.shimo.im/f/5QUzv4EWkIcEQAzs.png!thumbnail)

#### 2、创建AppID

如果之前已经创建了AppID可跳过这一步。登录苹果开发者账号，点击如下图红色箭头区域，进入证书配置页面

![](https://uploader.shimo.im/f/Udvx0myyCssMkX2m.png!thumbnail)

选中“Identifiers”，并且对应的是“App IDs”

![](https://uploader.shimo.im/f/GyeCaFwZBtsiHtEu.jpeg!thumbnail)

选中对应的平台（Platform），输入对应的描述（Description）、Bundle ID

![](https://uploader.shimo.im/f/yBdh9fFtXpsbwo9r.jpg!thumbnail)

打开推送功能，选中如下图所示，点击右上角“continue”按钮，执行下一步

![](https://uploader.shimo.im/f/xTEHRmWlZdkF9Nol.png!thumbnail)

确定信息无误后，点击右上角“Register”进行注册

![](https://uploader.shimo.im/f/miSnMCNRxQMtTnPW.jpg!thumbnail)

#### 3、创建本地CRS证书

打开MAC电脑上的钥匙串访问，点击窗口左上角的“钥匙串访问”中的“证书助理”，选择“从证书颁发机构请求证书…”

![](https://uploader.shimo.im/f/VPTe3r4uHV0UUSQi.png!thumbnail)

将证书选择为“存储到磁盘”，输入任意合法的邮箱地址后即可将证书保存到本地目录路径下

![](https://uploader.shimo.im/f/qzmEZDhyrRwkWmvH.png!thumbnail)

#### 4、创建推送证书

登录苹果开发者账号，点击下图红色箭头指示区域

![](https://uploader.shimo.im/f/5FhUwTYKtRMOpLwX.png!thumbnail)

点击加号“+”，创建证书

![](https://uploader.shimo.im/f/4o2cXVres6QBXLOg.png!thumbnail)

选择“Services”下创建推送证书，其中红色箭头指示的为创建开发调试环境下的推送证书，蓝色箭头指示的为创建生产环境以及开发调试下的推送证书，

![](../../../.gitbook/assets/image%20%28128%29.png)

这里假如创建的是开发环境的推送证书，选中红色箭头对应的圆圈，点击右上角的“continue”按钮，进入下一步，选择项目对应的“App ID”，点击右上角的“continue”按钮，进入下一步

![](https://uploader.shimo.im/f/Dbs9y2fY1JQDOQzw.jpg!thumbnail)

选择本地的“CRS”文件，点击右上角的“continue”按钮，进入下一步，即可生成对应项目开发环境下的推送证书，点击右上角的“Download”按钮，将证书下载到本地，选中刚才下载的证书，双击安装。

#### 5、导出推送证书p12

打开MAC电脑上的钥匙串访问，找到刚才安装的推送证书，选中右击导出该证书

![](https://uploader.shimo.im/f/FVQZAYHFTrwqn6hg.jpg!thumbnail)

设置证书的本地存储路径，选择导出证书的格式为个人信息交换\( .p12 \)，设置证书密码

![](https://uploader.shimo.im/f/p1pgLxFaPI0yIlL9.jpeg!thumbnail)

#### 6、上传证书

登录“GrowingIO” 用户运营页面，找到对应配置的项目，确保之前已经成功集成了触达SDK，在应用管理中的“**应用配置**”中选择需要配置的推送证书的环境，输入对应的“BundleID”，选中本地导出的p12的推送证书，输入密码并保存。

