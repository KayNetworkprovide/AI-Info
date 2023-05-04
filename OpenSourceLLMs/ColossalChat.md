#TODO

UC伯克利提出的ColossalChat只需要不到100亿个参数就可以达到中英文双语能力，效果与ChatGPT和GPT-3.5相当。

此外，基于LLaMA模型的ColossalChat，还复刻了完整的RLHF过程，是目前最接近ChatGPT原始技术路线的开源项目。

![Image](https://mmbiz.qpic.cn/mmbiz_png/UicQ7HgWiaUb1A2vP0l9KYMVeoQmTLdAcRGsxs3HH9J294Y3bccibojXI0iaJqUXia9Cr51DvE9GZjTC72VUwafAwFA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![Image](https://mmbiz.qpic.cn/mmbiz_png/UicQ7HgWiaUb1A2vP0l9KYMVeoQmTLdAcR90ubcLk07iaNjZVCkDOqZUPE6KR5FQR5rwyDSLCMwXELRIZNal63Vwg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

### 

**中英双语训练数据集**

ColossalChat发布了一个双语数据集，其中包含大约100,000个中英文问答对。

该数据集是从社交媒体平台上的真实问题场景中收集和清理的，作为种子数据集，使用self-instruct进行扩展，标注成本约为900美元。

与其他self-instruct方法生成的数据集相比，该数据集包含更真实和多样化的种子数据，涵盖更广泛的主题。

  

该数据集适用于微调和RLHF训练。在提供优质数据的情况下，ColossalChat可以实现更好的对话交互，同时也支持中文。

  

![Image](https://mmbiz.qpic.cn/mmbiz_png/UicQ7HgWiaUb1A2vP0l9KYMVeoQmTLdAcRdPpO09klIqfZq378udQIQm1fNPiaicKDHW7q5ibtb9lVXOzOia1pk2AQzQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

 **完整的RLHF管线**

RLHF的算法复刻共有三个阶段：

在RLHF-Stage1中，使用上述双语数据集进行监督指令微调以微调模型。

在RLHF-Stage2中，通过对同一提示的不同输出手动排序来训练奖励模型分配相应的分数，然后监督奖励模型的训练。

在RLHF-Stage3中，使用了强化学习算法，这是训练过程中最复杂的部分。

![Image](https://mmbiz.qpic.cn/mmbiz_png/UicQ7HgWiaUb1A2vP0l9KYMVeoQmTLdAcRcvq2YryPQPOlyCmsRZueBc72WIwg8N2O7bTgXD7MFW6bMXbuKI1fQA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)