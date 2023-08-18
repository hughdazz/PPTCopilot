# README

2023.8.18 : 更新下具体原理供各位参考:

我们的前端有两个界面，一个是项目管理界面，基于vue-element-admin修改，不过后期由于我个人的喜好将element换成了腾讯的tdesign库；一个是ppt编辑界面，基于g站上pptist修改而来，该项目ppt的内部表示方式是JSON，这就给我们修改的空间

我们的后端是基于beego框架从0搭建

如果要运行起来，你要去后端的conf里加入你的OPENAI API KEY，然后也需要Clash代理本地7890端口

生成PPT的流程是：

1. 前端接受到一个ppt的主题(topic)，发送到后端
2. 后端请求chatgpt，返回一个xml格式的大纲，这是我们的prompt工程
3. 后端返回大纲到前端，前端进行解析并让用户修改
4. 前端将修改后的PPT发送到后端
5. 后端将xml中的每一页概述发给chatgpt，进行请求，得到有具体内容的xml，这样能突破chatgpt的字数限制，可以生成任意多ppt
6. 数据库中事先存了一些ppt模版，这些ppt模版遵循固定格式，方便进行文本替换，如`{{title}}`之类
   进行文本替换，得到完整ppt
7. 代表ppt的JSON返回给前端，直接渲染、展示

## 项⽬简介

本⽹站旨在打造⼀个提供能够根据由⾃然语⾔描述的需求，基于ChatGPT提供的NLP服务，⾃动⽣成内容符合需求描述的格式化⽂档。该格式化⽂档中的内容描述了PPT⽂档的幻灯⽚分⻚，每个幻灯⽚分⻚中的主标题内容、N级标题和主要⻚⾯内容。再将格式化⽂档的内容转为PPT⽂档，从⽽能够在线对于其样式（包括⼀般⽂本框、图⽚、图形等元素对象的⼤⼩，位置，颜⾊等等）进⾏编辑的⽂档处理聚合平台，为⼴⼤有⽂档⾃动化⽣成和在线处理需求的相关⾏业从业者提供相关服务。

在线使用地址:http://...(学校经费停了)

以下是项⽬的部分演⽰截图：

