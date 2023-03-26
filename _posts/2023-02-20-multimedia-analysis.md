---
layout: post
title: 多媒體內容分析
subtitle: 了解多媒體，就是了解世界的第一步
categories: computer vision
tags: [電腦視覺, 多媒體]
---
## 0. 大綱
![](https://i.imgur.com/ojIBf7U.png)

## 1. Essence of images
- [Chapters 2 and 6 of “Digital Image Processing” by R.C. Gonzalez and R.E. Woods, Prentice Hall, 2nd edition, 2001](https://dl.icdst.org/pdfs/files4/01c56e081202b62bd7d3b4f8545775fb.pdf)

### 1.1 Image sensing
![](https://i.imgur.com/DzfTg4B.png)

- image 的每點數值，會被兩種因素決定
    - illumination 亮度：介於 0~∞
    - reflection 反射度：介於 0~1

### 1.2 Image Sampling and Quantization
圖像雖然實際上是連續的值，但電腦不可能把無窮多個資料點都紀錄，所以我們需要
- <span style="background-color: #f7d6b9; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">影像調整</span>
    - **Sampling**
        - 量變
        - 固定距離取樣
    - **Quantization**
        - 質變
        - 將數值限定在固定範圍之內（顆粒度變大）
- ![](https://i.imgur.com/Y1MMHWW.png)

### 1.3 Digital Image Representation
- Dynamic range
    - ![](https://i.imgur.com/LYuC1Gd.png)
    - 中間的圖片有最大的 Dynamic range
- Image size
    - ![](https://i.imgur.com/wnT6OjU.jpg)
    - 可以發現需要儲存的數量差距很大
- Gray-Level resolution
    - ![](https://i.imgur.com/htjz6UO.jpg)
    
### 1.4 Histogram
一張灰階圖片的 histogram in the range $[0, L-1]$ 是一個**離散**的函數
- <span style="background-color: #e2f8f0; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">$h(r_k) = n_k$ </span>
    - $r_k$ is the $k$th gray level and
    - $n_k$ is the number of pixels in the image having gray level $r_k$
- normalized histogram
  - $$p(r_k) = n_k/n$$
- $n$ 是圖片 pixel 的總數
- ![](https://i.imgur.com/ltlHdZQ.png)

### 1.5 Color fundamentals
- RGB
    - 因為人的視錐細胞組成，才分成藍綠紅三原色
    - ![](https://i.imgur.com/MVLFHTj.png)
    - ![](https://i.imgur.com/wo07iIF.png)![](https://i.imgur.com/q5X6uRE.png)
- CMY
    - 利用印刷透色的原理，就是反過來的 RGB
- CIE
    - 由實驗（人類左右眼比對顏色）出人類辨識的色域
    - 定義 X 為 red、Y 為 green、Z 為 blue
    - 則符合下列兩個條件式
        - $x=\frac{X}{X+Y+Z},$ $y=\frac{Y}{X+Y+Z},$ $z=\frac{Z}{X+Y+Z}$
        - $x+y+z = 1$
    - ![](https://i.imgur.com/OVeNk40.png)
- HSI
    - 前述三原色為基底的色彩模式，適合電腦來顯示
    - <span style="background-color: #ffd7c1; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">特色</span>
        - RGB 並不適合人類去辨識，因為人類對「亮度」比較敏感
        - 有了 HSI 如此一來，我們如果可以把亮度與彩度分開來，圖形在**壓縮**的時候，即可以盡量壓縮彩度、保留色度，做到效果最好的呈現
    - H：hue 色調
    - S：saturation 飽和度
        - H, S 統稱 chromaticity
    - I：brightness intensity 亮度
    - ![](https://i.imgur.com/dDGD4OI.png)
    - <span style="background-color: #e2f8f0; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">可以想成 RGB 的正方體立起來，直軸就是 brightness</span>
        - ![](https://i.imgur.com/xCGGOCW.png)
        - ![](https://i.imgur.com/NxNi0SE.png)
    - 又被稱為 HSV、HSL
    - 轉換公式
        - ![](https://i.imgur.com/bPh8tG2.png)
- Nomuniform quantization
    - 圖像如果要做 quantization，並不是均勻的分佈
    - ![](https://i.imgur.com/kJeNTlT.png)
    - ![](https://i.imgur.com/ga9DJYc.png)

### 1.6 Color histogram
- histogram 當然也可以不用 gray level 來表示
    - ![](https://i.imgur.com/zmRYad1.png)
    - <span style="background-color: #c8d8df; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">Histogram is one of the **most useful feature** to describe images or be the basis for similarity measure</span>
- histogram-based difference
    - $D_j(I_1, I_2) = \Sigma_{i=1}^{B}|H_j^1(i) - H_j^2(i)|$
    - $D(I_1, I_2) = w_1D_1 + w_2D_2 + w_3D_3$
    - $j$ 指不同 level、I 為圖片、w 為 weight

## 2. Essence of videos
- 影片就是影像的巨集，只是有人的影像暫留
    - ![](https://i.imgur.com/7iMJ2Va.png)
- 所以一樣需要 sampling 跟 quantization

### 2.1 Video data representation
- 資料壓縮也跟影像一樣，偷偷把人類比較不會感知到的資料丟掉（所以需要轉換色彩空間將亮度彩度分開，不保持 RGB）
    - （人敏感）亮度老實紀錄
    - （不敏感）彩度少記一點
    - ex: YUV YIQ YCbCr（都有固定的轉換公式）
    - ![](https://i.imgur.com/DW0uJrx.png)
    - ![](https://i.imgur.com/qMtZVvU.png)
- <span style="background-color: #c8d8df; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">Chroma Subsampling</span>
    - 4:4:4、4:2:2(每四個點，記兩個Cb、兩個Cr)、4:1:1、4:2:0(人為決定雖然命名奇怪)
    - ![](https://i.imgur.com/DuqCfmL.png)
    - Y 是代表亮度
- Motion Estimation
    - 不需要每個畫面都去紀錄，只需要紀錄每張彼此的「差距」即可（但還是需要記第一張）
    - 找出兩張圖片內的物件的 Motion Vector
    - ![](https://i.imgur.com/coA8j6f.png)
- IPB frame
    - I(intraframe)：完整的紀錄一整張
    - P(forward predicted frame)：往前看 I
    - B(bidirectionally predicted frame)：前後看最近的 I 或 P
    - Group of Picture(GOP) in MPEG-2
        - ![](https://i.imgur.com/wrwJFV9.png)

### 2.2 Video Feature
- Motion type
    - Camara motion
        - ![](https://i.imgur.com/msfnTLy.png)
    - Object motion
        - ![](https://i.imgur.com/2PlXAo4.png)

## 3. Video syntax analysis
- [J.S. Boreczky, et al., "Comparison of video shot boundary detection techniques" Proc. of SPIE Conference on Storage and Retrieval for Image and Video Databases, vol. 2670, 1996](https://www.csie.ntu.edu.tw/~r96944046/paper/MMAI/Comparison%20of%20video%20shot%20boundary%20detection%20techniques(1996).pdf)

### 3.1 Basic infomation
- shot
    - 畫面內容的急劇變化
    - A basic unit for advanced accessing – browsing, summarization, retrieval
- key frames
    - representative frames of a shot

### 3.2 Detection process
- **outline**
    - ![](https://i.imgur.com/nFee5lV.png)
    - video input
        - temperal frames
    - extract features
        - rgb
        - motion
- **pixel difference**
    - 直接減，最直覺
    - 對 camera motion 最敏感
    - 效果很差
    - 改進：可以不用 pixel 間的差異，改看 windows 內的差異
- **histogram comparision**
    - 可以 gray level 作為 x 軸
    - 對 camera motion 不敏感
    - ![](https://i.imgur.com/7vrsBp3.png)
    - ![](https://i.imgur.com/6J9OEok.jpg)
    - color histogram difference
        - ![](https://i.imgur.com/SE8IOk1.png)
- **likelihood ratio**
    - 切成不同區域(blocks)，看每區的平均亮度與變異數
    - ![](https://i.imgur.com/kprb8lw.png)
    - 只要值超過一個 threshold，就是找到一個 camera break
- **edge change ratio**
    - 先找到圖片的邊緣
    - 關注 Xin Xout 與全部 pixel 的比例，從比例圖就可以判斷切換不同 shot 的種類
    - ![](https://i.imgur.com/NfRzyM6.png)
    - 因為 shot 要做的是找到兩個 frame 的間隔，所以 ECR 是以 xin out 的 max 為代表，找到 ECR 就可以找到間隔了
- **Motion Vector**
    - 看 motion vector 都指向哪一張 frame
    - 用中間的切換當作 shot 改變
    - ![](https://i.imgur.com/f3GaOEv.png)
    - ![](https://i.imgur.com/xoF7aBM.png)（箭頭由新指向舊）
- **Differences in DCT domain**
    - Discrete Cosine Transform (DCT) coefficients
    - 關注圖片的 discrete 高頻位置（人較為不敏感）
    - 計算出相似性
- **Gradual Tranisition Detection**
    - 一般都是注意很大的變化，但還要怎麼注意到比較小的細微變化（溶解 resolved）
    - ![](https://i.imgur.com/2Iskz1K.png)
    - Twin-Comparision
        - 那就訂兩個 threshold
        - 如果連續的畫面都超過小的 threshold，慢慢累積起來也有超過大的 threshod，那就是 resolved 溶解 shot
        - ![](https://i.imgur.com/T5q7rfH.png)
    - Edge change ratio
        - 直接從上面談到的 Edge change ratio 來判斷是否是 gradual transition
        - ![](https://i.imgur.com/6kAgPDZ.png)
        - ![](https://i.imgur.com/BFDk7Wv.png)

### 3.3 Evaluation
- <span style="background-color: #c8d8df; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">數值意義</span>
    - precision：找出來的，正確比例
    - recall、truth positive rate：全部正確，找出的比例
    - false positive rate：全部錯誤，找出的比例

- ![](https://i.imgur.com/FFC0eUi.png)
- ![](https://i.imgur.com/6Rpe5Uq.png)
- PR(precision vs recall)
    - ![](https://i.imgur.com/r2b0jcA.png)
    - 兩者通常是 trade-off
- ROC(Ture positive rate vs False positive rate)
    - ![](https://i.imgur.com/eZnTDcN.png)
- PR vs ROC
    - <span style="background-color: #e2f8f0; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">ROC 的 false positive rate 通常都很小（分母有通常極大的 true positive），所以就算 false positive（false positive rate 的分子） 很大，因為 true positive+false positive（false positive rate 的分母）還是更大，故 ROC 的 false positive rate 保持很小，所以理論上 ROC 比較「樂觀」</span>
- **各演算法的評估**
    - PR Curve for All Data(含 hard cut 跟 graduate transition)
        - ![](https://i.imgur.com/9weSecT.png)
    - PR Curve for All Data – Cut Only
        - ![](https://i.imgur.com/zFqAQzR.png)
    - histogram 最穩定
    - region(likelyhood ratio) 也很棒
    - DCT 最差

## 4. Scene Detection in Movies and TV shows
- [Rasheed, et al. “Scene detection in Hollywood movies and tv shows” Proc. of IEEE Computer Society Conference on Computer Vision and Pattern Recognition, vol. 2, pp. 343-348, 2003](https://www.crcv.ucf.edu/papers/Scene-segCVPR2003.pdf)

### 4.1 System Flowchart
- ![](https://i.imgur.com/R2BjBOG.png)

### 4.2 Feature Detection
- **shot detection**
    - 利用 histogram 以 HSV 當作橫座標軸
        - 16 bin HSV normalized color histogram
        - 8 bins for hue, 4 bins each for saturation and value
    - <span style="background-color: #e2f8f0; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">計算連續 frame，軸的重疊程度(以兩張 frame 的較小的 bin 的和)，如果小於 threshold，就為另一個 shot</span>
        - ![](https://i.imgur.com/99qSP3Q.png)
- **key frame selection**
    - 每一組 shot 都找 key frame（未必一個）
    - 步驟：
        1. 先拿最中間 frame
        2. 其他 frame 看像不像，如果遇到很不像的，就是另外一個 key frame
        - ![](https://i.imgur.com/SmOsarE.png)
- **Motion Contents and Shot Length**
    - shot length
    - shot motion content
        - 利用 MPEG-1 compressed video 預估 affine transformation（變形的狀況：如位移、旋轉）
        - 並且計算與真實圖片之間的誤差（Difference between the original and reprojected flow vectors）
        - ![](https://i.imgur.com/a71wNEI.png)
        - ![](https://i.imgur.com/JN8b2J6.png)

### 4.3 Find Scene Boundaries

#### 4.3.1 Pass One: Color Similarity Analysis
![](https://i.imgur.com/TVzuay4.png)
- 跟前面的每個畫面都做 shot coherence
- 比較方法：
    - 往前每張圖都找![](https://i.imgur.com/EwCVNgg.png)
    - 挑最大的那一個 Best shot coherence ![](https://i.imgur.com/pR6Uqym.png)
    - 把全部的 local min （綠跟藍點，前面沒有人跟他很像）當成潛在的 scene boundary
    - 再根據附近（Window size）的圖片的相似性來慢慢合併（藍點）相同的情境（避免短暫的畫面變化，如 flash back、有人突然進來）
    - ![](https://i.imgur.com/AHCaga9.png)

#### 4.3.2 Pass Two: Scene Dynamics Analysis
- 使用到一開始的 shot motion vector
- ![](https://i.imgur.com/B3QsLFc.png)
- 如果連續兩個 scene dynamic 都很大，表示 motion vector 都很大，我們就認定他為 **`action scene`**，當初就是因為 motion vector 太大才會誤認成不同 scene，所以 merge
![](https://i.imgur.com/gnjHGaQ.png)

### 4.4 Scene Representation
- **shot goodness**
    - 先找出最具代表性的 shot 候選人
    - 在一個 scene 內 shot 互相比較
        - ![](https://i.imgur.com/6NuECZA.png)
        - sence coherence、長度越大越好
        - $SCM_i$ 要改成 $SMC_i$，表第 $i$ shot 的 scene motion content，內容越「安靜」越好
    - 再利用人臉方式，找到最終的代表 shot
        - ![](https://i.imgur.com/SQ4hJYc.png)

## 5. CBIR
- [Y. Rui, T.S. Huang, and S.-F. Chang, “Image retrieval: current techniques, promising directions, and open issues” Journal of Visual Communication and Image Representation, vol. 10, pp. 39-62, 1999.](https://research.lenovo.com/~yongrui/ps/jvcir98.pdf)

### 5.1 Overview
content-based image retrieval
一開始因為做不到「以文字進行搜尋圖片」，但可以手動 label data，所以才需要「以圖片搜尋圖片」，找出已經label的相似的圖片
![](https://i.imgur.com/JYXzkuV.jpg)

### 5.2 Color for CBIR
- **Color Descirptor Metrics**
    - 研究顏色的以對方式
        - ![](https://i.imgur.com/S7WNgGx.jpg)
    - 基礎的相比特性
        - 不會小於零
        - 當兩著相同為零
        - 對稱性：ab相比跟ba相比要一樣
        - 三角不等式：ab距離+bc距離 >= ac距離
- **Minkowski-form metrics**
    - histogram 對應的 bin 相減的絕對值的和
        - ![](https://i.imgur.com/R3WBuXk.png)
    - 只考慮到 same color 的誤差
        - 純藍與純紅與純紫距離都相同...因為都沒有交疊，效果不好
    - ![](https://i.imgur.com/nF9ZOcv.png)
- **histogrma intersection(D1)**
    - 改成兩者的交疊程度（取 min），如果有取 normalize （長度標準變相同）就是 r 取 1
- **histogram enclidean distance(D2)**
    - 兩者相減取平方，就是 r 取 2
    - 可以用線性代數方法表示
- **Binary Set Hamming Distance (D3)**
    - 要兩兩比較，那我們就用 exculsive or 來做快速搜尋
    - ![](https://i.imgur.com/UNNdhoC.png)
    - 減或是 exclusive or 表示有幾個不同的值
- **Histogram Quadratic-Form Metrics（D4）**
    - 不只單純跟一個比距離（兩個 histogram 相同的 bin）
    - ![](https://i.imgur.com/zsDBa9Z.png)
    - 但相比時，weighted 要改變
    - 可以更正上述純藍純紫純紅的相對距離，使差異顯示
        - ![](https://i.imgur.com/c7r58uS.png)
- **Binary Set Quadratic Distance (D5)**
    - D4 加上 binary vector
- **Histogram Mahalanobis distance**
    - 如果每張圖片都有某些地方都一樣（ex 固定有一塊都藍藍的），那並不會助於辨識，所以可以算出共同的變異，也就是「變異數」，並且希望越小越好，所以取倒數
    - ![](https://i.imgur.com/wOEPYzn.png)
    - ![](https://i.imgur.com/orGGVcD.jpg)
- Mean Color Distance (D7)
    - 超簡單，就 rgb 取平均，再算歐式距離
- Color Moment Distance (D8)
    - 超簡單，rgb 取變異數，再算歐式距離
- 結果：
    - sunset
        - ![](https://i.imgur.com/vt8dNYy.png)
        - ![](https://i.imgur.com/m1DNS1p.png)
        - ![](https://i.imgur.com/edfAv2p.jpg)
        - D6 看起來最讚
    - nature
        - ![](https://i.imgur.com/gPIwCIl.png)
        - ![](https://i.imgur.com/zh1BzOO.png)
        - ![](https://i.imgur.com/HUqOly4.jpg)

### 5.3 Texture for CBIR
- 種類
    - Man-made textures
        - Brick walls, handwoven rugs, …
    - Natural textures
        - Water, clouds, sand, grass, lizard skin, …
- Texture Features
    - Structural, Statistical, Spectral(analysis in spatial-frequency 光譜、最成功)
- CNN 就是學 texture 的變化
- textural property
    - 粗糙程度 Coarseness
    - 對比程度 Contrast
    - 方向性 Directionality
    - 直線形 Line-likeness
    - 規則性 Regularity
    - 顆粒度 Roughness
- spectral texture feature
    - ![](https://i.imgur.com/Bx25stY.jpg)
    - 一個函數為**週期性**，那他就可以被 $sin$ 跟 $cos$ 乘上係數 `coefficient` 來組成，稱為 `Fourier series`
    - 一個函數為**非週期性**，那他也可以被 $sin$ 跟 $cos$ 乘上 `weighting function`，稱為 `Fourier transform`
- Fourier transform
    - 每個 almega 都會對應到一組 sin 與 cos
        - ![](https://i.imgur.com/v6Rfn9C.png)
        - 上方為分析
        - 下方為合成
        ```
        ex:(4,5,6) = 4*(1,0,0) + 5*(0,1,0)+ 6*(0,0,1)
        要怎麼得到4?就是 (4,5,6) 跟(1,0,0) 做內積
        等號左到右叫分析，右到左就是合成
        ```
        ```
        fourier tansform 就是做一樣的事情，把 x(t) 跟 e 這個基底做很多內積
        e^(-jwt) 也就是尤拉公式可以轉成 sin cos 相加
        inverce 跟 forward 基底差別（指數差一個負號），就是共軛複數
        ```
        - ex: 1
            - ![](https://i.imgur.com/nkJ4Sut.jpg)此圖經二維離散傅立葉轉換後：（用離散轉換是因為$f(x)$是像素之值的函數，非連續（輸入值為像素的位置））
            - ![](https://i.imgur.com/nYMZP3G.jpg)
            - 可以觀察到：
                - 橫向：圖一頻域的頻率高，較窄，而圖二時域裡可以看到「亮點」的橫軸長度較長
                - 縱向：圖一頻域的頻率地，較寬，而圖二時域裡可以看到「亮點」的橫軸長度較短
        - e.g. 2
            - ![](https://i.imgur.com/SZaNQ72.jpg)
            轉換後：
            - ![](https://i.imgur.com/kYjAbQo.jpg)
            - 觀察紅線方項，原圖中明暗變化多有上下起伏，而頻域圖中則對應到同個方向會出現一道光棘。
                - 這是因外在該方向有很多不規則之細節部分的小變化，越細微的變化越需要高頻率的 $cosine$ 函數去擬合，因此可以看到該方向頻率權重一直延伸到很遠的地方。
    - Two-dimensional Discrete Fourier Transform
        - ![](https://i.imgur.com/kV66g6k.png)
        - ![](https://i.imgur.com/7CVjnxw.png)
        - ![](https://i.imgur.com/wFCkDV8.png)
- Gabor Texture
    - Fourier coefficients 是依據 entire image (Global) → 失去 local information
    - 因此 **`Gabor`** 就是 local spatial frequency analysis
    - Gabor kernels：類似 **`Fourier basis`** 與 **`Gaussian`** 相乘
    - Image $I(x,y)$ convoluted with Gabor filters $h_{mn}$ (totally M x N)
        - ![](https://i.imgur.com/LCkp7Vi.png)
    - ![](https://i.imgur.com/WeTmhRS.png)

## 6. Dimension Reduction
### 6.0 Curse of Dimensionality
- 二維中，一個充滿一個正方形圓形，佔了該正方形的 $78.5\%$ ($\frac{4}{\pi}$)
- 三維中，一顆充滿一正方體的球，只佔了 $52.3\%$ ，約只有一半。
- 越多維，該值就越小，趨近0
- 假設每一維度之分量呈高斯分佈，那在高維度中，所有**點都在距離圓心差不多遠的距離**，因為都很小
    - ![](https://i.imgur.com/hgYMZ7P.png)
    - 此時很難去找出去區域性的 pattern

### 6.1 Principal Component Analysis
利用資料維度降低，得知資訊
![](https://i.imgur.com/7N2gwfF.png)
- 兩種角度：
    - 投影的資料，越分散越好 Maximum Variance Formulation
    - 投影的資料，流失越少越好 Minimum Error Formulation
- ![](https://i.imgur.com/SsVWUOn.jpg)
    - 第一排表前幾大的 eigenvector
    - 第二排左是 eigenvector 的重要性（eigenvalue 順序）
    - 第二排右是 error 大小
    - 第三排是用M個 eigenvector 所重新投影的 3
        - ```
            ex:(4,5,6)向(1,0,0)投影後為(4,0,0)
            (4,5,6)向(1,0,0)、(0,1,0)投影後為(4,5,0)
            ```
        - Eigenfaces 也是用這樣的概念，投影到不同的臉的輪廓

### 6.2 Singular Value Decomposition
- SVD works directly on data, PCA works on covariance matrix of data
- The SVD technique examines the entire set of data and rotates the axis to maximize variance along the first few dimensions
- ![](https://i.imgur.com/CNjdm5q.png)
- ![](https://i.imgur.com/YGmNzzl.png)
- ![](https://i.imgur.com/OvEHGnX.png)
- ![](https://i.imgur.com/DITv7KL.png)
- 最後直接把數值「低」的，表示概念很弱，直接 truncate 掉

### 6.3 Multidimensional Scaling (MDS)
- Goal: represent data points in some lowerdimensional space such that the distances between points in that space correspond to the distance between points in the original space
- 高維的某些點接近，低維度也要接近
- ![](https://i.imgur.com/nOccoDG.png)
- Stress：![](https://i.imgur.com/QTYygId.png)
    - 演算法：
        - 先隨便亂擺
        - 根據 Stress
        - 再調整

### 6.4 Isometric Feature Mapping(Isomap)
- ![](https://i.imgur.com/W3GJVnv.jpg)
    - 左邊是不同角度的同一張人臉
    - 右方是2的不同特徵（上面跟下面有沒有圈圈的特徵）
- 將這些資料以高維表達，可能會 **follow 一些特殊的結構**！而不是直接算距離！
    - 把瑞士捲攤開的距離，應該會更能表達高維的兩點距離（實作可以用附近的點依序找到目標點）![](https://i.imgur.com/NtuLida.jpg)
- Algorithm
    - Step 1: construct neighborhood graph
    - Step 2: compute shortest paths
    - Step 3: construct d-dimensional embedding
        - 如此一來就可以再拿來做 `MDS`

### 6.5 Locally Linear Embedding (LLE)
- Eliminate the need to estimate pairwise distances between widely separated data points. LLE recovers global nonlinear structure from locally linear fits.![](https://i.imgur.com/GshiUUX.jpg)（剛好也是用瑞士捲作為例子）
- 任何一個點，都可以被表成鄰居的線性組合![](https://i.imgur.com/W8NaXFO.png)
- 降維後，彼此的關係也依然相同
    - example：兩維的人臉![](https://i.imgur.com/Qz4XcaJ.png)

## 7. Machine Learning

### 7.1 Overview
- Any computer program that can improve its performance at some task through experience (or training) can be called a learning program
- **Basic Statistical Learning Problems**
    - Regression: 
        - X: input variable, 
        - Y: output variable. 
        - Infer a function f(X) so that given a value of x of the input variable X, y = f(x) is a good predication of the true value y of the output variable Y.
    - Classification: 
        - Assume that a random variable X can belong to one of a finite set of classes C={1,2,…,K}. Given the value x of variable X, infer its class label l=g(x), where $l\in C$
- **Unsupervised vs. Supervised**：沒給正確答案（自己做 clustering）；有給正確答案
- **Generative Models vs. Discriminative Models**：
    - Generative 資料的生成，是因為某些特定的模型（含某些參數）如：GMM、HMM、ChatGPT掌握人類的說話邏輯，這是非常困難...![](https://i.imgur.com/WuIRbOj.png)
    - Discriminative：單純能夠區分，就已經很足夠了，而不去預測背後的生成模型，如：SVM。

### 7.2 Gaussian Mixture Model (GMM)

#### 7.2.1 Introduciton
- 我們可以藉由調整並且組合很多的Gaussians with different means and covariance，那就幾乎可以模擬出所有分佈
- ![](https://i.imgur.com/Bu8N1Vh.png)
- ![](https://i.imgur.com/xstK8qT.jpg)
- $\pi$ 表示權重 weighted，再把每個Gaussian desity相乘後相加
- 觀察![](https://i.imgur.com/YrOFhnC.png)
- 已知貝式定理![](https://i.imgur.com/rVmYtPK.png)
- 現在要試著找處最好的幾組 Gaussian，最能描述目前的機率分佈![](https://i.imgur.com/tMDwDyH.png)
- 求極值就是一次微分後，取=0的情況，可以得出![](https://i.imgur.com/nQG0oAp.png)
- 可知每一個資料點$x_n$相乘$\gamma(z_{nk})$，可以決定最高山峰的位置$\mu_k$，這個$\gamma(z_{nk})$為加權值，就是由每一個小山的佔比。
- 而 $\pi_k$ 也可以用相同的微分=0 取極值方式與 Lagrange multiplier，找到![](https://i.imgur.com/i6cOV5Y.png)

#### 7.2.2 Expectation-Maximization (EM) Algorithm
- 公式推導上：發生雞生蛋、蛋生雞的問題（$\mu_k$ vs $\pi_k$），他們都需要彼此
- 所以先亂預測再調整，Expectation-Maximization 交互使用![](https://i.imgur.com/9YNiXtc.png)
- Gaussian 就可以一直變得越來越好![](https://i.imgur.com/u30r3iL.jpg)![](https://i.imgur.com/eDRAwbx.jpg)



### 7.3 Hidden Markov Model (HMM)

### 7.4 Support Vector Machine (SVM)
