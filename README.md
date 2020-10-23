# electron+vue+sqlite3跨平台桌面应用开发
  electron+vue+sqlite3 三者结合让您轻松快速开发PC端桌面应用，electron可以让您想开发网站一样轻松开发桌面应用，electron为您提供丰富的API省去很多代码，您只需花时间在业务代码上，并且可以多段打包。vue是当前最火的前端框架之一，加入vue可让你开发跟简单，并且更省时间，为您减少更多开发成本。sqlite是一款轻型的关系数据库，无需安装、无服务器、零配置的、支持事务。它是在世界上最广泛部署的 SQL 数据库引擎，链式操作非常好用，推荐使用，只是在electron应用内安装SQLite，比较特殊，不在这里已经为您解决了，使用过程有问题可以提问。
  
----
### 关于electron
使用 JavaScript，HTML 和 CSS 构建跨平台的桌面应用程序。如果你可以建一个网站，你就可以建一个桌面应用程序。 Electron 是一个使用 JavaScript, HTML 和 CSS 等 Web 技术创建原生程序的框架，它负责比较难搞的部分，你只需把精力放在你的应用的核心上即可。

### electron优势
----
1. Web 技术
> Electron 基于 Chromium 和 Node.js, 让你可以使用 HTML, CSS 和 JavaScript 构建应用。
2. 开源
> Electron 是一个由 GitHub 及众多贡献者组成的活跃社区共同维护的开源项目
3. 跨平台
> Electron 兼容 Mac、Windows 和 Linux，可以构建出三个平台的应用程序。

## 使用说明
```javascript
	#下载项目包

	npm install https://github.com/huanglishi/electron-vue-sqlite.git

	#进入项目目录并安装依赖包

	cd you-project

	yarn # 或者 npm install

	#运行项目

	yarn run dev # 或者 npm run dev

```
## 特别说明
#### 1.打包配置
```javascript
 "build": {
    "productName": "Elerp",//项目名 这也是生成的exe文件的前缀名
    "appId": "com.example.erp",
    "copyright":"@经和科技",
    "compression": "store",
    "directories": {
      "output": "build"// 输出文件夹
    },
    "files": [
      "dist/electron/**/*"
    ],
    "asar": false,// asar打包
    "nsis": {
      "oneClick": false,  
      "allowToChangeInstallationDirectory": true, 
      "perMachine": true
    },
    "mac": {
      "icon": "build/icons/icon.icns"
    },
    "extraResources":  { // 拷贝db\dll等静态文件到指定位置;他在安装文件resources下；
      "from": "./extraresources/",
      "to": "extraresources"
    },
    "win": {
      "icon": "build/icons/icon.ico",
      "extraResources":  { 
        "from": "./extraresources/",
        "to": "extraresources"
      },
      "target": [
        {
          "target": "nsis",  
          "arch": [ 
            "x64"
          ]
        }
      ],
      "publish": [ 
        {
          "provider": "generic", 
          "url": "http://127.0.0.1:8080/updata/" 
        }
      ]
    },
    "linux": {
      "icon": "build/icons"
    }
  },
  
  注：使用sqlite3数据数据库必须加extraResources配置，否则数据打包文件
  使用remote.app.getPath('userData')方式手动添加到用应文件目录。
```
#### 2.数据库文件db放在安装目录
 项目根目录建extraresources文件夹，本项目local.db文件放在里面
#### 3.重新编译
```javascript
#sqlite3是新增模块,使用前请先重新编译原生模块

yarn  rebuild # 或者 npm rebuild

```
### 在您方便时候也可以在右上角给我 `⭐ Star` ~哦
###  开发过程又是什么问题可加 QQ:[504500934](https://ynjiyuan.com "504500934") 进行交流
## 如果可以帮助您，您也可以赞助一下喝杯茶



![Pandao editor.md](https://honey.ynjiyuan.com/wxpayqrcode.png "Pandao editor.md")


