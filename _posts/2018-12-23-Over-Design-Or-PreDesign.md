---
layout: post
title: "过度设计和过早设计"
description: ""
category: "2018-12"
tags: [设计，工作]
---

最近一个多月工作上基本是以开会讨论为主，讨论前期设计。听起来前期进行这么详细的设计，至少是对业务，需求细节都已经很了解，其实并不完全是这样的。

### 情况介绍
新公司这边亚太地区的业务最近成立了，大规模的招人要做三个业务，产品和技术都在招。因为招人的顺序，研发的招聘相比于产品要快。研发招聘进来了，也不能在空转，要有节奏，可先于产品做一些设计。

老板对于互联网的几个业务和工作的方式很熟悉，是一个互联网老兵。鉴于他以往的经历，以及对要做的三个业务的了解，认为这个三个业务在纵向上肯定会有交集，为了后续的业务的快速发展，组织架构划分了三个组：交易平台组，信息平台组和具体业务的“前端”组。

现在是研发先到位了，根据这三个业务的了解，提前做一些ERD的设计。因为组织架构上的划分，交易平台组和信息平台组从一开始就要定位成能够支持三个业务线，提高业务的开发效率。现在公司中，正在规划的业务中，只有一个业务（暂时称为T）已经正式在线上跑。前提的ERD设计很自然的以已经在线上跑的业务员为参照物，进行一些抽象的设计。

### 过程
在产品的具体业务负责人还没有到岗前，根据已有的业务做了一套抽象设计，然后和具体业务的开发不停地在讨论看看是否可以满足他们现有的业务，以及后续怎么把这个业务迁移过来，包括订单，商品等等。这个过程进行了多次的讨论。

在研发讨论后，一致认为差不多了，加上产品的同事陆陆续续到岗了，就开始跟产品讨论这个设计。（这一步是不是觉得有点哪里不对劲）

在这个讨论的过程中，有一位同事(称为S，是一个类顾问的角色)他是对T 业务很熟悉的产品，也做过对应的研发工作，主要是和他讨论更多的业务流程和细节，另外的产品同事更多的是还在了解业务过程中。讨论中除了讨论业务流程之外，还针对研发设计的ERD 的每一个字段去讨论，非常详细的业务细节。（这一步是不是觉得很奇怪，和产品讨论很具体的技术细节。）这个过程开了很多次讨论会，其中很多的概念都是技术在设计的时候提出的，产品在过程中也没有觉得不妥。

### 高潮
产品内部的同事分工后开始做原型了，做出来后，就开始跟研发一起评审产品的原型。这个过程中，研发更多的反应是，你这个设计跟我们之前确认的ERD 设计不符，很复杂，我们要改设计。过程中不停的发散，各种问题。大家对统一概念的理解，产品和技术不一致，导致冲突很多。产品说，既然这么复杂，我把某个功能砍掉吧，这时技术不乐意了，我们的设计不支持这样的，跟我们之前设计的ERD 又不一样了。产品又说：你们的过程就不对，技术怎么能先于产品设计ERD 呢？我们出了圆形后，你们要我们根据之前的ERD 去修改原型，怎么能从一开始就让产品去适应技术。陷入了僵局。

* 技术是否能基于产品做设计？这个我认为没有绝对的答案。主要还在与双方的协作和沟通。技术团队如果是一个快速响应变化，这本来不是个大问题，毕竟技术是为业务服务的。如果是一个需求变更时都无法沟通，接受的技术团队，提前设计可能是一个灾难。
* 产品在讨论技术细节？产品能对技术细节了解当然是最好的。如果产品一开始不是以产品业务需求，而是以技术实现去讨论方向就偏了，产品就应该以产品的视角去展示业务需求，把具体的技术实现留给研发去决定。而不是一上来：我有个需求，你们只要帮我加一个表/新增一个前端页面路由就可以实现，很简单的。
* 统一领域语言。这个方法真的可以省去了沟通中的很多问题，避免鸡同鸭讲。而这个语言更应该是有产品这边提出，毕竟他们更接近，了解具体的业务。
* 设计一个系统支持三个业务？架构都是演进的。即便要做阿里巴巴一样的业务，一开始，也不应该按照阿里巴巴现在这种架构去设计。我们现在没有一个人做过完整的三个业务线。一开始就做这么一个“支撑中台”的设计，很多边界都不清楚，如何能够设计清楚。业务线的分分合合，也是一个演进的过程，分久必合，合久必分。没必要在一开始就把架构设计这么复杂，一开始就花这么多时间去讨论，设计过度的去设计。
