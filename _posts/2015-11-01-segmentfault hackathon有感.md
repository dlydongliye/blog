---
layout: post
title: Segmentfault
category : 扯淡
tagline: "Supporting tagline"
tags : [Segmentfault]
---
{% include JB/setup %}
# Segmentfault Hackathon参与有感
---

@(hackathon)[Segmentfault|Android|Markdown]()

**Hackathon**  编程马拉松的灵魂是合作地编写程序和应用。 编程马拉松的时长一般在几天到一周不等。编程马拉松不是编写些一次性作品那么简单。编程马拉松的精髓在于：很多人，在一段特定的时间内，相聚在一起，以他们想要的方式，去做他们想做的事情——整个编程的过程几乎没有任何限制或者方向。
- [Segmentfault]()[1]：SegmentFault 是一家中文的开发者社区及媒体。最初的产品原型来自于国外最大的程序员问答社区 StackOverflow、现阶段获得1024 万融资；
- [Markdown]()[2]()：简洁高效的编辑器；
- 队伍 ：NullPointer团队：阿蔡，阿媛，阿乐。

---- ---------------
<!--break-->

[TOC]()

## High View

> 像使用水煤电一样，使用无人机，我们是无人机中的uber，uber共享经济的具体实现，采用阿里百川的SDK，结合亿航的无人机优势，采用最新的spring-boot和REST后端服务，Android端采用Material design设计，retrofit网络请求。    —— [维基百科]()(https://zh.wikipedia.org/wiki/uber)

### Spring Boot (服务器端)
```java
`@Controller
@EnableAutoConfiguration
public class SampleController {

@RequestMapping("/")
@ResponseBody
String home() {
return "Hello World!";
}

public static void main(String[]() args) throws Exception 
{
SpringApplication.run(SampleController.class, args);
}
}
```
` 

### Retrofit（Android端）
``` java
`@GET
public interface GitHubService {
  @GET("/users/{user}/repos")
  Call\<List\<Repo\>\> listRepos(@Path("user") String user);
}

@GET("/users/list")

@GET("/group/{id}/users")
List\<User\> groupList(@Path("id") int groupId);

@POST("/users/new")
Call\<User\> createUser(@Body User user);
```
`### NullPointer
  Segment fault基于Stackoverflow设计，而Stackoverflow在程序的世界里是堆栈溢出的意思，所以我们设计出了NullPointer的队名，在程序里意为空指针；
##### 招募队员：由于和scipio是好基友，看完segmentfault的hackathon果断参赛，由于需要路演，急需感兴趣单身美女一枚（原谅我们的初心，墙角蹲一会），外加上程序媛还会产品设计等多项职能，果断邀请程序媛美美参赛；
  队长是来自腾讯SNG的阿蔡，擅长java后端和服务器，队员来自牛掰的招联咯，我负责Android端，阿媛负责产品设计和路演；

### 比赛过程
1，时间：2015.10.24程序员日      地点：深圳湾软件创业大厦3W咖啡厅
2，上午九点三人从深圳四面八方匆匆赶来，么么，附几张美图：
 



3，领证，衣服，一气呵成，断然再来张美图：


4，拿到贴纸，衣服，心情爆好，来张全家福：


5，鉴于写了这么长段，来张作者图，也是可以的吧：



6，题目出来以后，大家都在疯狂的头脑风暴，我们组当然不能落后啊，就假装的讨论起来，然后很有兴致的讨论了共享模式，因为涉及到相关赞助商，所以两个程序猴断然觉得和这次作品如果涉及到无人机相关必火，融入阿里百川必得奖，然后的然后就是针对产品美女一顿语言思想狂轰滥炸，最后的最后产品美女听信谗言，将信将疑的接受了我们的思维模式，哈哈，然后我们就开始愉快的决定了产品的大致方向；

7，午饭很丰盛，来打酱油的我们很快就想睡觉午休了，鉴于此，我们做了相关分工，我和阿蔡分别负责产品前后端，阿陈负责产品文案和产品UI，因为大家都是第一次聚在一起做产品，难免生疏，造成大量的时间浪费，因为在产品没有出相关的原型图之前，本屌丝暂时无事可做，所以就很假装的和阿蔡聊起了使用相关技术等问题；

8，因为阿蔡有了两年工作经验，所以他推荐使用新的技术开发，以达到这次参赛的目的：学习。从他后端开始，重新学习Spring—Boot的开发模式，我这边不在使用原始的okhttp和volley，而是采用较新的Retrofit网络框架，UI部分采用Google新近力推的Material Design和Navigation抽屉模式，以及5.0新加入的RecyclerView和CardView相结合，数据库方面采用郭神的Litepal ORM框架，然后图片的上传和下载以及视频的播放和上传都是采用阿里百川的SDK服务；

9，讨论完技术相关问题，已经接近5点了，然后又是一顿下午茶和晚餐，紧接着就是正式编码阶段了，因为原型图已给出，所以我和阿蔡就开始分别搭框架了，因为技术很菜，所以这段就略过，诸位大神不喜不喷啊，然后就巴拉巴拉。。。。。。

10，写累了，来张各组聆听segment fault CTO讲解题目图（大部分开发者都是Mac，所以追求极客的你，Mac搞起）：


11，写代码，写代码，然后晚上11点半了，产品妹子说好晚，我该回家了，嗯，走吧（好后悔没送其回家，哭）

12，我和阿蔡继续奋战，coding。。。。（风骚的背景图一定要有）

13，凌晨3点，喝了这几罐红牛的我，有一刻，觉得自己是不是要流鼻血挂掉，累的实在不行，就只能和阿蔡结对编程了，图片太劲爆，还是不上传为妙，我司不能宣扬色情嘛。。。

14，然后的然后就是继续写代码了。。。12点提交作品，路演开始！！！

15，产品妹子有点心慌慌，毕竟这样的场合，分到第七组的我们，就这样开始路演了，妹子详细介绍我们的产品的使用场景等，然后我向他们展示了我一天的工作量。。。心好慌，初具规模的App,依然有太多功能需要去实现，好吧我菜了；

16，轮到评委问问题，其中有个胖子评委（额，因为不知道您的大名，就先这么称呼吧，实在抱歉了）说到：你这工作量有点小巴拉巴拉的；然后我解释了相关原因，感觉还不错，紧接着segmentfault的CTO向我们发难了称：我们的项目跑题了。额，好吧，由于时间关系我就没和你争辩了。

17，最后的最后，我们空手而归，心塞。。。附图：




### 总结
###### 准备不足
报名前期没有丝毫准备，针对技术和相关产品规划不明确，在短短32小时内写成一个出色APP很难；
###### 人手不够
由于只配置了三人队伍，且只有2人参与实际编码，且只有我一人完成客户端交互，造成方案和产品不配套，最后导致App只有相关雏形；
###### 缺乏大赛经验
前期准备不足，中途使用新的技术和SDK，结尾产品妹子稍微紧张的路演（妹子i'm sorry），都是导致这次hackaton无功而返的原因；
###### 不够极客
大赛开始，我们团队只是简单的围绕着深圳优势无人机，赞助商阿里百川等做文章，又因为阿里百川的SDK文档不够完善，导致在实际使用中出现很多问题，而其他队伍，跳开了这个局限，做自己喜欢做的，这一切都是因为我和阿蔡不够极客，没有更好的想法，蹲墙角反思中；
###### 学到很多
马马虎虎终于可以自己做App了，瞬间自信了。。。（原谅我的无耻），人外有人，好多优秀开发者，学习劲头更足了，极客精神，创新意识加强了，最重要的一点：看到了几个妹子，瞬间舒心了；




> **注意：**此内容纯属虚构，如有雷同，请告诉我。

## 印象笔记相关

### 笔记本和标签
**马克飞象**增加了`@(笔记本)[标签A|标签B]`语法, 以选择笔记本和添加标签。 **绑定账号后**， 输入`(`自动会出现笔记本列表，请从中选择。

### 笔记标题
**马克飞象**会自动使用文档内出现的第一个标题作为笔记标题。例如本文，就是第一行的 `欢迎使用马克飞象`。

### 快捷编辑
保存在印象笔记中的笔记，右上角会有一个红色的编辑按钮，点击后会回到**马克飞象**中打开并编辑该笔记。
> **注意：**目前用户在印象笔记中单方面做的任何修改，马克飞象是无法自动感知和更新的。所以请务必回到马克飞象编辑。

### 数据同步
**马克飞象**通过**将Markdown原文以隐藏内容保存在笔记中**的精妙设计，实现了对Markdown的存储和再次编辑。既解决了其他产品只是单向导出HTML的单薄，又规避了服务端存储Markdown带来的隐私安全问题。这样，服务端仅作为对印象笔记 API调用和数据转换之用。

> **隐私声明：用户所有的笔记数据，均保存在印象笔记中。马克飞象不存储用户的任何笔记数据。**







## 反馈与建议
- 微博：[@马克飞象]()(http://weibo.com/u/2788354117)，[@GGock]()(http://weibo.com/ggock "开发者个人账号")
- 邮箱：\<hustgock@gmail.com\>

---- -----
感谢阅读这份帮助文档。请点击右上角，绑定印象笔记账号，开启全新的记录与分享体验吧。




[^demo](): 这是一个示例脚注。请查阅 [MultiMarkdown 文档]()(https://github.com/fletcher/MultiMarkdown/wiki/MultiMarkdown-Syntax-Guide#footnotes) 关于脚注的说明。 **限制：** 印象笔记的笔记内容使用 [ENML]()[5]() 格式，基于 HTML，但是不支持某些标签和属性，例如id，这就导致`脚注`和`TOC`无法正常点击。


  [1](): http://maxiang.info/client_zh
  [2](): https://chrome.google.com/webstore/detail/kidnkfckhbdkfgbicccmdggmpgogehop
  [3](): http://adrai.github.io/flowchart.js/
  [4](): http://bramp.github.io/js-sequence-diagrams/
  [5](): https://dev.yinxiang.com/doc/articles/enml.php


