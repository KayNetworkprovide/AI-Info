**RedPajama-INCITE开源产品介绍**

RedPajama-INCITE（以下简称RedPajama）是在5月5日才开源的类ChatGPT产品，主要提供30亿、70亿两种参数，特点是功能强大算力消耗低，可在笔记本、普通显卡运行，适用于中小企业和个人开发者。

30亿参数：主要包括基础款、聊天款和指令调优三个版本。在8000亿token数据集上进行训练，在HELM和Eleuther的测试中比同类的GPT-Neo、Pythia-2.8B更优秀。自动生成的文本丝滑流畅，可以加入拟人化情感。

![Image](https://mmbiz.qpic.cn/mmbiz_png/bVibMfbuuqMl190C9icdaEAAvgaolSXZDo7WA4eQsKRXd4hZTGoDvQDiaMV50hQbcBE5xMsKNqu8SryMjJfaJjnaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

30亿参数开源地址：https://huggingface.co/togethercomputer/RedPajama-INCITE-Base-3B-v1

70亿参数：也是在8000亿token数据集上进行训练，RedPajama希望扩大至1万亿。主要包括基础款、聊天款和指令调优三个版本。其中，指令调优版本的测试结果非常棒，甚至高于LLama-7B版本。

70亿参数开源地址：https://huggingface.co/togethercomputer/RedPajama-INCITE-Chat-7B-v0.1

![Image](https://mmbiz.qpic.cn/mmbiz_png/bVibMfbuuqMl190C9icdaEAAvgaolSXZDoiceTqic9gHtE6wXP8SVYvYdVEcd70KvUj9wCcPInNelgOTaCsKmWb1cA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**RedPajama曾开源1.2万亿token训练数据集**

今年4月17日，RedPajama曾宣布开源1.2万亿token数据集，帮助开发者训练类ChatGPT大语言模型。（开源地址：https://huggingface.co/datasets/togethercomputer/RedPajama-Data-1T）

RedPajama完美复制了LLaMA模型上的1.2万亿训练数据集，按照其论文的数据模式从维基百科、GitHub、普通抓取、C4、图书、ArXiv、Stack Exchange抓取了1.2万亿训练数据，并进行了数据优化、过滤。

其中，普通抓取渠道获取了8780亿数据，并通过多个质量过滤器进行过滤，包括选择类似维基百科页面的线性分类器。C4获取1750亿，基于标准 C4 数据集。GitHub获取590亿，按许可证和质量过滤；图书获取260亿，包括开放书籍的语料库，并根据内容相似性进行去重。

ArXiv获取280亿，去除了样板文件的科学文章。维基百科获取240亿，基于子集数据删除了样板内容。StackExchange获取200亿，基于子集数据删除了样板内容。目前，Together正在打造RedPajama V2，这是一个包含2万亿token的训练数据集。

![Image](https://mmbiz.qpic.cn/mmbiz_png/bVibMfbuuqMl190C9icdaEAAvgaolSXZDocvYficE1MaSpib0U9ticIx6pceE3GjJ5ib2I9h0LG4xblKUha7JtUt0Iaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Together表示**，非常感谢蒙特利尔大学的AAI CERC实验室，斯坦福基础模型研究中心，Ontocord.ai，Meta AI，EleutherAI，OLCF等学术机构和开源社区的鼎力支持。如果没有他们贡献核心训练代码、架构、数据，根本不可能推出RedPajama。

4月17日，RedPajama宣布开源1.2万亿token数据集，帮助开发者训练类ChatGPT大语言模型。这也是目前类ChatGPT领域，全球最大的开源训练数据集。（地址：https://huggingface.co/datasets/togethercomputer/RedPajama-Data-1T）
RedPajama完美复制了LLaMA模型上的1.2万亿训练数据集，由维基百科、GitHub、普通抓取、C4、图书、ArXiv（知名论文网站）、Stack Exchange七部分组成。完整数据集容量约5T，根据数据使用条例已经允许商业化。

4月17日，RedPajama宣布开源1.2万亿token数据集，帮助开发者训练类ChatGPT大语言模型。这也是目前类ChatGPT领域，全球最大的开源训练数据集。（地址：https://huggingface.co/datasets/togethercomputer/RedPajama-Data-1T）

据悉，RedPajama完美复制了LLaMA模型上的1.2万亿训练数据集，由维基百科、GitHub、普通抓取、C4、图书、ArXiv（知名论文网站）、Stack Exchange七部分组成。完整数据集容量约5T，根据数据使用条例已经允许商业化。

最近的类ChatGPT开源项目实在是太卷了，不仅开源了基础模型，就连核心训练数据集也陆续开源，生怕开发者缺衣少粮服务真是周到位啊。但一次性开源如此庞大的数据集还真是少见。

![Image](https://mmbiz.qpic.cn/mmbiz_png/bVibMfbuuqMnibBPibL6T7DfHKK1lkXcuv0TCleNBK7VXVqMTFCaujxtUTJsoM8mpJC1ibS2SQbVCibxqNKxIL9seMQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

ChatGPT的出现加快了生成式AI的商业化落地，并引领了全球新一轮AI技术变革。由于Open AI没有开源ChatGPT，LLaMA、Alpaca、Guanaco、LuoTuo、Vicuna、Koala等一大批优秀的开源项目如雨后春笋般快速增长。

其中，由Meta AI发布的LLaMA是公认最佳的ChatGPT平替产品，其中，**70亿参数模型经过1.2万亿数据训练单个CPU就能跑，比较适合中小型企业和普通开发者**。但LLaMA只能用于学术研究不允许商业化。所以，RedPajama复制了LLaMA1.2万亿训练数据，帮助开发者加速大语言模型训练进程。

其实RedPajama本身就是一个类ChatGPT大语言模型由Together、 Ontocord.ai、ETH DS3Lab、Stanford CRFM和Hazy Research一起合作开发。预计5月份，RedPajama会将大语言模型进行开源。

![Image](https://mmbiz.qpic.cn/mmbiz_png/bVibMfbuuqMnibBPibL6T7DfHKK1lkXcuv0TFY3TGeQ9ZFYqZnUhCo8w2mWHUiaOiaJiaot1PdppX3VQQamYnf1ZV4qQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

本次开源的数据集，RedPajama受LLaMA 70亿参数模型启发，**按照其论文的数据模式从维基百科、GitHub、普通抓取、C4、图书、ArXiv、Stack Exchange抓取了1.2万亿训练数据**，并进行了数据优化、过滤。

其中，普通抓取渠道获取了8780亿数据，并通过多个质量过滤器进行过滤，包括选择类似维基百科页面的线性分类器。C4获取1750亿，基于标准 C4 数据集。GitHub获取590亿，按许可证和质量过滤；图书获取260亿，包括开放书籍的语料库，并根据内容相似性进行去重。

ArXiv获取280亿，去除了样板文件的科学文章。维基百科获取240亿，基于子集数据删除了样板内容。StackExchange获取200亿，基于子集数据删除了样板内容。总体来说，RedPajama完美复制了LLaMA的训练数据集。

![Image](https://mmbiz.qpic.cn/mmbiz_png/bVibMfbuuqMnibBPibL6T7DfHKK1lkXcuv0zWSoPNEIkZQFtW9C694l2MltyEiaCAzS2wGCscqibN8UnficPOeTqZFSg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

RedPajama还开源了所有数据预处理和质量过滤器，使得任何人都可以按照数据准备方法复制 RedPajama-Data-1T。（地址：https://github.com/togethercomputer/RedPajama-Data）

![Image](https://mmbiz.qpic.cn/mmbiz_png/bVibMfbuuqMnibBPibL6T7DfHKK1lkXcuv0A15IaN0A3Klm8Fmjacdqicr3FHpPEbOFY5y0KwRRc5YeVWhHYfCWBiaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

RedPajama表示，正在积极训练类ChatGPT大语言模型，并进行深度优化。根据Alpaca模型的展示，仅需5万条高质量、多样化的指令，就能显着改善对话功能。

目前，RedPajama已经收集了10万条高质量指令，将用于发布RedPyjama模型的指令优化版本。