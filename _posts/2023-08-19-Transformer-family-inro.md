---
layout: post
title: Transformer 系列模型介紹
subtitle: 認識 Transformer, Vision Transformer(ViT) 與 Swin Transformer(Swin T)
categories: 電腦視覺
tags: [電腦視覺, 多媒體, 論文閱讀, Transformer, Vision Transformer, Swin Transformer]
---

## 0. 講解 Video
請先觀看講解 Video 在進行下方的問題討論、paper 內容與詳細資訊

<iframe width="672" height="378" src="https://www.youtube.com/embed/JydFplmsT-0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## 1. Transformer

### 內容

<a href="//www.csie.ntu.edu.tw/~miulab/f111-adl/doc/221006_Attention.pdf">Attention Mechanism pdf file</a>
<embed src="//www.csie.ntu.edu.tw/~miulab/f111-adl/doc/221006_Attention.pdf" type="application/pdf" width="100%" height="400px"/>

<a href="//www.csie.ntu.edu.tw/~miulab/f111-adl/doc/221013_Transformer.pdf">Transformer pdf file</a>
<embed src="//www.csie.ntu.edu.tw/~miulab/f111-adl/doc/221013_Transformer.pdf" type="application/pdf" width="100%" height="400px"/>

### 討論
- Transformer 在一個一個 feed whole transformer output 回 decoder input 時，算不算 recurrent?
    - 過程是 autoregressive ，算是 implicit recurrent，但 transformer 整個架構還是跟 RNN 架構裡的 recurrent 不同
    - ```
        The autoregressive generation process in the Transformer can be
        considered a form of implicit recurrence, although it doesn't 
        involve explicit recurrent connections like traditional recurrent 
        neural networks (RNNs).

        In the context of sequence generation, recurrence refers to the
        dependence on previously generated tokens to generate subsequent 
        tokens. In the Transformer, the autoregressive generation process
        achieves this by using the previously generated tokens as input 
        at each decoding step.

        During generation, the Transformer decoder operates sequentially,
        generating one token at a time. At each decoding step, the model
        attends to all the previously generated tokens through self-attention
        and generates the next token based on the attended information. 
        This process can be seen as an implicit recurrence because the 
        decoder leverages the information from earlier generated tokens 
        to make predictions for the current token.

        While there are no explicit recurrent connections or hidden states
        in the Transformer decoder, the autoregressive generation process
        allows the model to capture dependencies between tokens and generate
        coherent sequences. So, while it's not recurrent in the same sense
        as RNNs, it still exhibits a form of sequential dependence and
        can be considered a form of implicit recurrence.
    ```

