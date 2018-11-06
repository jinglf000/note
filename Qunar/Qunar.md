## Qunar

#### 1、导航地址

金融BU导航：http://md.corp.qunar.com/appdownload?framework=qrn&edition=2018-08

新人入职：http://wiki.corp.qunar.com/confluence/pages/viewpage.action?pageId=204603108

gitlab地址：http://gitlab.corp.qunar.com/s/scar.jing

Qunar社区：http://qunar.it/

负责项目地址：

Node项目：    git@gitlab.corp.qunar.com:financefe/finance_primary_rn.git      |[金融主页](http://dev.qunar.com:7001/m/finweb/ssr/financeCenter?clientSource=QUNAR&from=financeCenter
)

RN项目：  git@gitlab.corp.qunar.com:financefe/finance_primary_rn.git  需要XCode

笔记：[杨崇多](http://wiki.corp.qunar.com/confluence/spaces/viewspace.action?key=~chongduo.yang)

调试包地址：http://md.corp.qunar.com/appdownload?framework=qrn&edition=2018-09

模拟器包安装步骤：http://wiki.corp.qunar.com/confluence/pages/viewpage.action?pageId=114448236

技术使用：node、react、redux、flux、reselector



####2 、Xcode模拟器使用：

首先：安装xcode

```shell
xcrun instruments -s // 列出所有可用设备
xcrun instruments -w "iPhone X (12.0)"// 开启制定模拟器
xcrun simctl install booted <app路径> // 安装指定app，这时会在模拟器里发现这款app
xcrun simctl launch booted <app identifier> // 从模拟器里运行应用
xcrun simctl uninstall booted <app identifier> // 从模拟器里删除应用	
```

####3、vim 使用
https://coolshell.cn/articles/5426.html

```shell
i // 切换vim编辑器模式为insert模式
esc // 退出insert模式，改为normal模式
:wq //  保存并退出
```

####4、charles 使用，抓取http，https包

* 1、安装charles，使用激活地址，激活
* 2、安装 证书 `help ssl Proxying`  安装 证书、ios Simulator 证书
* 3、退出本地代理 `shadowSocks` 注意是退出
* 4、`charles-proxy-proxy setting` port `8888` ,socks proxy 开启
* 5、`charles-proxy-ssl proxy settings` enabled and 添加一个地址 `* 443`
* 6、`shift + command + p` 两次切换代理

#### 5、使用 React Native Debugger 调试RN项目，关闭既有的调试方式 浏览器

JS Bundle 加载方式 ---> 

服务地址：localhost:8081 同时使用switchHost 设置host 为本地

开启 JS Debug Mode 和 Debug inChrome 其他关闭





在RN app项目中设置 服务器地址，配置了RN项目异步请求的服务地址。

jr.qunar.com/app 为真实服务地址

jrbetam.qunar.com/app betam 的后台服务地址

jrbetay.qunar.com/app 