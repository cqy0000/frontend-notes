# 搭个简易梯呗（MAC版）

记录自己搭建的主要过程，并不详细讲解

## 买个VPS服务器

用的[vultr](https://my.vultr.com/)，最后服务器配置如下：
![vultr](images/vutrl.png 'vutrl配置')

deploy成功后，先ping一下IP，如果不能传数据，就destroy这个instance，换一个location再走一遍

## 连接到VPS

### 连接VPS服务器
```
ssh root@hostname // hostname是当前VPS的IP
```
根据提示输入密码(上图网页中的password，直接复制粘贴)
出现root@vultr，说明已经登入成功

###  V2ray一键安装脚本命令

```
bash <(curl -s -L https://git.io/v2ray.sh)
```
一路回车确定配置

### 生成vultr链接

```
v2ray url
```

## 安装v2ray客户端

v2ray下载地址：https://github.com/2dust/v2rayN/releases

### 配置v2ray的configure

点击import from other links..., 将刚才生成的vultr链接导入，点击完成

![v2ray](images/v2ray.png 'v2ray配置')



### 运行v2ray

点击load core， 点击PAC模式

![v2ray](images/v2ray2.png 'v2ray配置2')


### 修改PAC配置

有时候github上面图片显示不出来，可以修改PAC配置
添加一行：".githubusercontent.com"
