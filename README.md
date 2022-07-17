# 修改微信运动步数
使用**Zepp Life** app（*原**小米运动**app*）修改微信步数，2022.7.16亲测成功，需要[阿里云](https://tianchi.aliyun.com/notebook-ai "不需要magic network")或者[Google Colab](https://colab.research.google.com/ "需要magic network"):raised_eyebrow:

## 目录
* [准备工作](#准备工作)
* [使用步骤](#使用步骤)
* [更新日志](#更新日志)

## 准备工作
  - 下载`changebushu.py`
  - 登录[阿里云](https://tianchi.aliyun.com/notebook-ai "不需要magic network")或者[Google Colab](https://colab.research.google.com/ "需要magic network")

## 使用步骤
### 阿里云
  - 在阿里云上传`changebushu.py`
  - 修改用户登录手机号和密码，一定要是注册`Zepp Life app`的
  - 修改步数范围，尽量保持在`10000~12000`之间。保存修改后的`.py`文件
  - 新建一个`terminal`
  ```python
  python3 changebushu.py
  ```
  - 当弹出的信息中出现修改成功后，登录微信运动查看
  
### GoogleColab
*阿里云要到期了:laughing:不想继续掏钱所以找到了Google Colab*:zany_face:
  - 在GoogleColab新建一个`.ipynb`文件，点击`+Code`增加一个代码块（一个就够了！）
  - 把`changebushu.py`里面的代码全部复制进这一个代码块里
  - 修改用户登录手机号和密码，一定要是注册`Zepp Life app`的
  - 修改步数范围，尽量保持在`10000~12000`之间
  - 直接运行这个代码块即可

## 更新日志
  - **`v0.1`** 2022.5.11：第一次上传
  - 2022.7.16：添加`Google Colab`的使用方法

