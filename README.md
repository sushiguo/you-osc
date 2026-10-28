# 优优电视 制品仓库

这里只放三样东西：最新的 APK、应用内更新用的 `update.json`、以及可以直接订阅的 JSON / M3U / TXT 配置。源码不在这里。

## 应用更新

| 用途 | 地址 |
| --- | --- |
| 更新清单（已写进 APK 默认值，无需手填） | https://raw.githubusercontent.com/sushiguo/youyou/main/update.json |
| 最新 APK | https://github.com/sushiguo/youyou/releases/latest/download/youyou-tv.apk |
| 指定版本 APK | https://github.com/sushiguo/youyou/releases/download/v610282115/youyou-tv.apk |

`update.json` 描述的是平板版包名 `com.youyou.tvbox.osc`；版本号是 9 位 `6MMDDHHMM`。清单里的 `sha256`、`size` 与签名证书任一对不上，应用都不会安装，并会把具体原因显示出来。
应用内查看或改地址：我的 → 模块管理 → 应用更新地址；留空即回到上面这个默认值。

## 订阅配置

应用内「我的 → 添加订阅」粘贴下面的地址即可。文件按内容重新起了 ASCII 名字（原来多用中文名，粘到地址栏要先转义），内容除下面两处外与本机版本逐字节相同。

| 配置 | 内容 | 地址 |
| --- | --- | --- |
| ziyong-yuan.json | 自用源（点播 + 直播 + 搜索，本机原文件名「自用源」） | https://raw.githubusercontent.com/sushiguo/youyou/main/tvbox/own/ziyong-yuan.json |
| ziyong-dancang.json | 自用单仓 | https://raw.githubusercontent.com/sushiguo/youyou/main/tvbox/own/ziyong-dancang.json |
| ziyong-dancang2.json | 自用单仓 2 | https://raw.githubusercontent.com/sushiguo/youyou/main/tvbox/own/ziyong-dancang2.json |
| ziyong-duocang.json | 自用多仓 | https://raw.githubusercontent.com/sushiguo/youyou/main/tvbox/own/ziyong-duocang.json |
| zyplayer.json | ZyPlayer 格式配置 | https://raw.githubusercontent.com/sushiguo/youyou/main/tvbox/own/zyplayer.json |
| qixing-baohe.txt | 七星宝盒仓库 | https://raw.githubusercontent.com/sushiguo/youyou/main/tvbox/qixing-baohe.txt |
| shiguang-duocang.txt | 拾光多仓 | https://raw.githubusercontent.com/sushiguo/youyou/main/tvbox/shiguang-duocang.txt |
| ziyong-live.m3u | 自用直播（M3U） | https://raw.githubusercontent.com/sushiguo/youyou/main/tvbox/own/ziyong-live.m3u |
| ziyong-live-cang.json | 自用直播仓库（21 组聚合） | https://raw.githubusercontent.com/sushiguo/youyou/main/tvbox/own/ziyong-live-cang.json |
| ziyong-live-qingtian.txt | 自用直播·晴天源 | https://raw.githubusercontent.com/sushiguo/youyou/main/tvbox/own/ziyong-live-qingtian.txt |
| ziyong-live-youguan.txt | 自用直播·油管源 | https://raw.githubusercontent.com/sushiguo/youyou/main/tvbox/own/ziyong-live-youguan.txt |
| tvbox/own/live.txt | 自用直播列表（TXT，326 行） | https://raw.githubusercontent.com/sushiguo/youyou/main/tvbox/own/live.txt |
| live.txt | 直播列表（含 YouTube 频道，368 行） | https://raw.githubusercontent.com/sushiguo/youyou/main/subscriptions/live/live.txt |
| child-animation.txt | 动画剧集（1460 行） | https://raw.githubusercontent.com/sushiguo/youyou/main/subscriptions/live/child-animation.txt |

两处改动：`ziyong-live-cang` 原文件 21 行里用的是全角逗号，机器读会当格式错误，这里换成半角并改成 `.json`；其余文件未动。

配置里引用的 `jar` / `js` / `token.txt` 仍指向它们原本的站点或本机路径（`127.0.0.1:9978` 是应用自己的本地代理，`token.txt` 只存在于平板本地），本仓库不代存第三方脚本与二进制；成人向的仓库文件已全部剔除。

## 发版

APK、清单与配置由工程里的 `scripts/publish_artifacts.py` 一次性写好：它先用 aapt / apksigner 核对包名、版本号、debuggable 与签名证书（与 `app/build.gradle` 不一致就直接拒绝发布），再把 APK 作为 Release 资产上传（72MB 走不了 Contents API），最后写 `update.json` 并回读 raw 地址与下载直链逐字节核对。
APK 资产固定叫 `youyou-tv.apk`：下载地址里带中文要先转义，白白多一处会坏的地方，版本信息由 tag 承担。
