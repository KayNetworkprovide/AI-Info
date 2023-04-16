## [Colossal-AI](https://www.bing.com/ck/a?!&&p=ce81cdd691a1f61cJmltdHM9MTY4MTUxNjgwMCZpZ3VpZD0wYWVkYzEzNy1lYzY2LTZhMDEtMTk0Yy1kM2ZmZWQ4ODZiMmImaW5zaWQ9NTE4NA&ptn=3&hsh=3&fclid=0aedc137-ec66-6a01-194c-d3ffed886b2b&psq=clossal+ai&u=a1aHR0cHM6Ly9jb2xvc3NhbGFpLm9yZy8&ntb=1)

有提供数据集！！
他本身是一套独立于pytorch之外的基础框架
在训练SD, GPT上都能独立出来用，效率更高
[hpcaitech/ColossalAI: Making large AI models cheaper, faster and more accessible (github.com)](https://github.com/hpcaitech/ColossalAI)
[ColossalAI/applications/Chat at main · hpcaitech/ColossalAI (github.com)](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat)

## How to use?

### [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#supervised-datasets-collection)Supervised datasets collection

we collected 104K bilingual datasets of Chinese and English, and you can find the datasets in this repo [InstructionWild](https://github.com/XueFuzhao/InstructionWild)

Here is how we collected the data

[![](https://raw.githubusercontent.com/hpcaitech/public_assets/main/applications/chat/data-collect.png)](https://raw.githubusercontent.com/hpcaitech/public_assets/main/applications/chat/data-collect.png)

### [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#rlhf-training-stage1---supervised-instructs-tuning)RLHF Training Stage1 - Supervised instructs tuning

Stage1 is supervised instructs fine-tuning, which uses the datasets mentioned earlier to fine-tune the model.

You can run the `examples/train_sft.sh` to start a supervised instructs fine-tuning.

### [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#rlhf-training-stage2---training-reward-model)RLHF Training Stage2 - Training reward model

Stage2 trains a reward model, which obtains corresponding scores by manually ranking different outputs for the same prompt and supervises the training of the reward model

You can run the `examples/train_rm.sh` to start a reward model training.

### [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#rlhf-training-stage3---training-model-with-reinforcement-learning-by-human-feedback)RLHF Training Stage3 - Training model with reinforcement learning by human feedback

Stage3 uses reinforcement learning algorithm, which is the most complex part of the training process:

[![](https://raw.githubusercontent.com/hpcaitech/public_assets/main/applications/chat/stage-3.jpeg)](https://raw.githubusercontent.com/hpcaitech/public_assets/main/applications/chat/stage-3.jpeg)

You can run the `examples/train_prompts.sh` to start training PPO with human feedback.

For more details, see [`examples/`](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat/examples).

### [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#inference-quantization-and-serving---after-training)Inference Quantization and Serving - After Training

We provide an online inference server and a benchmark. We aim to run inference on single GPU, so quantization is essential when using large models.

We support 8-bit quantization (RTN), 4-bit quantization (GPTQ), and FP16 inference. You can Online inference server scripts can help you deploy your own services.

For more details, see [`inference/`](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat/inference).

## [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#coati7b-examples)Coati7B examples

### [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#generation)Generation

**E-mail****coding****regex****Tex****writing****Table**

### [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#open-qa)Open QA

**Game****Travel****Physical****Chemical****Economy**

You can find more examples in this [repo](https://github.com/XueFuzhao/InstructionWild/blob/main/comparison.md).

### [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#limitation)Limitation

**Limitation for LLaMA-finetuned models****Limitation of dataset**- Lack of summarization ability: No such instructions in finetune datasets. - Lack of multi-turn chat: No such instructions in finetune datasets - Lack of self-recognition: No such instructions in finetune datasets - Lack of Safety: - When the input contains fake facts, the model makes up false facts and explanations. - Cannot abide by OpenAI's policy: When generating prompts from OpenAI API, it always abides by its policy. So no violation case is in the datasets.

## [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#faq)FAQ

**How to save/load checkpoint****How to train with limited resources**

Here are some examples that can allow you to train a 7B model on a single or multiple consumer-grade GPUs.

If you only have a single 24G GPU, you can use the following script. `batch_size` and `lora_rank` are the most important parameters to successfully train the model.

```
torchrun --standalone --nproc_per_node=1 train_sft.py \
    --pretrain "/path/to/LLaMa-7B/" \
    --model 'llama' \
    --strategy naive \
    --log_interval 10 \
    --save_path  /path/to/Coati-7B \
    --dataset /path/to/data.json \
    --batch_size 1 \
    --accimulation_steps 8 \
    --lr 2e-5 \
    --max_datasets_size 512 \
    --max_epochs 1 \
    --lora_rank 16 \
```

`colossalai_gemini` strategy can enable a single 24G GPU to train the whole model without using LoRA if you have sufficient CPU memory. You can use the following script.

```
torchrun --standalone --nproc_per_node=1 train_sft.py \
    --pretrain "/path/to/LLaMa-7B/" \
    --model 'llama' \
    --strategy colossalai_gemini \
    --log_interval 10 \
    --save_path  /path/to/Coati-7B \
    --dataset /path/to/data.json \
    --batch_size 1 \
    --accimulation_steps 8 \
    --lr 2e-5 \
    --max_datasets_size 512 \
    --max_epochs 1 \
```

If you have 4x32 GB GPUs, you can even train the whole 7B model using our `colossalai_zero2_cpu` strategy! The script is given as follows.

```
torchrun --standalone --nproc_per_node=4 train_sft.py \
    --pretrain "/path/to/LLaMa-7B/" \
    --model 'llama' \
    --strategy colossalai_zero2_cpu \
    --log_interval 10 \
    --save_path  /path/to/Coati-7B \
    --dataset /path/to/data.json \
    --batch_size 1 \
    --accimulation_steps 8 \
    --lr 2e-5 \
    --max_datasets_size 512 \
    --max_epochs 1 \
```

## [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#the-plan)The Plan

-    implement PPO fine-tuning
-    implement training reward model
-    support LoRA
-    support inference
-    support llama from [facebook](https://github.com/facebookresearch/llama)
-    implement PPO-ptx fine-tuning
-    integrate with Ray
-    support more RL paradigms, like Implicit Language Q-Learning (ILQL),
-    support chain-of-thought by [langchain](https://github.com/hwchase17/langchain)

### [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#real-time-progress)Real-time progress

You will find our progress in github project broad

[Coati](https://github.com/orgs/hpcaitech/projects/17/views/1)

## [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#invitation-to-open-source-contribution)Invitation to open-source contribution

Referring to the successful attempts of [BLOOM](https://bigscience.huggingface.co/) and [Stable Diffusion](https://en.wikipedia.org/wiki/Stable_Diffusion), any and all developers and partners with computing powers, datasets, models are welcome to join and build the Colossal-AI community, making efforts towards the era of big AI models from the starting point of replicating ChatGPT!

You may contact us or participate in the following ways:

1.  [Leaving a Star ⭐](https://github.com/hpcaitech/ColossalAI/stargazers) to show your like and support. Thanks!
2.  Posting an [issue](https://github.com/hpcaitech/ColossalAI/issues/new/choose), or submitting a PR on GitHub follow the guideline in [Contributing](https://github.com/hpcaitech/ColossalAI/blob/main/CONTRIBUTING.md).
3.  Join the Colossal-AI community on [Slack](https://join.slack.com/t/colossalaiworkspace/shared_invite/zt-z7b26eeb-CBp7jouvu~r0~lcFzX832w), and [WeChat(微信)](https://raw.githubusercontent.com/hpcaitech/public_assets/main/colossalai/img/WeChat.png "qrcode") to share your ideas.
4.  Send your official proposal to email [contact@hpcaitech.com](mailto:contact@hpcaitech.com)

Thanks so much to all of our amazing contributors!

## [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#quick-preview)Quick Preview

[![](https://raw.githubusercontent.com/hpcaitech/public_assets/main/colossalai/img/Chat-demo.png)](https://chat.colossalai.org/)

-   An open-source low cost solution for cloning [ChatGPT](https://openai.com/blog/chatgpt/) with a complete RLHF pipeline. [[demo]](https://chat.colossalai.org/)

[![](https://raw.githubusercontent.com/hpcaitech/public_assets/main/applications/chatgpt/ChatGPT%20scaling.png)](https://raw.githubusercontent.com/hpcaitech/public_assets/main/applications/chatgpt/ChatGPT%20scaling.png)

-   Up to 7.73 times faster for single server training and 1.42 times faster for single-GPU inference

[![](https://raw.githubusercontent.com/hpcaitech/public_assets/main/applications/chatgpt/ChatGPT-1GPU.jpg)](https://raw.githubusercontent.com/hpcaitech/public_assets/main/applications/chatgpt/ChatGPT-1GPU.jpg)

-   Up to 10.3x growth in model capacity on one GPU
-   A mini demo training process requires only 1.62GB of GPU memory (any consumer-grade GPU)

[![](https://raw.githubusercontent.com/hpcaitech/public_assets/main/applications/chatgpt/LoRA%20data.jpg)](https://raw.githubusercontent.com/hpcaitech/public_assets/main/applications/chatgpt/LoRA%20data.jpg)

-   Increase the capacity of the fine-tuning model by up to 3.7 times on a single GPU
-   Keep in a sufficiently high running speed

## [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#authors)Authors

Coati is developed by ColossalAI Team:

-   [Fazzie](https://fazzie-key.cool/about/index.html)
-   [FrankLeeeee](https://github.com/FrankLeeeee)
-   [BlueRum](https://github.com/ht-zhou)
-   [ver217](https://github.com/ver217)
-   [ofey404](https://github.com/ofey404)

The Phd student from [(HPC-AI) Lab](https://ai.comp.nus.edu.sg/) also contributed a lot to this project.

-   [Zangwei Zheng](https://github.com/zhengzangw)
-   [Xue Fuzhao](https://github.com/XueFuzhao)

## [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#citations)Citations

@article{Hu2021LoRALA,
    title   = {LoRA: Low-Rank Adaptation of Large Language Models},
    author  = {Edward J. Hu and Yelong Shen and Phillip Wallis and Zeyuan Allen-Zhu and Yuanzhi Li and Shean Wang and Weizhu Chen},
    journal = {ArXiv},
    year    = {2021},
    volume  = {abs/2106.09685}
}

@article{ouyang2022training,
  title={Training language models to follow instructions with human feedback},
  author={Ouyang, Long and Wu, Jeff and Jiang, Xu and Almeida, Diogo and Wainwright, Carroll L and Mishkin, Pamela and Zhang, Chong and Agarwal, Sandhini and Slama, Katarina and Ray, Alex and others},
  journal={arXiv preprint arXiv:2203.02155},
  year={2022}
}

@article{touvron2023llama,
  title={LLaMA: Open and Efficient Foundation Language Models},
  author={Touvron, Hugo and Lavril, Thibaut and Izacard, Gautier and Martinet, Xavier and Lachaux, Marie-Anne and Lacroix, Timoth{\'e}e and Rozi{\`e}re, Baptiste and Goyal, Naman and Hambro, Eric and Azhar, Faisal and Rodriguez, Aurelien and Joulin, Armand and Grave, Edouard and Lample, Guillaume},
  journal={arXiv preprint arXiv:2302.13971},
  year={2023}
}

@misc{alpaca,
  author = {Rohan Taori and Ishaan Gulrajani and Tianyi Zhang and Yann Dubois and Xuechen Li and Carlos Guestrin and Percy Liang and Tatsunori B. Hashimoto },
  title = {Stanford Alpaca: An Instruction-following LLaMA model},
  year = {2023},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/tatsu-lab/stanford_alpaca}},
}

@misc{instructionwild,
  author = {Fuzhao Xue and Zangwei Zheng and Yang You },
  title = {Instruction in the Wild: A User-based Instruction Dataset},
  year = {2023},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/XueFuzhao/InstructionWild}},
}

## [](https://github.com/hpcaitech/ColossalAI/tree/main/applications/Chat#licenses)Licenses

Coati is licensed under the [Apache 2.0 License](https://github.com/hpcaitech/ColossalAI/blob/main/applications/Chat/LICENSE).

## Footer

[](https://github.com/ "GitHub")© 2023 GitHub, Inc.

### Footer navigation

-   [Terms](https://docs.github.com/site-policy/github-terms/github-terms-of-service)
-   [Privacy](https://docs.github.com/site-policy/privacy-policies/github-privacy-statement)
-   [Security](https://github.com/security)
-   [Status](https://www.githubstatus.com/)
-   [Docs](https://docs.github.com/)
-   [Contact GitHub](https://support.github.com/?tags=dotcom-footer)
-   [Pricing](https://github.com/pricing)
-   [API](https://docs.github.com/)
-   [Training](https://services.github.com/)
-   [Blog](https://github.blog/)
-   [About](https://github.com/about)