![""](https://raw.githubusercontent.com/hughdazz/PPTCopilot/master/.image/start.png)

![""](https://raw.githubusercontent.com/hughdazz/PPTCopilot/master/.image/ground.png)

![""](https://raw.githubusercontent.com/hughdazz/PPTCopilot/master/.image/yanshi.png)

## 使⽤说明

### 浏览ppt项⽬、收藏项⽬、克隆项⽬、查看项⽬信息：

在项⽬⼴场⻚⾯，展⽰现有的所有项⽬

⻚⾯导航栏中具有⼀个“搜索”的按钮，可以点击，输⼊信息，对项⽬进⾏搜索

点击项⽬⼴场中的项⽬，可以查看该项⽬的详细信息与⽂件

在显⽰项⽬详细信息的⻚⾯，可以通过“添加收藏”按钮对项⽬进⾏收藏，并可以在个⼈空间中看⻅收藏的项⽬

在显⽰项⽬详细信息的⻚⾯，可以通过“克隆项⽬”按钮对项⽬进⾏克隆，并可以在我的项⽬中看⻅克隆的项⽬，并可以看⻅并编辑其下所有⽂件

### 新建、删除项⽬、更新项⽬信息：

⽤⼾可以在我的项⽬⻚⾯点击“新建项⽬”按钮，来添加新的项⽬

⽤⼾可以在我的项⽬⻚⾯中对特定项⽬点击“更多”中的“删除”，来删除已有项⽬

⽤⼾在显⽰项⽬详细信息的⻚⾯，可以通过点击“编辑信息”按钮对项⽬的名称与简介进⾏编辑，完成后点击“保存信息”即可完成信息更新

⽤⼾可以在我的项⽬⻚⾯中对特定项⽬点击“更多”中的“上传封⾯”并上传图⽚⽂件，来更新该项⽬的封⾯

### 上传、删除、下载、重命名⽂件：

⽤⼾在显⽰项⽬详细信息的⻚⾯，可以通过点击“上传⽂件”按钮进⾏⽂件上传

⽤⼾在显⽰项⽬详细信息的⻚⾯中的⽂件列表中，可以通过点击特定⽂件“更多”中的“删除”

按钮进⾏⽂件删除⽤⼾在显⽰项⽬详细信息的⻚⾯中的⽂件列表中，可以通过点击特定⽂件“更多”中的“下载”按钮进⾏⽂件下载

⽤⼾在显⽰项⽬详细信息的⻚⾯中的⽂件列表中，可以通过点击特定⽂件“更多”中的“重命名”按钮进⾏⽂件重命名

### PPT⽣成、修改、删除：

⽤⼾在显⽰项⽬详细信息的⻚⾯，可以通过点击“新建PPT”按钮进⾏PPT⽣成，在跳出的

对话框中输⼊幻灯⽚标题并确认：

![""](https://raw.githubusercontent.com/hughdazz/PPTCopilot/master/.image/confirm.png)

在接下来的⻚⾯中输⼊主题与汇报⼈姓名，选择模板，点击创建ppt:

![""](https://raw.githubusercontent.com/hughdazz/PPTCopilot/master/.image/template.png)

等待⼀段时间后会显⽰⼤纲，点击右边的“Append”和“Edit”可对⼤纲进⾏编辑：

![""](https://raw.githubusercontent.com/hughdazz/PPTCopilot/master/.image/outline.png)

点击“创建ppt”按钮并等待⼀段时间（时间较⻓，若中间出现蓝⾊模板，请不要操作继续等待），显⽰PPT编辑⻚⾯：

![""](https://raw.githubusercontent.com/hughdazz/PPTCopilot/master/.image/ppt.png)

使⽤⿏标键盘和右边功能栏可对PPT进⾏编辑，具体使⽤⽅法⻅附录

退出该界⾯后，项⽬详情⻚会出现对应的.json⽂件：

![""](https://raw.githubusercontent.com/hughdazz/PPTCopilot/master/.image/file.png)

按照对⽂件的处理⽅法可对该⽂件进⾏重命名、下载和删除操作

若要修改PPT内容，可点击“打开”按钮，等待⼀段时间，跳转到PPT编辑⻚⾯进⾏编辑，

完成后点击右上⻆“导出”按钮，选择“保存到云端”即可完成修改

![""](https://raw.githubusercontent.com/hughdazz/PPTCopilot/master/.image/store.png)

![""](https://raw.githubusercontent.com/hughdazz/PPTCopilot/master/.image/export.png)

### 注册,登录,注销,个⼈信息维护功能：

⽤⼾在登录界⾯底端点击“注册”，给出⽤⼾名、密码以及邮箱来注册⾃⼰在本系统中的账号

在注册账号后，⽤⼾可以在登录界⾯输⼊⽤⼾名/邮箱和密码登录账号，并且正常使⽤系统的各个功能

在登录了账号之后，⽤⼾可以通过点击导航栏右上⻆的“登出”按钮来退出当前登录的账号

⽤⼾还可以通过个⼈中⼼的“上传头像”来修改⾃⼰的⽤⼾头像，进⾏个⼈信息的维护

## docker-compose部署

支持一键部署

```bash
docker-compose up
# 或
docker-compose up -d # 后台运行
```

如果希望在本地运行，在docker-compose.yaml里修改相关的SERVER_IP灯信息

```yaml
      # ...
        MYSQL_HOST: mysqldb
        MYSQL_PORT: 3306
        SERVER_IP: "localhost"
```

也可以分别部署一部分服务

- 后端

  ```bash
  docker-compose up pptcopilot-backend
  ```

- 前端

  ```bash
  docker-compose up pptcopilot-project pptcopilot-editor
  ```

在源码进行更新时，若要重新部署，请用

```bash
docker-compose build
```

停止服务

```bash
docker-compose down
```

## 维护者

该项⽬⽬前由同济⼤学计算机科学与技术系WinterIsComming⼩组开发维护。
