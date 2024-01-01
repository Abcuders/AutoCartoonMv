# | AutoAnimeMV:超轻量化快速部署看番遥遥领先！
<div align="center">
  <a href="https://github.com/Abcuders/AutoAnimeMV">
    <img src="./Image/logo.png">
  </a>

**全自动追番新时代！不动手才是硬道理！**


**简体中文 | [English](./README_en.md)**

*! En-README.md 由于我精力不够所以有太多落后未更新的地方,如果您感兴趣并且有时间的希望您能帮助一下我✊*

[![ GitHub 许可证](https://img.shields.io/github/license/Abcuders/AutoAnimeMv)](https://github.com/Abcuders/AutoCartoonMv/LICENSE) [![GitHub release](https://img.shields.io/github/v/release/Abcuders/AutoAnimeMv)](https://github.com/Abcuders/AutoAnimeMv/releases/) [![telegram](https://img.shields.io/badge/telegram-AutoAnimeMv-blue?style=flat&logo=telegram)](https://t.me/AutoAnimeMv)

***
> 😊这是一个**番剧自动识别**`剧名剧集+自动重命名+自动整理的工具,还可以帮你把ASS/SRT外挂字幕也一起整理了哟`,**具有部署方便,开箱即用的特点**,用来配合QBittorrent实现Rss订阅下载Emby全自动刮削一条龙到家式爽歪歪服务!
 
</div>

 **本工具现在支持Linux🐧和Windowsℹ️了并且有了自己的项目群耶（点击上面tg小蓝标直通车）👏👏👏**
 > `工具更新较快,用法和功能都会更新,建议多来看看`

> **🚀点击左上角打开目录，选择您要阅读的部分**
<div align="center">
 
 ## **🛎️🛎️New功能！🛎️🛎️**
 </div>
 
 > * 可以**批处理刮削已下载番剧**啦！(包括字幕文件) [如何使用?](#使用场景2-批处理本地已下载番剧) 
 > * 整理番剧可以使用硬链接了,**保种用户的福音** [如何使用?](#使用硬链接整理番剧)
 > * 加入了**Bgm API支持**！[看看](#bgm-api)
 > * **番剧特别篇**也可以识别整理了,并且可以按TMDB支持的方式刮削 [康康](#❓-什么样的番剧能够被识别)
 > * 新增AnimeList查询,针对Bgm和TMDB无法识别的特殊番剧别名提出的解决办法 [看一下?](#Animelist查询文件)
 > * 自动更新上线啦！[如何使用?](#启用自动更新可选)
 > * 番剧文件分类回归啦！[如何使用?](#📝-使用方法)
> * 支持外置配置了 [如何使用?](#配置)

# 🏕️ 环境支持

要使用本工具您必须需要`🐍Python3环境`支持，我们建议您搭配`🔵Qbittorrent`下载工具 `🟩Emby`/`🎶Jellyfin`等媒体库使用

# 💡 帮助&提醒

 * **`🐍Python3环境`**:您可以在[🐍Python官网](https://www.python.org/downloads/windows/)下载合适的版本进行安装,我们建议安装3.9及以上的版本,最低的版本要求是3.6版本
   >  🐍Python使用的依赖库:`sys` `os` `time` `re` `ast` `shutil` `win10toast` `requests` `zhconv`
   
   >以上依赖应该只有`win10toast`(Win通知-可选) `requests`(网络访问-可选),`zhconv`(简繁互化-必须)需要您进行安装,Linux(NAS)用户不需要安装`win10toast`(Win通知-可选)
 * 如果您直接使用pip进行install遇到 `❗Fatal error in launcher: Unable to create process using pip问题` ,请使用`python3 -m pip install`
 * **`🔵Qbittorrent`**:我们推荐您使用Docker进行安装使用,Win用户可以访问[Qbittorrent官网](https://www.qbittorrent.org/)进行安装
 * **`🟩Emby/🎶Jellyfin`**:[🟩Emby官网](https://emby.media/) [🎶Jellyfin官网](https://jellyfin.org/) [🎶Jellyfin-GitHub](https://github.com/jellyfin/jellyfin-media-player)


 * <img style="vertical-align:sub;" src="./Image/rss.png" height="15" width="35" > **`番剧网站`**:如果您需要RSS或BT或番剧支持，您可以来我们的Tg群寻找帮助
   
## 🕹️ 工具的处理逻辑

  * 开始Run之后会进行自动识别视频文件格式、番剧剧集、截断文件名、去除无效文字、剔除字幕组、保留剧名剧季，并将视频文件重命名为`S剧季E剧集.文件格式`再移至`下载路径` 下的`剧名\Season_剧季`文件夹(如果没有则会自动创建)就像下面一样,特殊剧集如7.5和00,则会被认为是`SP剧集`:
    ```
    [ANi] 无神世界的神明活动（仅限港澳台地区） - 01 [1080P][Bilibili][WEB-DL]  [AAC AVC][CHT CHS][MP4].MP4
    >>无神世界的神明活动/Season_01/S01E01.mp4
    ```
    > *我们将 判断是否属于`动漫`分类功能注释了，现在它是一个可选功能，您可以根据不同的类型设置不同的Video保存路径*
  * 如果下载的torrent中存在一个或多个ASS/SRT外挂字幕时,工具会将当集字幕重命名为`S剧季E剧集.字幕格式`并移至番剧旁,以便`🟩emby` `🎶Jellyfin`等媒体库软件识别

     🍟同时，在`下载路径`目录会生成以时间命名的Log文件,其内容为
     
     > 2023-06-03.log

     ```
    [2023-06-03 04:40:21] INFO: Running....
    [2023-06-03 04:40:21] INFO: 当前操作系统识别码为posix,posix/nt/java对应linux/windows/java虚拟机
    [2023-06-03 04:40:21] INFO: 接受到参数 ==> ['/downloads/AutoRmPY/AutoAnimeMv.py', '/downloads/动漫', '[ANi] 勇者死了！ - 01 [1080P][Baha][WEB-DL][AAC AVC][CHT].mp4']
    [2023-06-03 04:40:21] INFO: 匹配剧集 ==> 01
    [2023-06-03 04:40:21] INFO: 通过剧集截断文件名 ==> -勇者死了=---
    [2023-06-03 04:40:21] INFO: 番剧Name ==> 勇者死了
    [2023-06-03 04:40:21] INFO: id 4 TrueVideoName ==> 勇者死了,Season ==> 01
    [2023-06-03 04:40:21] INFO: 勇者死了 01 01 .mp4 << [ANi] 勇者死了！ - 01 [1080P][Baha][WEB-DL][AAC AVC][CHT].mp4
    [2023-06-03 04:40:21] INFO: 创建 勇者死了/Season_01 完成
    [2023-06-03 04:40:23] INFO: 创建 /downloads/动漫/勇者死了/Season_01/S01E01.mp4 完成...一切已经准备就绪
    ```
    > 这个是处理带有外挂字幕的番剧识别Log
    
    ```
    [2023-06-04 17:15:06] INFO: Running....
    [2023-06-04 17:15:07] INFO: 当前操作系统识别码为nt,posix/nt/java对应linux/windows/java虚拟机
    [2023-06-04 17:15:07] INFO: 接受到参数 ==> ['.\\AutoAnimeMv.py', 'E:\\\\D\\\\Test', '[BeanSub&FZSD&LoliHouse] Jigokuraku - 09', '2']参数
    [2023-06-04 17:15:07] INFO: 发现1个字幕文件 ==> ['BeanSub&FZSD&LoliHouse] Jigokuraku - 09 [WebRip 1080p HEVC-10bit AAC ASSx2].简体中文.ass']
    [2023-06-04 17:15:07] INFO: 匹配剧集 ==> 09
    [2023-06-04 17:15:07] INFO: 通过剧集截断文件名 ==> -Jigokuraku---
    [2023-06-04 17:15:07] INFO: 番剧Name ==> Jigokuraku
    [2023-06-04 17:15:07] INFO: id 4 TrueVideoName ==> Jigokuraku,Season ==> 01
    [2023-06-04 17:15:07] INFO: Jigokuraku 01 09 .mkv <<  [BeanSub&FZSD&LoliHouse] Jigokuraku - 09 [WebRip 1080p HEVC-10bit AAC ASSx2].mkv
    [2023-06-04 17:15:07] INFO: 创建 Jigokuraku\Season_01 完成
    [2023-06-04 17:15:07] INFO: 字幕文件[BeanSub&FZSD&LoliHouse] Jigokuraku - 09 [WebRip 1080p HEVC-10bit AAC ASSx2].简体中文.ass已导入
    [2023-06-04 17:15:09] INFO: 创建 E:\\D\\Test\Jigokuraku\Season_01\S01E09.mkv 完成...一切已经准备就绪
    ```

### ❓ 什么样的番剧能够被识别?
* 工具目前能够识别的类型要求为:
> 存在番剧剧集,且剧集处于剧名后(支持的剧集格式为`1-4位纯数字/XXXX集/第XXXX集/00/XX.XX(这些SP也可以识别)`),若存在`字幕组信息`,`字幕组信息`应在第一个位置,如果不在,则第一个位置应存在`《》`或者是其他情况(后文)
```
[DMG&LoliHouse] Kono Subarashil Sekai ni Bakuen wo! - 01 [WebRip 1080p HEVC-10bit AAC ASSx2].mkv
```

```
[漫游字幕组]散华礼弥/僵尸哪有那么萌 第1集 720P MKV（外挂字幕） [274.7MB].mkv
```

```
[织梦字幕组][间谍教室 スパイ教室][11集][1080P][AVC][简日双语] [337.62 MB].mp4
```

```
《江戶前精靈》#9 (日語原聲)【Ani-One Asia】.mp4
```

> torrent中包含`[]` `【】`也可以识别,包含`04月新番` `（僅限港澳台地區）` `2023.04.02`之类的信息也可以剔除干净
```
[Comicat][Jigokuraku][01][1080P][GB&JP][MP4].mp4
```

```
[ANi] 無神世界的神明活動（僅限港澳台地區） - 08 [1080P][Bilibili][WEB-DL][AAC AVC][CHT CHS].mp4
```

```
[c.c動漫][4月新番][無神世界的神明活動][07][BIG5][1080P][MP4][網盤下載]296.9MB.mkv
```

```
[Marukazoku][Sazae-san][2694][2023.04.02][BIG5][1080P][MP4].mp4
```

> torrent中包含`/`的将被工具认为是多语种译名番剧,若存在全英文译名将优先采用,不管哪个译名中存在`S2` `第二季` `Season2` `Season 2` `Season-2` `2nd-Season` 之类的剧季信息也可以识别(如果有需要,后面会开发`シーズン2`之类的剧季识别)
```
【喵萌奶茶屋】★01月新番★[英雄王，为了穷尽武道而转生～然后，成为世界最强的见习骑士♀～ / Eiyuuou, Bu wo Kiwameru Tame Tenseisu][10][720p][简体][招募翻译].mp4
```

```
[桜都字幕组] 因为太怕痛就全点防御力了。第2季/ Itai No Wa Iya Nano De Bougyoryoku Ni Kyokufuri Shitai To Omoimasu. S2 [10][ 1080P@60FPS ][简繁内封].mp4
```
> torrent中包含`v2`之类信息的重修版也是可以识别的(在开头的`v2`信息则会被剔除,字幕组信息还是在第一位)
```
[喵萌Production&LoliHouse] 偶像大师 灰姑娘女孩 U149 / THE IDOLM@STER CINDERELLA GIRLS U149 - 07v2 [WebRip 1080p HEVC-10bit AAC][简繁日内封字幕]675.6MB.mkv
```

```
[V2][织梦字幕组][鬼灭之刃 锻刀村篇 鬼灭の刃 刀锻冶の里编][01集][720P][AVC][繁日双语] [614.11 MB].mp4
```
> 番剧特别篇,会按TMDB支持的方式进行整理,即特别篇剧季会认定为`Season 00`,剧集则会按TMDB上的来,比如`我推的孩子`的`7.5`集,在TMDB上则是`第1集`
* 以上规则应该涵盖了绝大多番剧torrent
## 使番剧识别更精准的方法
### Bgm Api 
* 我们使用了BgmApi来进行更精准的剧名识别,您可以自由选择是否使用它
```ini
USEBGMAPIFLAGS = True #使用BgmApi进行更准确的识别
```
### AnimeList查询文件
* 这是一个针对Bgm和TMDB都无法识别的特殊番剧别名,进行查询的文件,其内容为
```json
{"AnimeList":['86-Eiti-Shikkusu','放學後失眠的你'],"AnimeAlias":{'86-Eiti-Shikkusu':'86-不存在的战区','放學後失眠的你':'放学后失眠的你'}}
```
* 您可以选择是否启用此功能和使用Github或本地的AnimeList(本地位置和`AutoAnimeMV.py`同路径) [配置?](#配置)
> 如果同时打开使用Github上的文件和使用本地的文件，则工具只会使用Github上的AnimeList文件
```ini
USEGITHUBANIMELISTFLAG = True #使用Github上的AnimeList文件
USELOCALANIMELISTFLAG = False #使用本地的AnimeList文件
FORCEDUSEBGMAPI = False #强制使用BgmApi进行识别,不查询AimeList文件
```
* *Bgm Api和AnimeList均有缓存设计,以加快运行速度*
## 🧰 测试工具 
* 自🍞`v1.5.0`以后，您可以使用`Test.py`对`AutoAnimeMv.py`进行Bt识别测试，以下是`Test.py`的使用方法
  > `Test.py` 不需要任何参数，但是需要`tese`文件，其内容为
    ```json
   {"Bt":"","Name":"","Season":"","Episodes":"","FileType":""}
    ```
  > `Bt`参数为种子名称 `Name`参数为番剧名称(可选) `Season`为剧季数(可选) `Episodes`为剧集数(可选) `FileType`为视频文件格式(可选)

 
* 🍚举例,以下是规范的Test格式,您也可以写入多行Tests数据
  ```json
   {"Bt":"[DMG&LoliHouse] Kono Subarashil Sekai ni Bakuen wo! - 01 [WebRip 1080p HEVC-10bit AAC ASSx2].mkv","Name":"Kono Subarashil Sekai ni Bakuen wo","Season":"01","Episodes":"01","FileType":".mkv"}
  ```
  > 这些test测试数据可以用来在未来更新了匹配机制的情况下快速测试这个算法
* 执行以下代码即可进行测试
  ```
  python3 Test.py 
  ```
* 输出内容(debug用):
  ```log
  [2023-06-03 12:49:12] INFO: 匹配剧集为01
  [2023-06-03 12:49:12] INFO: 通过剧集截断文件名 ==> -Kono-Subarashil-Sekai-ni-Bakuen-wo=---
  [2023-06-03 12:49:12] INFO: 番剧Name ==> Kono-Subarashil-Sekai-ni-Bakuen-wo
  [2023-06-03 12:49:12] INFO: id 4 TrueVideoName ==> Kono-Subarashil-Sekai-ni-Bakuen-wo,Season ==> 01
  [2023-06-03 12:49:12] INFO: Kono-Subarashil-Sekai-ni-Bakuen-wo 01 01 .mkv << [DMG&LoliHouse] Kono Subarashil Sekai ni Bakuen wo! - 01 [WebRip 1080p HEVC-10bit AAC ASSx2].mkv
  {'Bt': '[DMG&LoliHouse] Kono Subarashil Sekai ni Bakuen wo! - 01 [WebRip 1080p HEVC-10bit AAC ASSx2].mkv', 'Name': 'Kono-Subarashil-Sekai-ni-Bakuen-wo', 'Season': '01', 'Episodes': '01', 'FileType': '.mkv'}....Ok
  ```
  
* 如果您想在`Test`文件中屏蔽某一条test测试数据,直接在开头添加`#`即可
  ```json
  #{"Bt":"[DMG&LoliHouse] Kono Subarashil Sekai ni Bakuen wo! - 01 [WebRip 1080p HEVC-10bit AAC ASSx2].mkv","Name":"Kono Subarashil Sekai ni Bakuen wo","Season":"01","Episodes":"01","FileType":".mkv"}
  ```
## 📻 常见问题建议

* 在群晖NAS中，套件中心安装的`🐍python3`环境可能出现奇奇怪怪的问题，请使用第三方套件源(第三方源需要手动为`🐍python3`创建软连接至/usr/local/bin/python3)

* 如果你使用的是群晖NAS `🐳Docker`版的`🔵QBitTorrent`,你可以在容器日志中直接看到`AutoAnimeMv.py`输出的`简单Log信息`
> 如果您想要输出详细的Log信息，请启用`OPDETAILEDLOGFLAGS`配置 [配置?](#配置)
```ini
#config
OPDETAILEDLOGFLAGS = True #详细日志输出开关
```
  
# 📝 使用方法 
## 🚀Quick Start
 > `AutoAnimeMv.py`需要三到四个参数,`下载路径` `下载文件名` `下载文件数` `文件分类`(可选) 
 
 > 批处理模式下 `AutoAnimeMv.py`需要一到俩个参数,`下载路径` `文件分类`(可选) 

 > 更新模式下`AutoAnimeMv.py`需要一个至俩个参数,`update`(就是纯字符串update) `指定更新文件`

### 使用场景1-配合NAS(Linux)/Windows🔵Qbittorrent进行使用
  * 1.将`AutoAnimeMv.py`上传至`🔵QBittorrent`能访问的路径下
  
  * 2.在`🔵Qbittorrent`中创建`动漫`分类(非必须，当然不要分类也可以)

  * 3.修改qb配置: `下载`勾选 `Torrent 完成时运行外部程序`, 下面填上(传入参数顺序不可更改)
  
    ```
    python3 AutoAnimeMv.py放置路径 下载路径 下载文件名 下载文件数 文件分类(可选) 
    ```
    上面三个参数可以由`🔵Qbittorrent`传入，即
    ```
    python3 AutoAnimeMv.py放置路径 "%D" "%N" "%C" "%L"(可选)
    ```
     > <img src="./Image/Example/two.jpg" width="400" height="300"> <img src="./Image/Example/three.jpg" width="400" height="300">
  * 4.取消做种，修改qb配置: 将`🔵QBitTorrent `的`做种限制`改成`当分享率达到0当做种时间达到0分钟然后暂停torrent`

  * 5.现在你就可以下载一个番剧测试效果啦
    > 🚩举例，下面的文件名字都可以被识别`[Comicat][Jigokuraku][01][1080P][GB&JP][MP4].mp4` 
  
    >`【悠哈璃羽字幕社】[虚构推理_Kyokou Suiri ][09][x264 1080p][CHT].mp4`
  
    >` [桜都字幕组] 因为太怕痛就全点防御力了。第2季/ Itai No Wa Iya Nano De Bougyoryoku Ni Kyokufuri Shitai To Omoimasu. S2 [10][ 1080P@60FPS ][简繁内封].mp4`
  
    > 或者是带有干扰项的 `【喵萌奶茶屋】★01月新番★[英雄王，为了穷尽武道而转生～然后，成为世界最强的见习骑士♀～ / Eiyuuou, Bu wo Kiwameru Tame Tenseisu][10][720p][简体][招募翻译].mp4`

### 使用场景2-批处理本地已下载番剧
* 在Shell中执行以下代码,工具即可自动处理`下载路径`下的所有番剧和字幕文件
```
python3 AutoAnimeMv.py放置路径 下载路径 文件分类(可选) 
```
* 输出Log
```log
[2023-06-10 15:11:23] INFO: Running....
[2023-06-10 15:11:23] INFO: 当前工具版本为1.14.1
[2023-06-10 15:11:23] INFO: 当前操作系统识别码为nt,posix/nt/java对应linux/windows/java虚拟机
[2023-06-10 15:11:23] INFO: 接受到参数 ==> ['E:\\D\\fork\\AutoAnimeMv\\AutoAnimeMv.py ', 'E:\\D\\Test']
[2023-06-10 15:11:23] INFO: 现在是本地番剧文件批处理模式,正在扫描Path ==> E:\D\Test
[2023-06-10 15:11:23] INFO: 发现1个字幕文件 ==> ['[BeanSub&FZSD&LoliHouse] Jigokuraku - 09 [WebRip 1080p HEVC-10bit AAC ASSx2].简体中文.ass']
[2023-06-10 15:11:23] INFO: 发现3个番剧视频 ==> ['[ANi] 机动战士钢弹水星的魔女Season 2 - 18 [1080P][Baha][WEB-DL][AAC AVC][CHT][MP4].mp4', '[BeanSub&FZSD&LoliHouse] Jigokuraku - 09 [WebRip 1080p HEVC-10bit AAC ASSx2].mkv', '[Sakurato] Made in Abyss_ Retsujitsu no Ougonkyou [04v2][AVC-8bit 1080p AAC][CHS].mp4']
[2023-06-10 15:11:23] INFO: 匹配剧集 ==> 18
[2023-06-10 15:11:23] INFO: 通过剧集截断文件名 ==> -机动战士钢弹水星的魔女Season-2---
[2023-06-10 15:11:23] INFO: 番剧Name ==> 机动战士钢弹水星的魔女Season-2
[2023-06-10 15:11:23] INFO: id 2 TrueVideoName ==> 机动战士钢弹水星的魔女,Season ==> 02
[2023-06-10 15:11:23] INFO: 机动战士钢弹水星的魔女 02 18 .mp4 << [ANi] 机动战士钢弹水星的魔女Season 2 - 18 [1080P][Baha][WEB-DL][AAC AVC][CHT][MP4].mp4
[2023-06-10 15:11:23] INFO: 创建 机动战士钢弹水星的魔女\Season_02 完成
[2023-06-10 15:11:23] INFO: 字幕文件[BeanSub&FZSD&LoliHouse] Jigokuraku - 09 [WebRip 1080p HEVC-10bit AAC ASSx2].简体中文.ass已导入
[2023-06-10 15:11:25] INFO: 创建 E:\D\Test\机动战士钢弹水星的魔女\Season_02\S02E18.mp4 完成...一切已经准备就绪
[2023-06-10 15:11:25] INFO: 匹配剧集 ==> 09
[2023-06-10 15:11:25] INFO: 通过剧集截断文件名 ==> -Jigokuraku---
[2023-06-10 15:11:25] INFO: 番剧Name ==> Jigokuraku
[2023-06-10 15:11:25] INFO: id 4 TrueVideoName ==> Jigokuraku,Season ==> 01
[2023-06-10 15:11:25] INFO: Jigokuraku 01 09 .mkv << [BeanSub&FZSD&LoliHouse] Jigokuraku - 09 [WebRip 1080p HEVC-10bit AAC ASSx2].mkv
[2023-06-10 15:11:25] INFO: 创建 Jigokuraku\Season_01 完成
[2023-06-10 15:11:27] INFO: 创建 E:\D\Test\Jigokuraku\Season_01\S01E09.mkv 完成...一切已经准备就绪
[2023-06-10 15:11:27] INFO: 匹配剧集 ==> 04
[2023-06-10 15:11:27] INFO: 通过剧集截断文件名 ==> -Made-in-Abyss_-Retsujitsu-no-Ougonkyou-=
[2023-06-10 15:11:27] INFO: 番剧Name ==> Made-in-Abyss_-Retsujitsu-no-Ougonkyou
[2023-06-10 15:11:27] INFO: id 4 TrueVideoName ==> Made-in-Abyss_-Retsujitsu-no-Ougonkyou,Season ==> 01
[2023-06-10 15:11:27] INFO: Made-in-Abyss_-Retsujitsu-no-Ougonkyou 01 04 .mp4 << [Sakurato] Made in Abyss_ Retsujitsu no Ougonkyou [04v2][AVC-8bit 1080p AAC][CHS].mp4
[2023-06-10 15:11:27] INFO: 创建 Made-in-Abyss_-Retsujitsu-no-Ougonkyou\Season_01 完成
[2023-06-10 15:11:29] INFO: 创建 E:\D\Test\Made-in-Abyss_-Retsujitsu-no-Ougonkyou\Season_01\S01E04.mp4 完成...一切已经准备就绪
```

## 配置
### 使用内置配置
* `AutoAnimeMv.py` 内存在内置`config部分`,您可以自行配置相关参数(当不存在外置配置文件时使用)
```ini
#config
OPDETAILEDLOGFLAGS = True #详细日志输出开关
WINTOASTFLAGS = False #win弹窗通知开关 
USEFILELINKFLAGS = False #不使用MOVE改为使用硬链接进行番剧的整理(保种使用)
LINKFAILSUSEMOVEFLAGS = False #硬链接失败时使用MOVE
AUTOUPDATEFLAGS = True #自动更新开关
UPDATEURLPATH = 'https://raw.githubusercontent.com/Abcuders/AutoAnimeMv/main/' #UPDATEURL
NOUPDATELIST = 'AutoAnimeMv.py' #不更新列表
SKIPCHECKBEFOREUPDATEFLAGS = False #跳过自动解决更新前检查到的问题(更新覆盖内置自定义配置)
USEGITHUBANIMELISTFLAG = True #使用Github上的AnimeList文件
USELOCALANIMELISTFLAGS = False #使用本地的AnimeList文件
USINGPROXYFLAGS = True #使用代理开关,如果您的代理服务器需要认证,请使用 账号:密码@ip:port 这样的格式
HTTPPROXY = 'http://127.0.0.1:7890' #Http代理,请根据您的实际情况填写  
HTTPSPROXY = 'http://127.0.0.1:7890' #Https代理,请根据您的实际情况填写
SOCKS5PROXY = '' #SOCKS5代理,请根据您的实际情况填写
USEBGMAPIFLAGS = True #使用BgmApi进行更准确的识别
FORCEDUSEBGMAPI = False #强制使用BgmApi进行识别,不查询AimeList文件
BGMAPIURLPATH = 'https://api.bgm.tv/search/subject/' #BGMAPIURL
```
### 使用外置配置
* `Config.ini` 是外置配置文件,把它放在`AutoAnimeMv.py`的目录下,`AutoAnimeMv.py`便会自行加载
* 在外置配置文件没有配置的参数仍旧会使用内置配置
* *如何编写`Config.ini`请见上面*

> 使用外置配置的输出Log
  ```log
  [2023-06-12 00:54:39] INFO: 正在读取外置ini文件
  [2023-06-12 00:54:39] INFO: 配置 < AUTOUPDATEFLAGS = False
  ```

***

## 启用自动更新(可选)
* 安装`requests` `🐍Python依赖库`
* 检查`AUTOUPDATEFLAGS`配置开关为`True` [配置?](#配置)
  ```ini
  #config
  AUTOUPDATEFLAGS = True #自动更新开关
  ```
  > 如果您使用了代理,您还需要检查`USINGPROXYFLAGS`配置开关为`True`,并`配置代理信息`
  ```ini
  #config
  USINGPROXYFLAGS = True #使用代理开关,,如果您的代理服务器需要认证,请使用 账号:密码@ip:port 这样的格式
  HTTPPROXY = 'http://127.0.0.1:7890' #Http代理,请根据您的实际情况填写  
  HTTPSPROXY = 'http://127.0.0.1:7890' #Https代理,请根据您的实际情况填写  
  SOCKS5PROXY = '' #SOCKS5代理,请根据您的实际情况填写
  ```
* 在Shell中执行以下代码,即可更新相关文件
  ```bash
  python3 AutoAnimeMv.py update
  ```
* 输出Log
  ```log
  [2023-06-10 20:31:54] INFO: 当前工具版本为1.14.1
  [2023-06-10 20:31:54] INFO: 当前操作系统识别码为nt,posix/nt/java对应linux/windows/java虚拟机
  [2023-06-10 20:31:54] INFO: 接受到参数 ==> ['.\\AutoAnimeMv.py', 'update']
  [2023-06-10 20:31:54] INFO: 准备更新中
  [2023-06-10 20:31:55] INFO: 最新版 ==> 1.15.0,可更新的文件 ==> ['AutoAnimeMv.py']
  [2023-06-10 20:31:56] INFO: 更新 ==> AutoAnimeMv.py
  [2023-06-10 20:31:56] INFO: 全部已更新完毕
  ```
* 设置定时检查更新
> NAS(Linux)用户您可以使用`Crontab`或其他定时任务功能进行自动检查更新

> Win用户您可以使用`计划任务程序`进行自动检查更新

### 高级选项
* 您可以使用以下命令来指定下载更新某个文件,指定更新文件不受更新排除列表的限制
```
python3 AutoAnimeMv.py update 指定文件
```
* 您可以配置更新排除列表,让工具跳过某些文件的更新,配置方法如下
```ini
#config
NOUPDATELIST = '不想更新的文件1','不想更新的文件2','不想更新的文件3'  #不更新列表
```

* 如果您在更新主程序时没有配置外置config文件,工具会提醒您,并自动将您自定义的内置配置重写至config.ini文件中
```log
[2023-06-13 00:07:19] WARNING: 更新前检查到您没有配置外置config.ini,如果直接更新您的自定义配置将变为默认配置
[2023-06-13 00:07:19] INFO: 正在将您自定义的内置配置重写至config.ini文件中
```
> 您也可以关闭自动重写功能,开启`SKIPCHECKBEFOREUPDATEFLAGS`即可 [配置?](#配置)
```ini
#config
SKIPCHECKBEFOREUPDATEFLAGS = True #跳过自动解决更新前检查到的问题(更新覆盖内置自定义配置)
```

## 使用硬链接整理番剧
* 如果您想要保种,只需要启用(注意exFAT文件系统不支持软链接与硬链接)
> 如果您想在硬链接失败时改为使用MOVE处理番剧,请开启`LINKFAILSUSEMOVEFLAGS`

```ini
#config
USEFILELINKFLAGS = True #不使用MOVE改为使用硬链接进行番剧的整理(保种使用)
LINKFAILSUSEMOVEFLAGS = False #硬链接失败时使用MOVE
```
* 相关Log
```log
[2023-06-12 15:34:26] INFO: 创建 地狱乐\Season_01 完成
[2023-06-12 15:34:26] INFO: 字幕文件[BeanSub&FZSD&LoliHouse] Jigokuraku - 09 [WebRip 1080p HEVC-10bit AAC ASSx2].简体中文.ass已导入(硬链接)
[2023-06-12 15:34:26] INFO: 硬链接至 D:\D\Test\地狱乐\Season_01\S01E09.mkv 完成...一切已经准备就绪
```
* **💞小贴士**:如果您使用`保种功能`,我们建议您搭配`分类功能`使用 

## 开启下载并整理完成进行通知功能(可选)

### Windows下使用WinAPI进行通知
* 安装`win10toast` `🐍Python依赖库`
* 将`WINTOASTFLAGS`开关改为`True` [配置?](#配置)
  ```ini
  #config
  WINTOASTFLAGS = True #win弹窗通知开关 
  ```
* 一切准备就绪后,当番剧下载并整理完成Win将弹窗提醒您

### 使用`🔵Qbittorrent`的Mail提醒功能
* 进行`🔵Qbittorrent`设置>>`下载`选项
* 启用`下载完成时发送电子邮件通知`功能,填好相关配置
* 一切准备就绪后,当番剧下载并整理完成`qb`将发送Mail提醒您
> <img src="./Image/Example/four.jpg">

# 🧉 BB一下

* ⚠️本程序显然存在诸多问题，在此恳请各位大佬不吝赐教
* 23/5/26:下周我推要播总集篇，每周的精神食粮要断粮了😭😭没有你我怎么活呀，燕子！
* 23/6/1:嘿嘿嘿，无神真好看🤤

# ⭐ 贡献者 ✨

**感谢这些有趣又很棒的人！！！**
> 如果您也想要为这个项目添砖加瓦,可以直接来[Issues](https://github.com/Abcuders/AutoAnimeMv/issues)提出您宝贵的建议或者@我问一下能做些什么

<a href="https://github.com/wzfdgh">
<img src="https://avatars.githubusercontent.com/u/93830081?s=96&v=4"  width="60px" height="60px"> 
</a>
<a href="https://github.com/Nanako718">
<img src="https://avatars.githubusercontent.com/u/60038246?s=96&v=4"  width="60px" height="60px">
</a>

# Star History
[![Star History Chart](https://api.star-history.com/svg?repos=Abcuders/AutoAnimeMv&type=Date)](https://star-history.com/#Abcuders/AutoAnimeMv)

# 🧾 声明

**该仅供个人合法用途,任何使用该工具进行直接或者间接非法盈利活动的行为,均不属于授权范围,也不受到任何支持和认可**
