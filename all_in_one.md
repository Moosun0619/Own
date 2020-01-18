# 多合一签到脚本（自用Surge配置）--未修改完成勿用

##包含哔哩哔哩直播！！签到, 京东签到, 网易云签到, 百度贴吧签到, 人人视频签到, 喜马拉雅签到
（没有微博签到，微博签到需自行添加自己的超话id，所以请自己搞定，谢谢！）

> 此脚本仅支持Surge
>
>此根据 [@sazs34](https://github.com/sazs34)大佬的改编，如需qx的, 可去大佬的网址查看
>

**支持列表**

|    名称    | Cookie |                             签到                             |                       感谢                        |     说明     |
| :--------: | :----: | :----------------------------------------------------------: | :-----------------------------------------------: | :----------: |
|  哔哩哔哩 |   ✅    |                              ✅                               |   [@chavyleung](https://github.com/chavyleung)    |   cookie同原版    |
|    京东    |   ✅    | [获取](https://github.com/NobyDa/Script/blob/master/JD-DailyBonus/JD_DailyBonus.js) |       [@NobyDa](https://github.com/NobyDa)        | cookie同原版 |
| 网易云音乐 |   ✅    |                              ✅                               |   [@chavyleung](https://github.com/chavyleung)    |     cookie同原版    |
| 百度贴吧 |   ✅    |                              ✅                               |     [@chavyleung](https://github.com/chavyleung)  |    cookie同原版   |
|  人人视频 |   ✅    |                              ✅                                            |    [@chavyleung](https://github.com/chavyleung)     | cookie同原版 |
| 喜马拉雅  |   ✅    |                              ✅                               |     [@chavyleung](https://github.com/chavyleung)       | cookie同原版 |

脚本地址:

** https://raw.githubusercontent.com/XYXShawn/JS/master/all_in_one.js
 **

## 脚本配置说明

打开js文件,最开头的地方就能看到如下一段代码

```javascript
//因为有的人只有其中一个或两个需要进行签到,所以进行了配置化,可以指定签到
const global = {
    log: 1, //日志模式:0不显示 1全部显示 2精简显示,推荐值:1
    sign: { //用于设置哪些需要进行签到,哪些不处理
        baidu_tieba: true,
        netease_music: true
    },
    data: {
  
}
```

| 节点 |      作用      |                 说明                 |
| :--: | :------------: | :----------------------------------: |
| log  | 在qx中显示日志 | 0不显示 1全部显示 2精简显示,推荐值:1 |
| sign |  控制是否签到  |     true为进行签到,false为不签到     |
| data |    额外参数    |        用于签到脚本中数据配置        |

## Surge配置说明

### 添加MITM

```
[mitm]
hostname = *.bilibili.com, api.m.jd.com，tieba.baidu.com, music.163.com, *.rr.tv,mobwsa.ximalaya.com
```

### 获取cookie的脚本（脚本1）

以下cookie获取之后需注释掉

```
# 此处用于哔哩哔哩cookie获取，打开浏览器访问: https://www.bilibili.com 或 https://live.bilibili.com （需先登陆再获取cookie），待弹出获取成功后，即可注释掉
http-request ^https:\/\/(www|live)\.bilibili\.com\/?.? script-path= https://raw.githubusercontent.com/XYXShawn/JS/master/all_in_one.js

# 此处用于京东cookie获取，需要手动登录京东网页版https://bean.m.jd.com/ 签到获取Cookie, 待弹出获取成功后，即可注释掉
http-request https:\/\/api\.m\.jd\.com\/client\.action.*functionId=signBean(Index|GroupStageIndex) max-size=0,script-path= https://raw.githubusercontent.com/XYXShawn/JS/master/all_in_one.js

# 此处用于百度贴吧cookie获取，当失效时需手动登录https://tieba.baidu.com/index.html贴吧获取cookie，待弹出获取成功即可
^https?:\/\/tieba.baidu\.com url script-request-header all_in_one.js

# 此处用于网易云音乐cookie获取，当失效时需浏览器访问并登录:https://music.163.com/m/login 获取cookie，待弹出获取成功即可
^https?:\/\/music\.163\.com url script-request-header all_in_one.js

# 此处用于人人视频cookie获取，加mitm后打开APP，点击“我的”，待弹出获取成功即可
https:\/\/passport\.iqiyi\.com\/apis\/user\/info\.action.*authcookie url script-request-header all_in_one.js

# 此处用于喜马拉雅cookie获取,浏览器访问https://www.52pojie.cn/home.php?mod=space 即可
https:\/\/www\.52pojie\.cn\/home\.php\?mod=space url script-request-header all_in_one.js
```

### 签到脚本（脚本2)
```
（例：8点签到）
cron "0 0 8 * * *" script-path= https://raw.githubusercontent.com/XYXShawn/JS/master/all_in_one.js
```

## 触发Cookie方式详细说明

|                             名称                             |  方式  |                            说明                            |
| :----------------------------------------------------------: | :----: | :--------------------------------------------------------: |
|                         哔哩哔哩直播                           | 浏览器 |                先浏览器登陆：https://www.bilibili.com 或 https://live.bilibili.com ，再添加配置，再次打开浏览器获取cookie |
|                           百度贴吧                           | 浏览器 |             先浏览器登陆：https://tieba.baidu.com 或者 https://tieba.baidu.com/index/ ，再添加配置，再次打开浏览器获取cookie |
|                            网易云                            | 浏览器 |               https://music.163.com/m/login                |
|                         人人视频                           |  APP   |                   进入APP,访问一下个人中心                   |
|                         喜马拉雅                          |APP |        打开 APP, 访问下右下角账号          |
