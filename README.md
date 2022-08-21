# 修改微信运动步数
通过Github Action/[阿里云](https://tianchi.aliyun.com/notebook-ai "不需要magic network")/[Google Colab](https://colab.research.google.com/ "需要magic network")使用 **Zepp Life** app（*原**小米运动**app*）修改微信步数，Github Action 可设置每日定时执行。
> 2022.8.18亲测成功:ghost:

[![修改微信步数](https://github.com/Caryio/ZeppLifeChangeWechatSport/actions/workflows/RunFunction.yml/badge.svg?branch=main)](https://github.com/Caryio/ZeppLifeChangeWechatSport/actions/workflows/RunFunction.yml)
## 目录
* [准备工作](#准备工作)
* [使用指南](#使用指南)
  * [通过GithubAction](#通过githubaction)
    * [GitHubAction设置每日定时执行](#githubaction设置每日定时执行)
  * [通过阿里云](#通过阿里云)
  * [通过GoogleColab](#通过googlecolab)
* [注意事项](#注意事项)
* [更新日志](#更新日志)
* [声明](#声明)

## 准备工作
使用本仓库需要 Zepp Life app（*原小米运动app*），请务必把 Zepp Life 注册好，设置好，与微信的同步/第三方接入什么的都弄好再往下看

<p align="right">（<a href="#修改微信运动步数">回到顶部</a>）</p>
  
## 使用指南
### 通过GithubAction
   1. Fork 本仓库
   2. 在你自己 Fork 的仓库进行设置`Settings - Actions - General - Allow all actions and reusable workflows`，别忘了`save`
   3. 然后`Settings - Secrets - Actions - New repository secret`，按下面例子新建几个`secrets`：

   <table>
    <tr>
     <td colspan="2">确切步数修改</td>
     <td colspan="2">随机步数修改</td>
    </tr>
    <tr>
     <td>Name</td>
     <td>Value</td>
     <td>Name</td>
     <td>Value</td>
    </tr>
    <tr>
     <td>USER_PHONE</td>
     <td>18899996666</td>
     <td>USER_PHONE</td>
     <td>18899996666</td>
    </tr>
    <tr>
     <td>USER_PWD</td>
     <td>abc123</td>
     <td>USER_PWD</td>
     <td>abc123</td>
    </tr>
    <tr>
     <td>STEP</td>
     <td>10000</td>
     <td>STEP_MIN</td>
     <td>10000</td>
    </tr>
    <tr>
     <td colspan="2">------</td>
     <td>STEP_MAX</td>
     <td>12000</td>
    </tr>
   </table>
   
   （`USER_PHONE`是注册Zepp Life app的手机号，`USER_PWD`是账号密码，**`STEP_MIN`必须小于`STEP_MAX`**，最后修改的步数为二者之间随机数）
   
   4. 然后到`changebushu_Action.py`里选择到底需要确切还是随机，以下两种二选一，前者步数修改随机，后者步数修改确切。记得把另一句注释掉：
```python
   step = str(randint(int(os.environ['STEP_MIN']), int(os.environ['STEP_MAX'])))
   step = os.environ['STEP']
```
   确认一切无误就可以去`Actions`里`Run workflow`
   
**如果不想设置 secrets 或者看了上面内容依然设置不好，*请先看[声明第四条](#声明)*，然后自己决定要不要使用以下方法：直接修改[这个yml文件](/.github/workflows/RunFunction.yml)，把`${{ secrets.USER_PHONE }}`、`${{ secrets.USER_PWD }}`、`${{ secrets.STEP }}`等相关参数设置好，然后直接去 Actions 里 Run workflow 。但是要注意因为直接 fork 的仓库默认是公开`public`状态，所以你的个人隐私信息可能暴露！开发者不对此负任何责任。~~其实从这个方面来说还是设置secrets更香:stuck_out_tongue_closed_eyes:~~** 

<p align="right">（<a href="#修改微信运动步数">回到顶部</a>）</p>
  
#### GitHubAction设置每日定时执行
直接修改[这个yml文件](/.github/workflows/RunFunction.yml)，把以下两句解除注释：

```
schedule:
    - cron: '0 9,12 * * *'
```
即可每日在北京时间17:00、20:00运行。但 Action 的 schedule 经常出现**不准时运行**的情况，比如定了20:00却拖到20:50（甚至更晚）。而且第一天修改**很可能当天不会执行**。

修改里面的时间可以自己确定运行时间，要注意的是里面的数字指的是 UTC 时间，换算成北京时间要加8h。

关于 GitHub Action 定时执行，请看[与此相关的 GitHub 官方文档](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#schedule)。

<p align="right">（<a href="#修改微信运动步数">回到顶部</a>）</p>

### 通过阿里云
  1. 下载`changebushu.py`
  2. 登录[阿里云](https://tianchi.aliyun.com/notebook-ai "不需要magic network")并进入到CPU或者GPU环境，在里面上传`changebushu.py`
  3. 修改用户登录手机号`user`和密码`password`，一定要是注册`Zepp Life app`的
  4. 修改步数，以下两种二选一，前者步数修改确切，后者步数修改随机。记得把另一句注释掉：
```python
step = ''
step = str(randint(10121, 12302))
//确保前面的数字小于后面的数字
```
  
  保存修改后的`.py`文件
  6. 新建一个`terminal`
  ```bash
  python3 changebushu.py
  ```
<p align="right">（<a href="#修改微信运动步数">回到顶部</a>）</p>

### 通过GoogleColab
*阿里云要到期了:laughing:不想继续掏钱所以找到了Google Colab*:zany_face:
  1. 在GoogleColab新建一个`.ipynb`文件，点击`+Code`增加一个代码块（一个就够了！）
  2. 把`changebushu.py`里面的代码全部复制进这一个代码块里
  3. 修改用户登录手机号`user`和密码`password`，一定要是注册`Zepp Life app`的
  4. 修改步数，以下两种二选一，前者步数修改确切，后者步数修改随机。记得把另一句注释掉：
```python
step = ''
step = str(randint(10121, 12302))
//确保前面的数字小于后面的数字
```

  5. 直接运行这个代码块即可
  
<p align="right">（<a href="#修改微信运动步数">回到顶部</a>）</p>
  
## 注意事项
* 不保证一定成功，出问题概不负责嗷:innocent:
* Github Action 要用`changebushu_Action.py`，阿里云和 Google Colab 要用`changebushu.py`，别弄混了。*（不光是环境变量配置的问题，`changebushu_Action.py`里删除了很多调试参数输出，以确保不会在`workflow`里输出隐私信息）*
* Github Action 设置`secrets`时注意要按照上文的步骤弄，***不要***先设置`Environments`然后在里面加变量
* 实在设置不好可以看上文中不想设置`secrets`如何解决，但是**请先看[声明第四条](#声明)**

<p align="right">（<a href="#修改微信运动步数">回到顶部</a>）</p>
  
## 更新日志
*删除了很多 commits 记录，都快被我删没了:rofl:所以在这稍微记录一下*
  - **`v0.1`** 2022.5.11：第一次上传，添加阿里云的使用方法
  - 2022.7.16：添加 Google Colab 的使用方法；部分代码修改
  - **`v0.2`** 2022.7.17：添加 Github Action 的使用方法；重写`README.md`；部分代码修改
  - **`v0.3`** 2022.7.21：增加随机步数选择
  - 2022.7.22：增加GitHub Action每日自动执行
  
<p align="right">（<a href="#修改微信运动步数">回到顶部</a>）</p>

## 声明
- 本项目仅供编程学习/测试使用
- 请在国家法律法规和校方/公司相关原则下使用
- 开发者不对任何下载者和使用者的任何行为负责
- 程序使用的所有信息均利用 Github 的 [Encrypted secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) 加密，如果下载者和使用者通过上文中描述的“直接修改[这个yml文件](/.github/workflows/RunFunction.yml)”的方法导致任何个人信息泄露，开发者不对此负责。开发者已经提供使用 Github 的 [Encrypted secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) 加密的方法。

<p align="right">（<a href="#修改微信运动步数">回到顶部</a>）</p>
