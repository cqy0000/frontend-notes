# 下载安装视频

## 安装 youtube-dl
官网地址：https://github.com/ytdl-org/youtube-dl

```
brew install youtube-dl
```

## 安装ffmpeg

```
brew install ffmpeg
```

## 下载视频

```
youtube-dl -F --proxy socks5://127.0.0.1:1081 https://www.youtube.com/watch?v=Y2_lrL1ebHw //搜索视频下载信息

youtube-dl -f 303+251 --proxy socks5://127.0.0.1:1081 https://www.youtube.com/watch?v=Y2_lrL1ebHw // 下载高清1080视频时，音频和视频是分开下载的
```

下载视频其他的参数可以看官网，按需添加

## 安装运行autosub

官网地址：https://github.com/BingLingGroup/autosub/blob/dev/docs/README.zh-Hans.md

直接下载git源代码，解压缩

```
cd 项目
pip3 install .
```

tips: 更改本地python的版本

```
python --version // 查看版本，如果不是3.*，修改
open ~/.bash_profile
alias python=python3
source ~/.bash_profile
```

## 配置讯飞语音听写

申请讯飞账号，填写配置文件
讯飞API详解地址：https://www.xfyun.cn/doc/asr/voicedictation/API.html#%E6%8E%A5%E5%8F%A3%E8%AF%B4%E6%98%8E

```
{
    "app_id": "",
    "api_secret": "",
    "api_key": "",
    "business": {
        "language": "en_us",
        "domain": "iat",
        "accent": "mandarin"
    }
}
autosub -sapi xfyun -i '1.mp4' -sconf xunfei.json
```
生成字幕文件：1.en_us.srt

## 视频添加字幕

```
ffmpeg  -i '1.mp4' -vf subtitles=1.en_us.srt output.mp4
```
