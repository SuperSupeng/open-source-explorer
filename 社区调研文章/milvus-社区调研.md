# Milvus-社区调研
![](https://files.mdnice.com/user/3198/2f2521dd-66c8-4de4-b4e0-d5913b1c12b3.png)
# 写在前面
像任正非任总所说，让听得见炮火的人指挥战斗，写这系列文章也是为了来看看在开源前线的炮火声音是怎么样的，身处开源一线的工作人员都在做什么以及怎么做的。
# 一、产品
## 1.1 产品简介
Milvus 于 2019 年开源，致力于存储、索引和管理由深度神经网络学习与其他机器学习模型生成的海量 Embedding 向量，是 LF AI & Data 基金会毕业项目。

Milvus 向量数据库专为向量查询与检索设计，能够为万亿级向量数据建立索引。与现有的主要用作处理结构化数据的关系型数据库不同，Milvus 在底层设计上就是为了处理由各种非结构化数据转换而来的 Embedding 向量而生。

随着互联网不断发展，电子邮件、论文、物联网传感数据、社交媒体照片、蛋白质分子结构等非结构化数据已经变得越来越普遍。如果想要使用计算机来处理这些数据，需要使用 embedding 技术将这些数据转化为向量。随后，Milvus 会存储这些向量，并为其建立索引。Milvus 能够根据两个向量之间的距离来分析他们的相关性。如果两个向量十分相似，这说明向量所代表的源数据也十分相似。
## 1.2 产品应用场景
Milvus 向量数据库使用场景包括：
- 图片检索系统：以图搜图，从海量数据库中即时返回与上传图片最相似的图片。
- 视频检索系统：将视频关键帧转化为向量并插入 Milvus，便可检索相似视频，或进行实时视频推荐。
- 音频检索系统：快速检索海量演讲、音乐、音效等音频数据，并返回相似音频。
- 分子式检索系统：超高速检索相似化学分子结构、超结构、子结构。
- 推荐系统：根据用户行为及需求推荐相关信息或商品。
- 智能问答机器人：交互式智能问答机器人可自动为用户答疑解惑。
- DNA 序列分类系统：通过对比相似 DNA 序列，仅需几毫秒便可精确对基因进行分类。
- 文本搜索引擎：帮助用户从文本数据库中通过关键词搜索所需信息。
等泛互联网场景。
## 1.3 产品特性
- **云原生**：Milvus 2.0 采取了读写分离、实时离线分离、计算瓶颈/内存瓶颈/IO 瓶颈分离的微服务化设计模式，帮助面对复杂的工作负载选择最佳的资源配比。
- **日志即数据（log as data）**： Milvus 引入消息存储作为系统的骨架，数据的插入修改只通过消息存储交互，执行节点通过订阅消息流（publish/subscribe）来执行数据库的增删改查操作。这一设计的优势在于降低了系统的复杂度，将数据库关键的持久化和闪回等能力都下钻到存储层；另一方面，日志订阅机制提供了极大的灵活性，为系统未来的拓展奠定了基础。
- **批流一体**： Milvus 2.0 实现了 unified Lambda 流式处理架构，增量数据和离线数据一体化处理。相比 Kappa 架构，Milvus 引入对日志流的批量计算将日志快照和构建索引存入对象存储，这大大提高了故障恢复速度和查询效率。为了将无界的流式数据拆分成有界的窗口，Milvus 采用 watermark 机制，通过写入时间（也可以是事件发生时间）将数据切分为多个小的处理单元（message pack），并维护了一条时间轴便于用户基于某个时间点进行查询。
# 二、社区
## 2.1 这是一个什么样的社区
社区整体基于 github discussion，论坛，slack 与微信群，作为一个目前来看小众的开源项目其论坛相对不是非常活跃，而且除了论坛之外还有 github discussion 作为沟通渠道，可能会让人产生一种不知道该在哪里沟通的疑惑。作为一家成立不久的开源创业公司在研发能力与产品成熟度上还不够完备，所以其会较为依赖社区为其贡献代码。
## 2.2 社区规则
社区的一切行为建立在行为准则之上 [Code of Conduct](https://github.com/milvus-io/community/blob/cf1e7c96cfbc727089a5822c3a83b6c116f2f506/CODE_OF_CONDUCT.md)，并可以根据[贡献手册](https://github.com/milvus-io/community/blob/cf1e7c96cfbc727089a5822c3a83b6c116f2f506/CONTRIBUTING.md)进行贡献。但是相对比之下个人觉得 [AppFlowy](https://github.com/AppFlowy-IO/AppFlowy) 这个项目中的 [controbution guide](https://appflowy.gitbook.io/docs/essential-documentation/contribute-to-appflowy/contributing-to-appflowy) 写的会更清楚一些，并分为了 Non-coding Contributions 与 Coding Contributions。
![](https://files.mdnice.com/user/3198/c6c1aeea-ad86-4b60-84ce-cd51a22bd407.png)
而且对“新手如何参与贡献”与“团队决策过程”描述的并不清晰。结合其在[官网](https://milvus.io/community)中关于社区的一些描述可能存在不一致性，后期如果统一描述会更好。
## 2.3 社区关键角色的确认与晋升
在 milvus community 项目中有一个刚被 merge 的 [PR](https://github.com/milvus-io/community/pull/112) 描述了新的社区关键角色定义如下：
### 2.3.1 Contributor
Contributors are individuals who actively make contribution and are willing to participate in the code review of new contributions. They can have issues and PRs assigned to them, participate in discussion through GitHub and slack, and pre-submit tests are automatically run for their PRs. 

**晋升规则：**

- 社区中的积极贡献者，需要完成对项目的至少一个贡献
  - Have made at least one contribution to the project or community. Contribution may include, but is not limited to:
  - Authoring or reviewing PRs on GitHub. At least one PR must be merged.
  - Filing or commenting on issues on GitHub
  - Contributing to community discussions (e.g. meetings, Slack, github discussion)
  - Improve docs
  - Subscribed to the community slack
  - Have read the contributor guide
  - Actively contributing to 1 or more milvus related repos.

**权利与义务：**

- Expected to be responsive to issues and PRs assigned to them
- Expected to follow community rules and values
- They can be assigned to issues and PRs, and people can ask contributors for reviews with a /assign @username.
- Tests can be run against their PRs automatically. 
- Ask for mentorship from Committers/Maintainers
- Join the community meetings and give their advice

*ps: Milvus 项目中的[导师机制](https://github.com/milvus-io/community/pull/104/files)也是不错的尝试。When a new contributor has an issue assigned to his name, he is eligible to apply for a mentor. The Milvus maintainer team will then assign a mentor to the new contributor and the corresponding issue. 导师以及学员信息：[Mentorship Ongoing Pairs](https://wiki.lfaidata.foundation/display/MIL/Mentorship+Ongoing+Pairs)*

### 2.3.2 Committer
Committers are able to review code for quality and correctness on some part of the project. They are knowledgeable about both the codebase and software engineering principles and they should practice the community core values and guidelines as an example.

**晋升规则：**
- contributor for at least 3 months
- Finish at least one major contribution to the community
- Reviewers for at least 5 PRs to the codebase
- Reviewed or merged at least 5 substantial PRs to the codebase
- Knowledgeable about the codebase/doc
- Nominated by at least 1 Maintainer, seconded by at least 3 other committers/maintainers.

**权利与义务：**
- Expected to be responsive to review pull requests
- Expected to assign issues and prs to related expertise
- Expected to be responsive to mentions of others on github and slack
- Expected to join the community meetings and activities in time
- Committer status may be a precondition to accepting large code contributions
- Mentor and guide new contributors
- Committers can do /lgtm on open PRs.
- Committers can vote for the new commiters
- Prioritized technical support from the community 

**退休机制：**

A committer is considered emeritus by their own declaration. An emeritus committer will be list on our hall of fame and may request reinstatement of review access from the maintainers, which will be sufficient to restore him or her to active committer status.

### 2.3.3 Maintainer
Maintainers are able to both review and approve contributions. The maintainers consist group of active committers that moderate the discussion, manage the project release, and proposes new committers or maintainer. Maintainers should serve the community by upholding the community values and guidelines to make Milvus a better community for everyone.

**晋升规则：**
- 经验丰富的活跃 Contributor 和 Committer
- Commiter of the codebase for at least 3 months
- Merged at least 20 PRs to the codebase
- Primary reviewer for at least 10 substantial PRs to the codebase
- Deep understanding of the technical goals and design details of Milvus
- Nominated by at least 1 Approver, and reaches quorum in the exising Maintainer group.

**权利与义务：**
- Make and approve technical design decisions for the project.
- Define milestones and releases.
- Mentor and guide other memberships in the community.
  - Ensure continued health of subproject
- Adequate test coverage to confidently release
  - Tests are passing reliably (i.e. not flaky) and are fixed when they fail
- Ensure a healthy process for discussion and decision making is in place.
- Join the community meeting and discussion in time
- Nominate maintainers and committers and vote for new membership change.
- Prioritized technical support from the community 

**退休机制：**

maintainers has no concept of tenure, but will retire under the following circumstances:
- Actively choose to retire due to personal reasons.
- When a maintainer can no longer participate in community affairs and become inactive in the last 6 months.
- If the maintainer is absent in half of the community meetings and voting in the last 6 months.
- Retirees will become emeritus members and will be list at hall of fame.
# 三、文档
## 3.1 文档构成与托管位置
文档托管在 github 中，并且同样可以在侧边栏点击跳转到对应的 github 文档进行编辑。
![](https://files.mdnice.com/user/3198/a9749101-52d4-4d15-b9c4-777d55f546fb.png)
并未明显区分用户以及开发者文档。
## 3.2 文档更新频率 
文档基本上保持着每日一更的节奏，想要参与开源项目的朋友不妨先从协作文档入手。
# 四、产品规划
## 4.1 产品规划以及 roadmap 公开程度
Milvus 会每三周举行一次技术会议，并将会议链接公开在 [confluence](https://wiki.lfaidata.foundation/pages/viewpage.action?pageId=43287098) 上并将会议一些关键内容进行标注。
![](https://files.mdnice.com/user/3198/e2afda6d-e99c-44eb-bb94-8c445918eec2.png)
而且Milvus 也在 [confluence](https://wiki.lfaidata.foundation/display/MIL/Milvus+2.X+Roadmap+and+Time+schedule) 上公开了 roadmap 对一些 feature 做了状态的标注。
![](https://files.mdnice.com/user/3198/37160af1-e25f-413b-8516-de862ebb9b25.png)
## 4.2 重构文档
一些 [enhancment](https://wiki.lfaidata.foundation/pages/viewpage.action?pageId=43287103) 会形成 proposal。
![](https://files.mdnice.com/user/3198/7f660686-ac16-4513-abc7-30230e75eafe.png)
## 4.3 相关周边分享
Milvus 维护了[博客](https://milvus.io/blog)以及相关的源码解析活动，帮助用户以及开发者了解项目结构以及设计理念。在博客上国内外版本内容不一致，有英文水平又想参与开源项目的同学从博客翻译入手给社区做贡献也是一个思路。
## 4.4 开源协议
项目采用 Apache 2.0 协议
![](https://files.mdnice.com/user/3198/7ed668f2-37c3-44a0-b037-4a7f6e0216e9.png)
# 五、生态
## 5.1 活动种类
- Office hours：是 Milvus 社区的线上交流活动，主要目的是通过线上互动交流的形式，解答用户疑问、介绍和演示 Milvus 新特性和相关技术交流等。
- Paper reading：相关论文的研读与分享
- 源码解析：对 Milvus 相关代码进行分析与讲解
- MeetUp：主题沙龙
- Hacktoberfest：挑战赛
- 相关视频也会在b站上进行同步

*ps：播客前段时间在国内好像突然新增了好多，大大小小的项目以及个体都有了属于自己的播客渠道。*
# 六、社群
## 6.1 社群种类与活跃程度
- 微信群：Milvus 通过机器人将各个用户群打通，这样做有利有弊。利的地方在于解决了单个群活跃度低以及问题重复等问题，弊的地方在于如果群内很活跃那么就会产生大量信息，极端情况会导致无信息。所以要依据自己的项目以及社群类型做合适的运营策略。
- slack：slack 上也有专门的人进行答疑等操作。
## 6.2 主要沟通渠道
slack 主要面向的是海外用户，微信群主要面向的是国内用户，在群内工作人员更多更多是扮演者“客服”的角色，并引导客户将问题提到 issue 上进行讨论等。
# 七、题外话
关于开源社区调研的想法最开始形成于 PingCAP 工作期间，在此也先感谢一下几位前同事的支持。当时是抱着学习国外先进经验的目的，现在看来仍有必要，未来会持续调研国内外大小开源项目，发现优势，总结缺点，希望能帮助大家找到灵感。

在对 Milvus 这个开源项目的调研中，没有详细去探索其 issue 与 PR 的处理流程与响应等，是一个不太完整的部分。社区调研局限于个人认知难免有失偏颇，也欢迎大家批评指正。
