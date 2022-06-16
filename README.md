## 注意事项
1）5月8日晚，CloudFlare Workers 的业务域名 Workers.dev 被防火长城 DNS 污染、SNI阻断。

2）CloudFlare Workers，可自定义workers域名，教程已更新至博客`ifts.ml`；经过添加自定义域名，更换Host和SNI后已可正常使用。

0.给本项目个stars

1.将本项目fork至自己仓库修改`Deploy to Heroku`按键指向地址为自己仓库地址

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/kmingfctdc34nm/xcv) 

2.点击上面紫色`Deploy to Heroku`，会跳转到heroku app创建页面，应用程序名无需填写也能创建，名字会由heroku随机生成，选择节点（美国或者欧洲），新用户只需要自定义UUID码和CADDYIndexPage（参考：[Caddy主页配置](https://github.com/DaoChen6/IF-XTW/blob/master/README.md#5caddy%E4%B8%BB%E9%A1%B5%E9%85%8D%E7%BD%AE))，其他建议保持默认，点击下面deploy，几秒后搞定！   

3.若出现`We couldn't deploy your app because the source code violates the Salesforce Acceptable Use and External-Facing Services Policy.`提示，则返回仓库，>`Setting`>`Repository name`修改仓库名。

* 从以下链接中复制喜欢的主页链接到CADDYIndexPage变量中

|#|地址|
|:-:|:-:|
| 1(默认) | [欢迎使用caddy页面](https://raw.githubusercontent.com/caddyserver/dist/master/welcome/index.html) |
| 2 | [3DCEList元素周期表](https://github.com/wulabing/3DCEList/archive/master.zip) |
| 3 | [Spotify-Landing-Page-Redesign](https://github.com/WebDevSimplified/Spotify-Landing-Page-Redesign/archive/master.zip) |
| 4 | [dev-landing-page](https://github.com/flexdinesh/dev-landing-page/archive/master.zip) |
| 5 | [free-for-dev](https://github.com/ripienaar/free-for-dev/archive/master.zip) |
| 6 | [tailwindtoolbox-Landing-Page](https://github.com/tailwindtoolbox/Landing-Page/archive/master.zip) |
| 7 | [sandhikagalih/simple-landing-page](https://github.com/sandhikagalih/simple-landing-page/archive/master.zip) |
| 8 | [StartBootstrap/startbootstrap-new-age](https://github.com/StartBootstrap/startbootstrap-new-age/archive/master.zip) |
| 9 | [mikutap 一个好玩带音乐的页面](https://github.com/AYJCSGM/mikutap/archive/master.zip)<br>[演示](https://aidn.jp/mikutap) |
| 10 | [WebGL流体模拟](https://github.com/PavelDoGreat/WebGL-Fluid-Simulation/archive/master.zip)<br>[演示](https://paveldogreat.github.io/WebGL-Fluid-Simulation/) |
| 11 | [loruki-website](https://github.com/bradtraversy/loruki-website/archive/master.zip) |
| 12 | [bongo.cat一只音乐的猫](https://github.com/Externalizable/bongo.cat/archive/master.zip)<br>[演示](https://bongo.cat/) |

### CloudFlare Workers反代代码（支持VLESS\VMESS\Trojan-Go的WS模式，可分别用两个账号的应用程序名（UUID与path保持一致），单双号天分别执行，那一个月就有550+550小时）

1.适用单一应用的反代代码

```
addEventListener(
  "fetch", event => {
    let url = new URL(event.request.url);
    url.host = "appname.herokuapp.com";
    let request = new Request(url, event.request);
    event.respondWith(
      fetch(request)
    )
  }
)
```

2.适用单双日循环执行的反代代码

```
const SingleDay = '应用程序名1.herokuapp.com'
const DoubleDay = '应用程序名2.herokuapp.com'
addEventListener(
    "fetch",event => {
    
        let nd = new Date();
        if (nd.getDate()%2) {
            host = SingleDay
        } else {
            host = DoubleDay
        }
        
        let url=new URL(event.request.url);
        url.hostname=host;
        let request=new Request(url,event.request);
        event. respondWith(
            fetch(request)
        )
    }
)
```

3.适用多实例循环执行的反代代码

```
const Day0 = 'app0.herokuapp.com'
const Day1 = 'app1.herokuapp.com'
const Day2 = 'app2.herokuapp.com'
const Day3 = 'app3.herokuapp.com'
const Day4 = 'app4.herokuapp.com'
addEventListener(
    "fetch",event => {
    
        let nd = new Date();
        let day = nd.getDate() % 5;
        if (day === 0) {
            host = Day0
        } else if (day === 1) {
            host = Day1
        } else if (day === 2) {
            host = Day2
        } else if (day === 3){
            host = Day3
        } else if (day === 4){
            host = Day4
        } else {
            host = Day1
        }
        
        let url=new URL(event.request.url);
        url.hostname=host;
        let request=new Request(url,event.request);
        event. respondWith(
            fetch(request)
        )
    }
)
```

### 原作者项目地址：https://github.com/mixool/xrayku

# 鸣谢

- [Xrayku](https://github.com/mixool/xrayku)
- [Project V](https://github.com/v2fly/v2ray-core.git)
- [Project X](https://github.com/XTLS/Xray-core.git)
- [HeroKu](https://heroku.com)
- [heroku-vless](https://github.com/DanyTPG/heroku-vless.git)
- [Better Cloudflare IP](https://github.com/badafans/better-cloudflare-ip.git)
- [CloudflareSpeedTest](https://github.com/XIU2/CloudflareSpeedTest.git)
- [CloudflarespeedTest-Rust](https://github.com/lixiang810/CloudflareSpeedTest-Rust.git)
