
[LLaMA ＋ Text Generation WebUI ~ 大型語言模型網頁前端安裝教學 | Ivon的部落格 (ivonblog.com)](https://ivonblog.com/posts/text-generation-webui/)


[Ivon的部落格](https://ivonblog.com/)

-   [🇺🇸 English website](https://ivonblog.com/en-us/)
-   [首頁](https://ivonblog.com/)
-   [分類](https://ivonblog.com/categories/)
-   [標籤](https://ivonblog.com/tags/)
-   [動態牆](https://ivonblog.com/posts/timeline)
-   [封存](https://ivonblog.com/posts/)
-   [關於Ivon](https://ivonblog.com/about/)
-   [](https://ivonblog.com/posts/text-generation-webui/#)
-   

# LLaMA ＋ Text Generation WebUI ~ 大型語言模型網頁前端安裝教學

 2023.4.9  343

## 目錄

1.  [0. 硬體需求](https://ivonblog.com/posts/text-generation-webui/#0-%E7%A1%AC%E9%AB%94%E9%9C%80%E6%B1%82)
2.  [1. 安裝依賴套件](https://ivonblog.com/posts/text-generation-webui/#1--%E5%AE%89%E8%A3%9D%E4%BE%9D%E8%B3%B4%E5%A5%97%E4%BB%B6)
    1.  [Linux](https://ivonblog.com/posts/text-generation-webui/#linux)
    2.  [Windows](https://ivonblog.com/posts/text-generation-webui/#windows)
3.  [2. 下載大型語言模型](https://ivonblog.com/posts/text-generation-webui/#2-%E4%B8%8B%E8%BC%89%E5%A4%A7%E5%9E%8B%E8%AA%9E%E8%A8%80%E6%A8%A1%E5%9E%8B)
4.  [3. 啟動Text Generation WebUI](https://ivonblog.com/posts/text-generation-webui/#3-%E5%95%9F%E5%8B%95text-generation-webui)
5.  [4. WebUI使用方式](https://ivonblog.com/posts/text-generation-webui/#4-webui%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F)
6.  [5. 擴充功能](https://ivonblog.com/posts/text-generation-webui/#5-%E6%93%B4%E5%85%85%E5%8A%9F%E8%83%BD)
    1.  [角色扮演](https://ivonblog.com/posts/text-generation-webui/#%E8%A7%92%E8%89%B2%E6%89%AE%E6%BC%94)
    2.  [Google翻譯](https://ivonblog.com/posts/text-generation-webui/#google%E7%BF%BB%E8%AD%AF)
    3.  [文字轉語音](https://ivonblog.com/posts/text-generation-webui/#%E6%96%87%E5%AD%97%E8%BD%89%E8%AA%9E%E9%9F%B3)
    4.  [長期記憶](https://ivonblog.com/posts/text-generation-webui/#%E9%95%B7%E6%9C%9F%E8%A8%98%E6%86%B6)
    5.  [分析圖片內容](https://ivonblog.com/posts/text-generation-webui/#%E5%88%86%E6%9E%90%E5%9C%96%E7%89%87%E5%85%A7%E5%AE%B9)
    6.  [用Stable Diffusion繪圖](https://ivonblog.com/posts/text-generation-webui/#%E7%94%A8stable-diffusion%E7%B9%AA%E5%9C%96)
7.  [參考資料](https://ivonblog.com/posts/text-generation-webui/#%E5%8F%83%E8%80%83%E8%B3%87%E6%96%99)

這篇文章Ivon將解說Text Generation WebUI的安裝及使用方法。

![](https://ivonblog.com/posts/text-generation-webui/images/title.webp)

oobabooga開發的「Text Generation WebUI」是支援多種大型語言模型(LLM)的開源軟體，可以在本機與AI對話，等同離線版的小型ChatGPT。

Text Generation WebUI目前支援的大型語言模型有GPT-J-6B、LLaMA、Alpaca、Pygmalion、GTP4All等。還提供自訂角色、對話翻譯的擴充功能。

開發者想仿效ATOMATIC1111，製作大型語言模型版本的[Stable Diffusion WebUI](https://ivonblog.com/posts/windows-stable-diffusion-webui/)。這款軟體也確實能讓大型語言模型指揮Stable Diffusion繪圖。

## [](https://ivonblog.com/posts/text-generation-webui/#0-%E7%A1%AC%E9%AB%94%E9%9C%80%E6%B1%82)[0. 硬體需求](https://ivonblog.com/posts/text-generation-webui/#contents:0-%E7%A1%AC%E9%AB%94%E9%9C%80%E6%B1%82)

硬體需求視使用的大型語言模型而定，有些可以用CPU算，不需要GPU，但速度會很慢。

-   GPU VRAM至少4GB
-   RAM至少16GB
-   30GB以上硬碟空間

除本機安裝外，開發者也有維護[Google Colab筆記本](https://colab.research.google.com/github/oobabooga/AI-Notebooks/blob/main/Colab-TextGen-GPU.ipynb)供線上試玩。

## [](https://ivonblog.com/posts/text-generation-webui/#1--%E5%AE%89%E8%A3%9D%E4%BE%9D%E8%B3%B4%E5%A5%97%E4%BB%B6)[1. 安裝依賴套件](https://ivonblog.com/posts/text-generation-webui/#contents:1--%E5%AE%89%E8%A3%9D%E4%BE%9D%E8%B3%B4%E5%A5%97%E4%BB%B6)

### [](https://ivonblog.com/posts/text-generation-webui/#linux)[Linux](https://ivonblog.com/posts/text-generation-webui/#contents:linux)

1.  Nvidia顯示卡安裝[Nvidia專有驅動以及CUDA](https://ivonblog.com/posts/ubuntu-install-nvidia-drivers/)；AMD安裝[ROCm](https://docs.amd.com/bundle/ROCm-Installation-Guide-v5.1/page/How_to_Install_ROCm.html)。
    
2.  安裝[Anaconda](https://ivonblog.com/posts/linux-anaconda/)，建立Python 3.10.9虛擬環境
    

```
1
2
```

```bash
conda create -n textgen python=3.10.9
conda activate textgen
```

3.  安裝PyTorch

```
1
2
3
4
```

```bash
# Nvidia
pip3 install torch torchvision torchaudio
# AMD
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm5.4.2
```

4.  安裝Text Generation WebUI與依賴套件

```
1
2
3
```

```bash
git clone https://github.com/oobabooga/text-generation-webui
cd text-generation-webui
pip install -r requirements.txt
```

### [](https://ivonblog.com/posts/text-generation-webui/#windows)[Windows](https://ivonblog.com/posts/text-generation-webui/#contents:windows)

1.  Nvidia顯示卡需安裝[Nvidia驅動以及CUDA](https://www.nvidia.com/zh-tw/geforce/geforce-experience/)。
    
2.  安裝[Git for Windows](https://gitforwindows.org/)
    
3.  下載開發者提供的[一鍵安裝器](https://github.com/oobabooga/text-generation-webui/releases/tag/installers)，適用於Windows 10以上系統
    
4.  解壓縮，按二下`install`，依賴套件即會自動安裝。
    

## [](https://ivonblog.com/posts/text-generation-webui/#2-%E4%B8%8B%E8%BC%89%E5%A4%A7%E5%9E%8B%E8%AA%9E%E8%A8%80%E6%A8%A1%E5%9E%8B)[2. 下載大型語言模型](https://ivonblog.com/posts/text-generation-webui/#contents:2-%E4%B8%8B%E8%BC%89%E5%A4%A7%E5%9E%8B%E8%AA%9E%E8%A8%80%E6%A8%A1%E5%9E%8B)

Text Generation WebUI支援多種語言模型，包含[GPT-J-6B](https://huggingface.co/EleutherAI/gpt-j-6b)、[LLaMA](https://github.com/facebookresearch/llama)、[Stanford Alpaca](https://github.com/tatsu-lab/stanford_alpaca)、GPT-4chan等等。不過這些語言模型只支援英文對話，中文的請採用[Chinese-LLaMA-Alpaca](https://github.com/ymcui/Chinese-LLaMA-Alpaca)。

Text Generation WebUI還支援載入LoRA。

我使用[Pygmalion 6B](https://huggingface.co/PygmalionAI/pygmalion-6b)作示範，這是開源AI模型，基於GPT-J-6B訓練而來。

於Text Generation WeBUI的資料夾開啟終端機(Windows請按SHIFT＋右鍵)，使用此指令從Huggingface對應的儲存庫下載模型以及設定檔：

```
1
```

```bash
python download-model.py PygmalionAI/pygmalion-6b
```

下載的模型會放到`models`目錄。

## [](https://ivonblog.com/posts/text-generation-webui/#3-%E5%95%9F%E5%8B%95text-generation-webui)[3. 啟動Text Generation WebUI](https://ivonblog.com/posts/text-generation-webui/#contents:3-%E5%95%9F%E5%8B%95text-generation-webui)

完整引數請參考開發者的[Github](https://github.com/oobabooga/text-generation-webui)。

啟動引數可以設定全用CPU跑(`--cpu`)，或是自動分配任務給CPU和GPU(`--auto-devices`)。語言模型即使全用CPU跑，產生對話的速度還是可以接受的，只是講話會像中風一樣的緩慢。

1.  於Text Generation WeBUI的資料夾開啟終端機，用以下指令啟動WebUI。用`--auto-devices`引數自動分配計算任務給CPU和GPU，`gpu-memory`設定最多分配2GB VRAM（防止OOM，數值視顯卡VRAM而定)，`--model`指定要載入的模型。`--chat`以聊天模式啟動。

```
1
```

```bash
python server.py --auto-devices --gpu-memory 2 --model PygmalionAI_pygmalion-6b --chat
```

2.  啟動後，用瀏覽器開啟WebUI的網址：`http://127.0.0.1:7860`，保持終端機開啟。

要關閉此程式，於終端機按Ctrl＋C終止。

## [](https://ivonblog.com/posts/text-generation-webui/#4-webui%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F)[4. WebUI使用方式](https://ivonblog.com/posts/text-generation-webui/#contents:4-webui%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F)

如何下指令依使用的語言模型而定。

以Pygmalion這個模型來說，可以先從簡單的事實回答開始問起![](https://ivonblog.com/posts/text-generation-webui/images/title.webp)

並嘗試讓AI翻譯文本，或者要求寫個小故事。

跟ChatGPT的用法類似，要求AI執行特定任務前，要先下確切的提示詞(prompt)告訴AI要扮演什麼角色，這樣它會更明白要做什麼。

## [](https://ivonblog.com/posts/text-generation-webui/#5-%E6%93%B4%E5%85%85%E5%8A%9F%E8%83%BD)[5. 擴充功能](https://ivonblog.com/posts/text-generation-webui/#contents:5-%E6%93%B4%E5%85%85%E5%8A%9F%E8%83%BD)

擴充功能可從WebUI的Interface頁面選取，點選後按`Appy and restart Interface`。![](https://ivonblog.com/posts/text-generation-webui/images/Screenshot_20230409_154102.webp)

### [](https://ivonblog.com/posts/text-generation-webui/#%E8%A7%92%E8%89%B2%E6%89%AE%E6%BC%94)[角色扮演](https://ivonblog.com/posts/text-generation-webui/#contents:%E8%A7%92%E8%89%B2%E6%89%AE%E6%BC%94)

Text Generation WebUI支援AI角色扮演。

1.  在`characters`目錄放入`角色名稱.yaml`檔案，自訂AI的身份。![](https://ivonblog.com/posts/text-generation-webui/images/Screenshot_20230409_152406.webp)
    
2.  在WebUI的底部點選Character gallery切換角色。![](https://ivonblog.com/posts/text-generation-webui/images/Screenshot_20230409_102821.webp)
    
3.  這樣就可以玩角色扮演對話，並且對話紀錄會保留下來。![](https://ivonblog.com/posts/text-generation-webui/images/Screenshot_20230409_105458.webp)
    

### [](https://ivonblog.com/posts/text-generation-webui/#google%E7%BF%BB%E8%AD%AF)[Google翻譯](https://ivonblog.com/posts/text-generation-webui/#contents:google%E7%BF%BB%E8%AD%AF)

啟用擴充功能`google_translate`，用Google翻譯雙方的對話內容。

眾所周知Google翻譯不是普通的差。反正都要依賴不自由的網路服務，串ChatGPT API幫你翻譯還比較快。

### [](https://ivonblog.com/posts/text-generation-webui/#%E6%96%87%E5%AD%97%E8%BD%89%E8%AA%9E%E9%9F%B3)[文字轉語音](https://ivonblog.com/posts/text-generation-webui/#contents:%E6%96%87%E5%AD%97%E8%BD%89%E8%AA%9E%E9%9F%B3)

`silero_tts`：配合[Silero](https://github.com/snakers4/silero-models)這個模型，將對話內容文字轉語音並念出。

### [](https://ivonblog.com/posts/text-generation-webui/#%E9%95%B7%E6%9C%9F%E8%A8%98%E6%86%B6)[長期記憶](https://ivonblog.com/posts/text-generation-webui/#contents:%E9%95%B7%E6%9C%9F%E8%A8%98%E6%86%B6)

`long_term_memory`保留AI的對話紀錄。這樣AI擁有記憶，能記得之前談過的內容。

### [](https://ivonblog.com/posts/text-generation-webui/#%E5%88%86%E6%9E%90%E5%9C%96%E7%89%87%E5%85%A7%E5%AE%B9)[分析圖片內容](https://ivonblog.com/posts/text-generation-webui/#contents:%E5%88%86%E6%9E%90%E5%9C%96%E7%89%87%E5%85%A7%E5%AE%B9)

`send_pictures`這個擴充功能讓你上傳圖片給AI，再由AI依據CLIP模型的結果回傳圖片內容的描述文字。

### [](https://ivonblog.com/posts/text-generation-webui/#%E7%94%A8stable-diffusion%E7%B9%AA%E5%9C%96)[用Stable Diffusion繪圖](https://ivonblog.com/posts/text-generation-webui/#contents:%E7%94%A8stable-diffusion%E7%B9%AA%E5%9C%96)

類似Microsoft New Bing，叫AI幫你畫一張圖。

啟用擴充功能`sd_api_pictures`，即可在對話的時候，讓AI生成文字配合[Stable Diffusion WebUI](https://ivonblog.com/posts/windows-stable-diffusion-webui/)繪圖。

注意：Text Generation WebUI預設是跟Stable Diffusion WebUI使用相同的7860通訊埠，需要用`--listen-port`引數將前者變更為其他通訊埠。

1.  在SD WebUI的啟動引數加入`--api`，啟動SD WebUI。
    
2.  啟動Text Generation WebUI時加上`--listen-port 7861`引數，將通訊埠變更為7861/TCP。
    
3.  在Text Generation WebUI的界面最下方，展開sd_api_pictures的界面，填入SD WebUI的IP和通訊埠，按下Enter檢查連線。
    
4.  勾選`Immersive Mode`，再填入繪圖的提示詞。提示詞欄位只要填基本的品質提示詞即可，剩下的提示詞AI會自動從你的對話代入。![](https://ivonblog.com/posts/text-generation-webui/images/Screenshot_20230409_155606.webp)
    
5.  在與AI對話時，填入含有`send|main|message|me`加上`image|pic|picture|photo|snap|snapshot|selfie|meme`的提示詞，即會觸發Stable Diffusion繪圖功能，並回傳圖片。
    

## [](https://ivonblog.com/posts/text-generation-webui/#%E5%8F%83%E8%80%83%E8%B3%87%E6%96%99)[參考資料](https://ivonblog.com/posts/text-generation-webui/#contents:%E5%8F%83%E8%80%83%E8%B3%87%E6%96%99)

[oobabooga/text-generation-webui Wiki - GitHub](https://github.com/oobabooga/text-generation-webui/wiki)

感謝您的閱讀。歡迎分享Ivon的部落格(ivonblog.com)的文章，引用或轉載請註明文章網址，並遵守[創用CC-姓名標示-非商業性-禁止改作 4.0 國際](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.zh_TW)授權條款。

[Large Language Model](https://ivonblog.com/tags/large-language-model/)

## 相關文章：

-   [LLaMA、Alpaca、Vicuna、GPT4All，開源大型語言模型與相關軟體介紹](https://ivonblog.com/posts/meta-llama-introduction/)
-   [Android手機Termux跑Alpaca (LLaMA) 大型語言模型](https://ivonblog.com/posts/alpaca-cpp-termux-android/)

如果本網站文章對您有幫助，歡迎贊助我。

[](https://ivonblog.com/posts/text-generation-webui/#)

© 2021–2023  Ivon Huang

本站內容授權為【[姓名標示-非商業性-禁止改作 4.0 國際](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.zh_TW)】。轉載必須註明來源為[本站](https://ivonblog.com/)。

Website visitors  160314 | Page views  281886