### 學習資源
- [台大資訊 深度學習之應用 \| ADL 7.1: Attention Mechanism 注意力機制](https://www.youtube.com/watch?v=YJYcMLq1_f4&list=PLOAQYZPRn2V5yumEV1Wa4JvRiDluf83vn&index=26)
- [Applied Deep Learning 2022](https://www.csie.ntu.edu.tw/~miulab/f111-adl/)
- [Applied Deep Learning 2020](https://www.csie.ntu.edu.tw/~miulab/s108-adl/syllabus.html)
- [Attention is All you Need - NIPS papers](https://proceedings.neurips.cc/paper_files/paper/2017/file/3f5ee243547dee91fbd053c1c4a845aa-Paper.pdf)
- [The Annotated Transformer](http://nlp.seas.harvard.edu/2018/04/03/attention.html)


## 2. Vision transformer

### 內容
![](https://hackmd.io/_uploads/SkbEyG4q3.png)
![](https://hackmd.io/_uploads/By41JBVch.png)
![](https://hackmd.io/_uploads/r1qhkH49h.png)
- ![](https://hackmd.io/_uploads/rk4SUgH9h.png)
    - Hidden size $D$：vector dimension
    - MLP size：每一個 layer 的 neurons 數量
- ![](https://hackmd.io/_uploads/rkuRDxSch.png)
    - ViT-L/16 means the “Large” variant with 16 * 16 input patch size
        - patch size 跟 length 成反比，所以 patch 越大包，需要的 computational resource 就比較少
    - Traning 需要的資料量大，跟好不好訓練是兩回事
        - 雖然 ViT 要資料量大，結果才會好
        - 但在相同的資料下，需要的運算資源 ViT 比 CNN 少
    - | 名稱 | 模型 | pre-train dataset |
        | ---- | ---- | ----------------- |
        | **Ous-JFT** | ViT-H/14 | JFT-300M |
        | **Ous-I21k** | ViT-L/16 | ImageNet-21k  |
        | **BiT-L (Big Transfer)** | ResNet |   JFT-300M  |
        | **Noisy Student** | EfficientNet | semi-supervised learning on ImageNet and JFT- 300M with the labels removed  |


### 討論
- 為什麼需要 patch：圖像的解析度會太大
- 文獻內寫道 "Transformers lack some of the inductive biases inherent to CNNs, such as **translation equivariance** and **locality**, and therefore do **not generalize well** when trained on insufficient amounts of data..." 以下是這兩個專有名詞的介紹。
    1. **Translation Equivariance**: CNNs possess a property known as translation equivariance. ***This means that if an object in an image is shifted, the same feature will be detected regardless of its position in the image***. CNNs achieve this through shared weights and local receptive fields. However, Transformers do not inherently have this property. They process the entire image in parallel using self-attention, and the attention mechanism is not constrained by local receptive fields. As a result, Transformers may not capture translation equivariance as effectively as CNNs.
        - ![](https://hackmd.io/_uploads/BJ2mSHE9h.png)
    2. **Locality** (+bias): CNNs have an inherent bias towards local patterns in images due to their use of **local receptive fields**(The receptive field is the portion of the input that a particular neuron is "looking at" or "receptive to".) and **weight sharing**. This locality bias allows them to capture spatial hierarchies of features in images effectively. On the other hand, Transformers do not have a built-in bias towards local patterns. The self-attention mechanism in Transformers enables capturing global relationships between image patches but does not explicitly enforce locality. This can make it more challenging for Transformers to learn spatial hierarchies from limited amounts of training data.

- 在與 ResNet 比較時，論文內 ResNet 改做 Group Normalization
- Group Normalization：把每一組 batch，再多用 channel 分組，並對每一組做類似 layer normalization（但他是組內的每一個 channel 一起做，layer 是分開做）
    - The main idea behind Group Normalization is to **divide the channels of a feature map into groups and normalize each group separately across the spatial dimensions (H and W)**.
    - the feature map of size (N, C, H, W) is **divided into G groups**.Each group contains **C/G channels**.
    - Scale and shift the normalized values using learnable parameters (gamma and beta) for each group.
    - Advantage：
        - **Reduced Dependency on Batch Statistics**：GN calculates group-level statistics,varying size making it less dependent on batch statistics, which makes it less sensitive to the batch size compared to BN and LN.
        - Performance on **Small Datasets**：better generalization capabilities
        - **Spatial** Independence, Compatibility with **Non-sequential Data**：only uses spatial dimensions (H and W) to compute group-level statistics, making it more suitable for tasks where the spatial layout of the data is critical. This property can be advantageous in **computer vision tasks**, such as object detection or semantic segmentation, where objects can appear at different positions in the image.
    - 需要根據實驗來決定

- what is mean attention distance meaning in self-attention?
    - In a self-attention mechanism, each position in the sequence can attend to all other positions, including itself. The attention mechanism **calculates attention weights that represent the importance of each position relative to the others**.
    - These attention weights determine how much each position contributes to the representation of other positions in the output.
    - 在一層 layer 的情況下，對其他位置的影響關係（位置乘上權重）

### 學習資源
- [[Transformer_CV] Vision Transformer(ViT)重點筆記](https://hackmd.io/@YungHuiHsu/ByDHdxBS5)
- [An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale](https://arxiv.org/pdf/2010.11929.pdf)

## 3. Swin transformer
![](https://hackmd.io/_uploads/Hkyg_qFc2.png)
- 48、C、2C 這些就是一個 patch 的大小，也就是一個 token 的維度，就是一個 vector 的 dimension
    - $C$ 指的就是 channel，但可能不太好直觀的理解
- $H/4 * W/4$ 就是數量
- `W-MSA` 就是一次匡幾個 patch，做 self-attention，windows大小跟上述數據變化都無關
    - windows 大小（一次幾組attention一起做）跟最後結果無關，整張圖 feed 進去多少大小（$H/4 * W/4$ 就是數量）出來就是多少
![](https://hackmd.io/_uploads/BJYumLc52.png)

### Patch Merging
![](https://hackmd.io/_uploads/rkg6t5tc2.png)
- $W\*H\*C$ 這張圖
    - 每一個顏色就是 patch
    - C 就是代表一個 token 的 dimension、一個 patch 的 dimension、一個顏色的 dimension
    - 所以顏色的個數就是 $W\*H$
- $W/2\*H/2\*4C$ 這張圖
    - 個數就變成 $W/2\*H/2$
    - 紅黃藍綠四種顏色 concate 在一起，代表一個 token 的 dimension 變四倍、一個 patch 的 dimension 變四倍、一個顏色的 dimension 變四倍

### W-MSA
就是分塊丟入 self attention
- 下圖左半邊
    - ![](https://hackmd.io/_uploads/r1UIloKc2.png)
- Layer $l$，共四個 window，所以共四組 attention

### SW-MSA
- ![](https://hackmd.io/_uploads/rJH6kjFq2.png)
- 範例
    - ![](https://hackmd.io/_uploads/r1UIloKc2.png)
    - ![](https://hackmd.io/_uploads/B1vHxoK5h.png)
        - 在運算時，不是分9區，而是4區（利用 Masked-MSA 控制），如此一來運算的資源跟 layer $l$ 是一樣的
            - 4一區
            - 35一區
            - 71一區
            - 0268一區
    - ![](https://hackmd.io/_uploads/SyF0yiY5h.png)
    - 最後回復成最初的模樣

### Relative positive bias
- ![](https://hackmd.io/_uploads/rJPRQ8c9h.png)
    - 就是 $B$
    - 加在 attention matrix
    - 大小為 $C^2$
- 先照相對位置編碼，直接相加的話，會造成不同相對位置，所以每個數據需要調整
    - 每一項加上 $M-1$ 保持正數(範例的 M 為)：![](https://hackmd.io/_uploads/S1ZeyUq52.png)
    - row 乘上 $2M-1$，做出相對位置區隔：![](https://hackmd.io/_uploads/BJ_iWU99h.png)
- 行列相加完，對應 learnable 的 ralative position bias table：![](https://hackmd.io/_uploads/SkCtGI5c3.png)

### 詳細結構
- ![](https://hackmd.io/_uploads/ByjN4U55n.png)
    - **concat** : 
        - The first patch merging layer concatenates the features of each group of 2 × 2 neighboring patches, and applies a linear layer on the 4C-dimensional concatenated features.
        - $4$ 就是 patch mergeing 時，一開始有幾個值 concate 在一起
        - stage 1 前面這個是 patch partition，將圖片轉換成 $4*4 = 16$ 的 pitch size，所以就是 16 個 pixal concate 在一起
    - **downsp. rate**：
        - 指的就是 downsampling 的變化
            - 所以一開始 patch patition 完的 size 是 $4*4$，downsampling rate 會變成四倍，resolution 也就會變成 $\frac{1}{4}$倍，因為資訊被縮到$\frac{1}{4}$的範圍內了
        - patch mergeing 完，每個 patch 的長度會減半，downsampling rate 會變成兩倍，所以 resolution 就會每次都再 $*\frac{1}{2}$
        - ViT 一開始 patch size 就設定為 $16*16$，downsampling rate 就都保持相當高、resolution 保持相當的低。如此一來就會不利於做其他的 advance task。
    - **output size**：
        - 原圖是 $224*224$（忽略 Channel 一開始是 =3）
        - 所以每次需要表達原圖的 邊長size 就是 $224/downsp. rate$
- ![](https://hackmd.io/_uploads/HJNMBIc9n.png)
- 英文代表
    - T(Tiny)
    - S(Small)
    - B(Base)
    - L(Large)

### 遇到的問題
- ViT 所需要的資源還是太大
    - 改良版本：windows 內自己做 attention
    - patch merge
- position encoding
    - | 名稱 | 依據 | 學習 | 添加位置 |
        | ---- | ---- | -------- | --- |
        | Transformer | sin/cos 函數 | 不可以學習 | concate 在開頭 |
        | Visual Transformer | 絕對位置 | 可學習 | 加在開頭 |
        | Swin Transformer | 相對位置 | 可學習 | 加在 attention matrix |

### 學習資源
- [Swin Transformer](https://hackmd.io/@travisdirac/SJgEnsqGc)
- [Swin Transformer : Hierarchical Vision Transformer using Shifted Windows](https://arxiv.org/pdf/2103.14030.pdf)
- [Swin-Transformer网络结构详解](https://blog.csdn.net/qq_37541097/article/details/121119988)

