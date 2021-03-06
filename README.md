# 解决ncuwlan自动断网的问题
## 2019.1.17
如果经常更新会写在语雀：https://www.yuque.com/zhiwa/ideas/srbyga

```bsah
cd pyqt5-ncuwlan
pyinstaller -F --icon=us-wifi.ico us-wifi.py
```

近来ncuwlan的网与机房ncuhome_edu的网经常断线，为许多人带来了不方便，有人吐槽主教的网打游戏断线qaq，写个脚本用python连一下非常简单，但是很多人并不拥有python的环境，并且，账号多端登录会容易掉线，于是想到写一个桌面程序来解决这一个问题。


## 用户体验层
![liuct](/yuque.png)

## 业务实现层思路
使用pyqt5编辑窗口，用户第一次验证时储存信息
通过os.path获取当前路径，在相关目录下创建新的目录或直接在当前目录下创建隐藏文件（.json .txt都可以 加密储存）。

#### 设置隐藏文件，前提是有了test.txt文件
```python
import os
fn = '***test.txt***'
p = os.popen('attrib +h ' + fn)
p.close()
```

用户第二次登录时，判断是否存在该文件（进行验证），如果存在文件则直接执行检查网络和自动连接。

检查网络与发送请求
每隔6秒访问一些相应较快的网页，这样的网页最好准备多一些，这样更礼貌。当访问超时（5s）时，重新发送验证请求。



## 还能（需要）做什么
#### 安装包
和许多Windows下软件安装一样，让用户能自定义安装的位置并且设能够uninstall，将环境配置好并且创建桌面的快捷方式。或许也可以使用pyqt5写。


#### 发送错误报告
之前已经创建了 error log，有机会可以将它发送到接收服务器，便于开发者的维护和优化。


#### 退出登录/注销
其实这个不需要做或者说已经做到了，用户需要的是网络而不是账户登录，当账户发送更变时（账户注销），清除  remove 之前存储用户信息的文件。


#### 尝试自动分辨与连接
解决方案：访问学校不同的已知wifi请求的ip接口，连得上的话就可以判断用户用的是哪一个WiFi，之后的思路相似。


#### 更好看
我也很想知道，能不能更好看呢？！


## 其他
pyqt5的hello world
https://www.yuque.com/zhiwa/deepin/rb7shz

Python3.x：打包为exe
https://www.yuque.com/zhiwa/deepin/of5e9c

