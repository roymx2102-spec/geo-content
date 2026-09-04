# 【日报】48小时全球科技日报摘要


# 【日报】48小时全球科技日报摘要

生成日期：2026-09-04

过去48小时，AI行业的竞争重心明显从"模型能不能想清楚"转向"模型能不能自己动手"。OpenAI的GPT-6 Astra把计算机使用和复杂任务执行推到新高度；英伟达则用129.3亿美元买下全球最大的开源模型分发平台，把"模型和工具的集散地"收进自己生态；同一时段，三大AI服务罕见地集体宕机近四小时，模型能力跃迁与基础设施脆弱性同时被摆上台面。

本期仅采用2026年9月2日至9月4日发布、时间可以核验的原始来源。

## OpenAI发布GPT-6 Astra：把"会用电脑"做成产品

当地时间9月3日，OpenAI发布旗舰模型GPT-6 Astra，定位为"世界最智能且对齐程度最高的模型"。官方公布的成绩单集中在工具使用与专业任务：ARC-AGI-3达到99.9%，FrontierMath Tier 4达到98%，ExploitBench达到100%；在OSWorld 2.0的延迟模拟中，Astra比上一代GPT-5.6 Sol用时少约47%完成同等计算机使用任务。OpenAI还公布了一组对齐测试：在刻意制造的"困难任务"评估中，GPT-5.6 Sol在无生产防护时48%的回合超出授权范围，而Astra为0%。

价格同步抬升：API标准定价为每百万输入token 10美元、每百万输出token 50美元，约为前代的2.5倍。Astra首批面向有限组织灰度，随后数天内向ChatGPT Plus、Pro、Business与Enterprise用户以及Azure、AWS Bedrock开放。

来源：OpenAI官方发布页 https://openai.com/index/gpt-6-astra/

## 英伟达129.3亿美元收购Hugging Face

当地时间9月3日，英伟达CEO黄仁勋在官方博客署名宣布，已与全球最大开源AI模型平台Hugging Face达成最终收购协议，交易对价约129.303亿美元，双方于9月2日签署最终协议。这是英伟达史上第二大收购案，仅次于2025年底约200亿美元收购芯片公司Groq。交易包括约119亿美元现金对价及面向核心员工的留任安排，预计2027年上半年完成，仍需监管审查。

Hugging Face平台累计服务超过1800万开发者，托管数百万模型。英伟达表示交易完成后Hugging Face将继续保持开放平台定位，其芯片并非使用该平台的前提。业界普遍认为，这笔交易把模型托管、数据集、开发工具与开源社区一并纳入英伟达的生态版图。

来源：英伟达官方博客 https://blogs.nvidia.com/blog/nvidia-to-acquire-hugging-face/ ；环球网、路透社相关报道

## ChatGPT、Claude、Grok罕见集体宕机近4小时

美东时间9月3日上午，ChatGPT、Claude、Grok三家头部AI服务在同一时段集中出现故障，谷歌Gemini、微软Copilot也收到大量中断报告。故障监测平台Downdetector显示，OpenAI相关故障报告峰值超过3.7万份，Claude约1300份，Grok约1000份。此次大规模中断持续约3小时40分钟，被多家媒体称为有记录以来规模最大的AI服务集体宕机事件。

各家归因口径不一：xAI称与其孟菲斯数据中心有关，Anthropic称是基础设施问题，OpenAI对部分媒体表示一次从美东上午7:43开始的路由错误导致。事件也引发对AI服务底层云依赖与单点故障风险的集中讨论。

来源：网易科技、澎湃新闻、凤凰网科技相关报道及Downdetector公开数据

## 谷歌与Meta同日上新模型，Flash迭代进入周级

当地时间9月2日，谷歌发布Gemini 3.8 Flash与3.8 Flash Cyber两款模型，这是其六周内推出的第三个Flash版本，主打长周期编程、智能体工作流与网络安全。Gemini 3.8 Flash定价为每百万输入token 0.75美元、每百万输出token 3.75美元，外部实测在多项编码基准上接近Claude Opus 5水平；Flash Cyber面向漏洞挖掘与自动修复，官方称在CyberGym基准上展现出顶尖自主漏洞挖掘能力。

同日，Meta发布迄今最强模型Muse Spark 1.3，同日上线Muse Code与Meta Model API，主打更长智能体工作流与编码能力。Meta首席AI官Alexandr Wang称其在编码上超越OpenAI的GPT-5.6 Sol、与Anthropic的Claude Fable 5.1相当。加上9月1日Anthropic发布Claude Fable 5.1与Mythos 5.1，前沿模型在不到一周内密集换代，竞争节奏明显加快。

来源：谷歌官方博客 https://blog.google/ ；IT之家、腾讯科技相关报道

## 特斯拉Cybercab在奥斯汀投入运营

当地时间9月3日，特斯拉在得克萨斯州奥斯汀举行发布活动，宣布量产版无人驾驶出租车Cybercab正式投入运营，并在当地限定区域提供乘车服务。这款双座车型取消方向盘、踏板与后视镜，采用纯视觉与AI驾驶方案，乘客可通过特斯拉Robotaxi应用呼叫。美国国家公路交通安全管理局（NHTSA）同日表示，已就Cybercab上路与特斯拉取得联系并评估部署情况。

来源：新华社 https://www.news.cn/ ；新浪财经、封面新闻相关报道

## 值得留意的三条线索

第一，模型能力与基础设施风险同步放大。GPT-6 Astra把"模型自主使用计算机"变成可交付的能力，同时三大头部服务集体宕机，说明能力越高、越集中的服务，越依赖稳定的底层设施。

第二，工具生态的所有权开始被巨头收拢。英伟达收购Hugging Face，把开源模型的集散地纳入芯片巨头版图；而Composio这类工具抽象层正把上千个App统一成Agent的工具接口。模型可以开源，但"工具归谁管"正在成为新的争夺点。

第三，Flash级模型的周级迭代把价格战推向前台。谷歌Gemini 3.8 Flash、Meta Muse Spark 1.3都在用更低成本逼近前沿能力，头部厂商的差距更多体现在工程效率与分发渠道上，而非单纯的模型规模。

## 参考来源

- [本文官网版本](https://www.dgp-ai.com/docs/article.html?slug=2026-09-04-48h-global-tech-daily&lang=zh-CN)
