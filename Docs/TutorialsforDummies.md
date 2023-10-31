# | AutoAnimeMV: 杂~鱼♡杂~鱼♡
<div align="center">
  <a href="https://github.com/Abcuders/AutoAnimeMV">
    <img src="./Image/logo.png">
  </a>

**全自动追番新时代！不动手才是硬道理！**


**简体中文 | English文档无**

*! En-README.md 由于我精力不够所以有太多落后未更新的地方,如果您感兴趣并且有时间的希望您能帮助一下我✊*

[![ GitHub 许可证](https://img.shields.io/github/license/Abcuders/AutoAnimeMv)](https://github.com/Abcuders/AutoCartoonMv/LICENSE) [![GitHub release](https://img.shields.io/github/v/release/Abcuders/AutoAnimeMv)](https://github.com/Abcuders/AutoAnimeMv/releases/) [![telegram](https://img.shields.io/badge/telegram-AutoAnimeMv-blue?style=flat&logo=telegram)](https://t.me/+3q1JuBrrPkJkOWJl)

</div>

***

# 正文
* 首先告诉你 `AutoAnimeMv`(以下简称`AAM`) 有三种模式，每种模式的食用方法都不一样

* 先说明第一个模式 也就是 `QB下载模式` 这个模式下，QB每下一个番剧,都会启动 `AAM` 让TA去处理刚刚下载的番剧 >> [使用方法](#qb下载模式的小白式使用方法)

* 第二个模式 是 `批处理模式` 这个模式下，你可以对已经下载好的番剧进行整理(只处理字幕也可以，工具会自动识别的) >> [使用方法](#批处理模式的小白式使用方法)

* 第三个模式就是 `更新模式` 这个模式下你可以进行工具的联网自动更新

# 使用方法
## QB下载模式的小白式使用方法
* 第一步 把 `AAM` 仓库的全部文件 上传到QB能访问的目录下


* 第二步 安装AAM的所需依赖
    > 这里要注意请辨别你使用的是 Docker版本的QB 还是其他版本的QB
    
    > 如果你不知道如何辨别自己的版本是不是 Docker版本的QB 那么您的版本就是 其他版本的QB
    * Docker版本的QB 请使用下面的安装方法
    > Docker QB 自带了python3，所以你不需要安装python3

    * 开启Docker QB,进入到QB Docker内部 执行这段代码即可安装相关依赖
        
        ```shell
        python3 get-pip.py install -r requirements.txt
        ```

    * 非Docker版本的QB 请使用下面的安装方法

    * Windows或Linux 用户 执行 这段代码即可安装相关依赖
        > 首先你要有安装Python3哦 !
    
        ```shell
        python3 get-pip.py install -r requirements.txt
        ```

* 第三步 在QB里进行配置
    * 1.在`🔵Qbittorrent`中创建`动漫`分类(非必须)

    * 3.修改qb配置: `下载`切换`Torrent 内容布局`为`不创建子文件夹`

    * 4.修改qb配置: `下载`勾选 `Torrent 完成时运行外部程序`, 在输入框填入如下内容(参数顺序不可更改且参数要用`""`包裹,其中 `/dir/to/AAM.py` 更换为步骤一中脚本放置的绝对路径,如没有配置`分类`,请删除`"%L"`)

    ```shell
    python3 /dir/to/AAM.py "%D" "%N" "%C" "%L"(可选)
    ```
    > <img src="./Image/Example/two.jpg" width="300" height="300"> <img src="./Image/Example/three.jpg" width="300" height="300">
    * 4.取消做种，修改qb配置: 将`🔵QBitTorrent `的`做种限制`改成`当分享率达到0当做种时间达到0分钟然后暂停torrent`
* 第四步 没有了，到此 `AAM` 就安装完毕了，你可以在 [详细的文档](./DOCS.md) 中进行更高级更自定义的设置

## 批处理模式的小白式使用方法
* 第一步 
* 第二步 安装AAM的所需依赖
> 见上面 `QB下载模式的小白式使用方法` 的第二步
* 第三步 使用 `AAM` 批处理番剧
> 传入参数顺序不可更改且参数要用`""`包裹

```
python3 AutoAnimeMv.py "需要整理的番剧所在路径" "文件分类(可选)"
```
* 你可以在 [详细的文档](./DOCS.md) 中进行更高级更自定义的设置
