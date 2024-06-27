---
layout: post
title: 多媒體內容分析
subtitle: 了解多媒體，就是了解世界的第一步
categories: 電腦視覺
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
    - $D_j(I_1, I_2) = \Sigma_{i=1}^{B}\|H_j^1(i) - H_j^2(i)\|$
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
    - false positive rate：全部錯誤，沒找出的比例

- ![](https://i.imgur.com/FFC0eUi.png)
- ![](https://i.imgur.com/6Rpe5Uq.png)
- PR(precision vs recall)
    - ![](https://i.imgur.com/r2b0jcA.png)
    - 兩者通常是 trade-off
- ROC Receiver operating characteristic(True positive rate vs False positive rate)
    - ![](https://i.imgur.com/eZnTDcN.png)
- PR vs ROC
    - <span style="background-color: #e2f8f0; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">ROC 的 false positive rate 通常都很小（分母有通常極大的 true negative），所以就算 false positive（false positive rate 的分子） 很大，因為 true negative+false positive（false positive rate 的分母）還是更大，故 ROC 的 false positive rate 保持很小，所以理論上 ROC 比較「樂觀」</span>
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
- **histogram euclidean distance(D2)**
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
- **`Goal`**:represent data points in some lowerdimensional space such that the distances between points in that space correspond to the distance between points in the original space
- 原本高維的某些點距離，在壓縮後的低維度也要相似
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

#### 7.2.1 Introduction
- 我們可以藉由調整並且組合很多的Gaussians with different means and covariance，那就幾乎可以模擬出所有分佈
- ![](https://i.imgur.com/Bu8N1Vh.png)
- ![](https://i.imgur.com/xstK8qT.jpg)
- $\pi$ 表示權重 weighted，再把每個Gaussian density相乘後相加
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
- [Hidden Markov Model Clearly Explained! Part - 5](https://www.youtube.com/watch?v=RWkHJnFj5rY)
- [Hidden Markov Models](https://www.youtube.com/playlist?list=PLix7MmR3doRo3NGNzrq48FItR3TDyuLCo)

#### 7.3.1 elements of HMM
- ![](https://i.imgur.com/MvutSBm.png)
    - $N$: the number of states in the model
    - $M$: the number of distinct observation symbols per state
    - The **state-transition** probability when state from $i$ to $j$
        - $A=\{a_{ij}\}$
    - The **observation** symbol probability distribution when state is in $j$
        - $B=\{b_j(k)\}$
    - The initial state distribution
        - $\pi$
- To describe an **HMM**, we usually use the compact notation $\lambda = (A,B,\pi)$

#### 7.3.2 Probability evaluation
![](https://i.imgur.com/paxaBDd.png)
- 最直覺算法：
    - 總共有 $N^T$ 種 state sequences
    - 如果先固定一種 $q = (q_1q_2...q_T)$
        - ![](https://i.imgur.com/7x6ht1e.png)
        - ![](https://i.imgur.com/fXqUu4w.png)
    - 一種 $q = (q_1q_2...q_T)$ 的機率
        - ![](https://i.imgur.com/ikQv0P3.png)
    - 故總機率為
        - ![](https://i.imgur.com/IfQCGGk.png)
    - 但複雜度 $TN^T$ 太高
        - ![](https://i.imgur.com/ifFSjNZ.png)
        - $2T-1$ 的減一表示乘法第一個數字不用乘
        - $+(N^T-1)$ 表示最後 $N^T$ 種情況都要相加在一起

- **Forward Procedure**
    - $\alpha_t(i)$ 表示已知模型 $\lambda$ 在時間 $t$ 時的 state 為 $S_i$
    - ![](https://i.imgur.com/DFsSuXi.png)
    - inductive 圖解，就是把所有會到達 state $S_j$ 的情況 prob 都加起來
        - ![](https://i.imgur.com/XTQ4D2n.png)
    - 整體圖示
        - ![](https://i.imgur.com/0iFDeIY.png)

- **Backward Procedure**
    - 跟 **Forward** 差不多，只是由反方向算過來
    - ![](https://i.imgur.com/IOmd3Nf.png)
    - inductive 圖解
        - ![](https://i.imgur.com/EIlFYCN.png)

#### 7.3.3 Optimal state sequence
![](https://i.imgur.com/uRZ2Tq3.png)
- 先只關注在單一的 state 找到最好（機率最高）的情況
    - ![](https://i.imgur.com/jeMGmlz.png)
    - 圖示：![](https://i.imgur.com/MZ5F8AS.png)
- 但他們並不是 independent，如果選擇每一個最好出現的情況，那也許 state 本身不會相連
    - ![](https://i.imgur.com/3XKR8j0.png)
- **Viterbi Algorithm**
    - 必須考慮到先前狀況，定義
        - ![](https://i.imgur.com/qeklKVq.png)
    - 每選擇一個 state（$max$函數）都要考慮到前一個 transition prob $a_{ij}$ 跟 observation prob $b_j(O_{t+1})$
        - ![](https://i.imgur.com/VOgfahS.png)
    - 總演算法
        - ![](https://i.imgur.com/JCqEAkf.png)
            - $\psi$ 是為了找出前面的 State

#### 7.3.4 Parameter estimation
![](https://i.imgur.com/cE4J14Q.png)
- 使用 **Baum-Welch algorithm**
    - 但只能找到 locally optimal result
- 先定義新的符號 $\xi$ 表示 state 從 $i$ 到 $j$ 的機率
    - ![](https://i.imgur.com/fLYgRdb.png)
    - 可以看成 $\alpha$ 與 $\beta$ 的組合
        - 圖示：![](https://i.imgur.com/pYR6Q1I.png)
        - 算示：![](https://i.imgur.com/LpLpIXY.png)
- 挑整方法
    - 把 $\gamma$ 和 $\xi$ 做跨時間的總和，就能夠以 state 的角度，去得知平均的經過狀況(expected number)，也就是機率最大的情況
    - ![](https://i.imgur.com/Lk2hJsf.png)
    - 因此就能夠進而調整 $a$、$b$、$\pi$，找到機率最大的 $\bar a$、$\bar b$、$\bar \pi$
    - ![](https://i.imgur.com/9SBnfhC.png)
- 結論：
    - ![](https://i.imgur.com/miB4AcF.png)
    - ![](https://i.imgur.com/Hh7og2d.png)

### 7.4 Support Vector Machine (SVM)

#### 7.4.1 definition
- 用一個超平面，來切割資料點
    - 超平面 `ax + by + c = 0`
    - 如何決定超平面？
        - 傾斜程度：法向量
        - 與原點距離：bias
- 超平面以上為 +1，以下為 -1
- 需要符合的特性：
    - ![](https://i.imgur.com/38jiddC.jpg)![](https://i.imgur.com/zlYBa8w.jpg)
- 最好的效果：
    - 開一條運河，黑點白點都在運河兩邊，運河越寬越好
        - ```
            我們求極值的情況，不喜歡極大，因為最大可以到無限大，數學式很難表達，
            而喜歡極小值，最小就是 0，數學也就很好運算。
            ```
        - ![](https://i.imgur.com/9bXKRht.png)
    - 但運河我們可以容許一些誤差
        - ![](https://i.imgur.com/cz9XXla.jpg)
        - ![](https://i.imgur.com/OBeZhdp.png)
        - $\Gamma$ 是誤差
        - $C$ 是允許誤差的權重
    - 運算的過程會遇到 Dual Problem，也就是一開始是要解上述的式子，但我們可以推導出，另外一個式子，用來跟資料集 dot product 運算，最後相加與加上 bias，可以直接從正負號看出結果，相當簡單！
    - ![](https://i.imgur.com/ns01vpT.png)

#### 7.4.2 Kernel Trick
- 前提：
    - 剛剛的推倒都屬於 **線性結構**
    - 普遍做法為，在低維沒辦法的用線性區分，那我們就利用 Mapping 方法，Mapping 到更高的維度，就可以在高維區分了。![](https://i.imgur.com/0KmFDY9.png)
- 但我們知道，剛剛只需要跟資料集做 mapping 即可以看出結果，但可不可以也不需要 mapping 就做到三維內積的結果，而這就是 kernel trick
    - ![](https://i.imgur.com/YHu3hbZ.png)
    - ![](https://i.imgur.com/0MbPhDE.png)
    - ![](https://i.imgur.com/d6YjDdP.png)

#### 7.4.3 Multiclass SVMs
- 用**不是誰**來分類（one against one）
    - ![](https://i.imgur.com/vYGVn59.png)
- 當資料不多時（以萬筆計算），SVM 就可以有很棒的效果，DL 之前的霸主
- LIBSVM：目前最主流的 library 之一

## 8. Audio Signals

### 8.1 Introduction
- 聲音就是一種波動現象，跟光很像
    - ![](https://i.imgur.com/Yfgmi08.png)
- 所以也需要將波 **數位化**
    - ![](https://i.imgur.com/v6ckkJD.png)

#### 8.1.1 Sampling
- 取樣理論 ***`Nyquist theorem`***
    - For audio, typical sampling rates are from 8 kHz (8,000 samples per second) to 48 kHz.
    - 假設為週期性波，如果 **取樣頻率跟波形頻率一樣**，那永遠只會取樣到同一個點，就會誤以為是一條線，如下圖（波形圖的正負表疏密）
        - ![](https://i.imgur.com/bAvU2JS.png)
    - 如果取樣頻率再高一點，結果也是不對的，不正確模擬的頻率，就稱為 Alias frequency
        - ![](https://i.imgur.com/5UQz8uD.png)
    - **`Nyquist Theorem`**：所以 Nyquist 說最少要 sample 訊號 frequency 的兩倍
    - **`Nyquist frequency`**：如果機器只能 handle 150,000 hz，那波形只能接受 75,000 hz 的波形，75,000 hz 就是 Nyquist frequency，進來機器前會經過濾波器。

#### 8.1.2 Quantization
- 通常 uniform quantization rates 是 8-bit 跟 16-bit
    - 8-bit 有 256 levels
    - 16-bit 有 65536 levels
- **Linear and Nonlinear Quantization**
    - Non-uniform quantization
        - 聲音是因地制宜的，因此 quantization 必須跟周圍環境音比較，才決定
    - **Weber’s Law**：人類的感覺
        - ![](https://i.imgur.com/7UBYLdX.png)
    - Quantization 的方式
        - 當 r(response)要是 uniform，s(stimulation)就不會是 uniform
            - ![](https://i.imgur.com/iHR1Hp8.png)
        - 兩種 uniform 方式
            - ![](https://i.imgur.com/XNFZXZo.png)
            - 但兩種都差不多
            - ![](https://i.imgur.com/KvNuQKq.png)

#### 8.1.3 Audio Filter
- 我們要把一些不重要的資料去除，以免後方也不好處理
- 人能夠發出 50Hz to 10kHz，但機器處理大小要 2 的次方，故取 20Hz 到 20kHz
- 很難從 time domain 看出規則，所以要轉成 frequency domain，也因為人的聽覺就是 based on frequency domain
    - 使用傅立葉轉換
- **Short-Time Fourier Transform (STFT)**
    - 切成很多小段小段
    - 而每一段，短時間內的訊號是不變的
    - 每一段也都會先乘上各自的權重(window function)
    - ![](https://i.imgur.com/XH0tLo7.png)
    - 【補充】不同的 Window funtion：
        - 公式：![](https://i.imgur.com/5wB0JA6.png)
        - 結果：![](https://i.imgur.com/KnIOfT0.png)
    - 最後再作傅立葉轉換
        - ![](https://i.imgur.com/8taTfas.png)
        - 第一部分整條的效果不好
        - 第二三四部分的 over-lapping 就可以觀察出片段跟片段之間的關係

### 8.2 Features
- Short-term frame level vs. long-term clip level
    - frame：10~40 ms，是為基本單位
    - clip 為一系列的 frame
    - ![](https://i.imgur.com/pSEhwno.png)

#### 8.2.1 Frame level Times features
- 用 $N$ to denote the frame length, and $s_n(i)$ to denote the $i_{th}$ sample in the $n_{th}$ audio frame.
- **Volume**：
    - ![](https://i.imgur.com/vNSLPhN.png)
    - 會被錄音設備影響，所以要做 Normalize
- **Zero Crossing Rate**：
    - 過零率，聲音變化時，通過零的比例
    - 過零率越高，頻率應該會越高，所以用聲音的變化狀況推估頻率
    - ![](https://i.imgur.com/PEjRisO.png)
    - 可以用來判斷 unvoiced speech，母音就是 unvoiced speech，聲音可能小小的不明顯、但短時間內有快速變化！
- **Pitch**：
    - 音高
    - 一段聲音波的基本頻率
    - voiced speech(母音)、harmonic(泛音) 通常都有很好的 pitch
    - ![](https://i.imgur.com/0z52iE9.png)
    - ![](https://i.imgur.com/2oRSgKe.png)
        - x軸 $l$ 表示多久取樣一次
        - $R(l)$ 相乘是重複狀況
        - $A(l)$ 相減是相反狀況
        - 目標是找多久重複一次，故 $R(l)$ 我們要看山峰、$A(l)$ 要看波谷
        - 波型的週期越小，表聲音的頻率越高

#### 8.2.2 Frame level Spectral features：
- 光看 time domain 很難得知所有的特性，因此我們可以將其轉至 frequency domain
- 固定時間取樣，作傅立葉轉換
- ![](https://i.imgur.com/p6PQTV4.jpg)
    - 第二張圖的顏色深淺表示 frequency 的強弱
- $S_n(\omega)$
    - 表示特定頻率的能量
- **Frequency centroid, brightness**：
    - 頻率的能量加權平均
    - ![](https://i.imgur.com/Rszx59a.png)
- **Bandwidth**：
    - 標準差
    - ![](https://i.imgur.com/GR25Nyt.png)
- **Subband Energy Ratio**：
    - 不同頻率區段的能量值
    - ![](https://i.imgur.com/gEwEwOC.png)
    - four subbands are 0-630 Hz, 630-1720 Hz, 1720-4400 Hz, and 4400-11025 Hz.
- **Spectral Flux**：
    - 相鄰時間（n、n-1）、相同頻率（k）的能量差值
        - ![](https://i.imgur.com/kOHneUN.png)
    - ![](https://i.imgur.com/NH8AJCL.png)
        - The SF values of speech are higher than those of music. 因為音樂可以連續，如果演講也連續就糊在一起了...
- **Spectral Rolloff**：
    - The $95th$ percentile of the power spectral distribution
    - 看累積到的 $95th$ 能量在哪裡，就可以看出能量是往右還是往左偏斜
- **MFCC (Mel-Frequency Cepstral Coefficients)**
    - 不知道要選什麼 feature 就選他，聲音界的 color histogram
    - 把剛剛的 frequency domain 圖形結果再做一次傅立葉轉換，觀察出各自頻率區段內的變化狀況，稱為 Ceptrum
        - ![](https://i.imgur.com/GfafMul.png)
        - Human pitch perception is most accurate between 100Hz and 1000Hz.
            - Linear in this range
            - Logarithmic above 1000Hz
        - A mel is a unit of pitch defined so that pairs of sounds which are perceptually equidistant in pitch. 當頻率高低到人類感受到一個 pitch 差別。
        - ![](https://i.imgur.com/p2msSxQ.png)
    - ![](https://i.imgur.com/91weYG0.png)
    - 最後再取出幾個最小的值與位置

#### 8.2.3 Clip-Level Features
就是上面提過的內容
- **Volume-based features**:
    - VSTD (volume standard deviation)
    - VDR (volume dynamic range)
    - Percentage of low-energy frames: proportion of frames with rms volume less than 50% of the mean volume within one clip
    - NSR (nonsilence ratio): the ratio of the number of nonsilent frames
- **ZCR-based features**:
    - With a speech signal, low and high ZCR periods interlaced.
    - ZSTD (standard deviation of ZCR)
    - Standard deviation of first order difference
    - Third central moment about the mean
    - Total number of zero crossing exceeding a threshold
    - Difference between the number of zero crossings above and below the mean values
- **Pitch-based features**:
    - PSTD (standard deviation of pitch)
    - SPR (smooth pitch ratio): the percentage of frames in a clip that have similar pitch as the previous frames n Measure the percentage of voiced or music frames within a clip
    - NPR (nonpitch ratio):percentage of frames without pitch.n Measure how many frames are unvoiced speech or noise within a clip

## 9. Musical Genre Classification

### 9.1 Basic features
- 剛剛提過的features，但未必適合拿來作為音樂分類
    - Spectral Centroid
        - ![](https://i.imgur.com/MkOy3UW.png)
    - Spectral Rolloff
        - ![](https://i.imgur.com/4lnfX1K.png)
        - It is used to distinguish voiced from unvoiced speech and music. (unvoiced speech has a high proportion of energy contained in the high-freq. range of the spectrum)
    - Spectral Flux
        - ![](https://i.imgur.com/PKX2gRM.png)
    - MFCC
        - ![](https://i.imgur.com/91weYG0.png)
- **Analysis Window**
    - ![](https://i.imgur.com/RlRKshZ.png)
- 如何利用一連串高維 features vectors，來代表
    - 直接平均
    - 可以利用 GMM 來表達
    - SVM

### 9.2 Rhythmic content features
- 作者音樂家，以樂理的原則去發展 features
- 節拍（beats）的組合為節奏（rhythmics）
    - the regularity of the rhythm, the relation of the main beat to the subbeats, and the relative strength of subbeats to the main beat
- Steps of a common automatic beat detector 
    1. Filterbank decomposition
    2. Envelop extraction
    3. **Periodicity detection** algorithm used to detect the lag at which the signal’s envelope is most similar to itself
    - 其實就跟剛剛的 pitch detection 一樣，只是這個的相隔時間比較長
- Based on discrete wavelet transform (DWT)
- ![](https://i.imgur.com/mCXCzMz.png)
- Octave:
    - 在數理上，每一個八度音程(Octave)正好對應於不 同的振動模式，而兩個八度音程差的音在頻率上 正好差上兩倍。例如：在第0個八度的La(記為A0) 頻率為27.5 Hertz，則第1個八度的La(記為A1)頻 率即為27.5*2=55.0 Hertz。在這每一個八度的音 程中，又可再將其等分為12個頻率差相近的音， 這分別對應於【C Db D Eb E F Gb G Ab A Bb B】， 這樣的等分法就是所謂的十二平均律(Twelve- Tone Scale)。這當中每一個音符所對應的頻率， 都可以藉由數學的方程式準確的算出
    - f1=21/12f2=1.05946f2
- Envelope：
    - 將一種音色波形的大致輪廓描繪出來，就可以表示出該音色在音量變化上的特性，而這個輪廓就稱為Envelope(波封)
    - 一個波封可以用4種參數來描述，分別是Attack(起音)、Decay(衰減)、Sustain(延持)、與Release(釋音)，這四者也就是一般稱的"ADSR"
    - ![](https://i.imgur.com/cK6qq58.png)
    - Envelope extraction：![](https://i.imgur.com/tbPSene.png)
    - Enhanced Autocorrelation：![](https://i.imgur.com/b4BoqBm.png)
        - ![](https://i.imgur.com/dDD7Y0w.png)
        - ![](https://i.imgur.com/ocF2KCZ.png)
        - ![](https://i.imgur.com/dwC0Drg.png)
        - ![](https://i.imgur.com/5WY4iA4.png)
        - ![](https://i.imgur.com/Oc2czpY.png)
        - ![](https://i.imgur.com/XOmCWg0.png)
- Beats histogram
    - ![](https://i.imgur.com/l7pKsVI.png)
    - ![](https://i.imgur.com/9rtxDu9.png)
- Pitch 也幾乎一樣的 features，只是時間長度更短
    - Folded Pitch：把所有相同音階(各種高八度的 Do 版本)，都疊加在一起
- 剛剛都是features，現在看實驗
- Evaluation
    - ![](https://i.imgur.com/V8K5w3K.png)
    - Classification
        - Simple Gaussian classifier
        - Gaussian mixture model
        - K-nearest neighbor classifier 
    - Datasets 
        - 20 musical genres and 3 speech genres 
        - 100 excerpts each with 30 sec
        - Taken from radio, CD, and mp3. The files were stored as 22050 Hz, 16-bit, mono audio files.
    - Result
        - ![](https://i.imgur.com/IxQtPSV.png)
- Window size 的選擇
    - ![](https://i.imgur.com/AfBfrOR.png)
- Feature 大 pk
    - BHF 與 PHF 為本 paper 提出
    - 講半天，如果單挑，傳統的還是比較好 ==
    - 但合一，效果還是會變好
    - ![](https://i.imgur.com/iqEux5Y.png)
    - 人如果只聽3 sec 準確性可以到 70%

## 10. Audio Effects Detection

### 10.1 Sound Effect Modeling
- 為了把聲音裡的笑聲、掌聲等等聲音偵測出來
- **HMM**s can describe the time evolution between states using the transition probability matrix. 
- ![](https://i.imgur.com/BOFi8HE.png)
- 這些 features 就是 observation，再判斷是哪個 state（哪種特效聲）

### 10.2 Log-Likelihood Scores Based Decision Method
- 但不能夠把他們都判斷為特效聲，他有可能是別的聲音
    - 所以利用 Bayesian decision theory 設定 Log-Likelihood Scores
    - ![](https://i.imgur.com/VH3S3js.png)
    - 利用測試片段，分別丟入判斷是否為特效聲、非特效聲的模型
    - 如果兩者相除很大（設定 threshold），代表高機率特效聲，也低機率非特效聲，那就可以判斷非特效聲，代表不屬於當時訓練資料內的類別
- **Cost function**
    - ![](https://i.imgur.com/NJg4qNN.png)
        - $P(C_j)$ 表示他為 $C_j$ 的機率
        - $P(\bar C_j|C_j)$ 為他是 $C_j$ 但被誤判為非 $C_j$ 的機率
- **Bayesian threshold**
    - ![](https://i.imgur.com/TeIWSJV.png)
- **總覽**
    - ![](https://i.imgur.com/H7qdtmq.png)
- **Sound Effect Attention Model**
    - 找出我們會特別注重的地方
    - ![](https://i.imgur.com/1AuPYje.png)
    - 距離波峰越近越集中、能量越高越好
    - ![](https://i.imgur.com/QlIj9Hk.png)
    - 結果波形會有點凹凹凸凸，所以用其 Gaussian、Gamma 波形模擬來看效果
        - ![](https://i.imgur.com/uDReLvn.png)

## 11. Semantic Concept Detection

### 11.0 The Semantic Gap Problem
- ![](https://i.imgur.com/6dZUkEq.jpg)
- 兩份圖片的顏色、構圖也許很像，但語意內容有落差（一壘 vs 二壘安打）

### 11.1 Semantic Indexing of Multimedia Content
- Query by example（如前方的 Content-based image retrival 以圖搜圖） may not suitable for users. Users are familiar with query by keywords.（還是用關鍵字搜圖比較適合使用者）
- semantic labeling as a machine learning problem
    - 辨識出基礎的 label 表示語意概念
    - 再加上這些 label 的組成，構成更複雜的語意概念
- **Framework**
    - ![](https://i.imgur.com/1tomVZS.png)
- 問題 Atomic concepts are modeled using features from a single modality
    - 所以我們還需要融合(fusion)，來描述狀況
    - 而我們使用的是 high-level concepts (late fusion)，不是直接將 feature 串在一起(early fusion)，而是使用 model 的性質融合
- **Learning Visual Concepts**
    - visual scenes 或 objects 使用 GMM
    - spatio-temporal 的 events 或 objects 使用 HMMs
    - 在這份 paper 作者們 compare the performance of GMMs and SVMs for the classification of static scenes and objects
- **Learning Audio Concepts**
    - Audio-based atomic concepts
        - Silence, rocket engine explosion, music, …
    - HMM 被用來 model each audio concept
    - 在一個 shot 裡面，HMMs 產生 N-best list at each audio frame 經過整個 shot，然後就平均 scores
- **Learning Multimodal Concepts**
    - 使用上述模型得到的影像、聽覺的分數，並且做 fusion，作為 high-level features（搭配 Bayesian Network 與 SVM 做分類）
    - Bayesian Network：
        - ![](https://i.imgur.com/H0OE7aj.png)
        - ![](https://i.imgur.com/uaFuYVY.png)
    - SVM：
        - ![](https://i.imgur.com/vCFQWRP.png)
- 結果：
    - 視覺
        - ![](https://i.imgur.com/SfHdIq0.png)
        - ![](https://i.imgur.com/ZOOlTY9.png)
        - SVM 比 GMM 好
    - 聽覺：detecting rocket engine explosion
        - ![](https://i.imgur.com/JHoWiOX.png)
        - HMM 比 GMM 好
    - 融合：
        - 利用 BM（best visual + best audio）模型
            - ![](https://i.imgur.com/26NWYZj.png)
        - 利用 SVM 模型
            - ![](https://i.imgur.com/WXhpTQ6.png)
        - 比較表
            - ![](https://i.imgur.com/nQHk7gB.png)
            - 融合（最後兩個）分數都會比較好！

## 12. Video Event Detection Using Motion Relativity and Visual Relatedness

### 12.1 introduction
- 很多 video event 必須要考慮到移動，單一靜態的畫面不足以判斷
    - ![](https://i.imgur.com/JQjNKa9.jpg)
- features
    - 要表達 Motion of visual words 也就是 What and How
    - ![](https://i.imgur.com/2mYgN0o.jpg)
    - ![](https://i.imgur.com/PoVqcON.png)

### 12.2 Methodology
- **Bag of Visual Words(BoW)**
    - ![](https://i.imgur.com/3S6ayrG.jpg)
- **Motion of visual words (MH-BoW)**
    - 得到 BoW 還不夠，我們還需要追蹤他的 Motion
    - ![](https://i.imgur.com/tFA9e3U.png)
    - 每一個 word 變成四個方向的向量維度 ![](https://i.imgur.com/wo2bWxG.png)
- **Relative motion (RMH-BoW)**
    - 有可能是鏡頭在動，所以需要分析
    - ![](https://i.imgur.com/lqt0OMn.jpg)
    - 表達成兩兩的相對關係，一個點變成一個 matrix 維度
    - ![](https://i.imgur.com/J6SfZXq.png)
- **Expansion with visual relatedness (ERMH-BoW)**
    - feature 會遇到相似狀況
    - ![](https://i.imgur.com/V19nHW0.png)
    - 我們就使用 relatiedness 來處理
    - Texture Ontology
        - ![](https://i.imgur.com/r2uUg8i.png)
    - 學習出 Visual Ontology
        - 找出 feature 的相關性
        - ![](https://i.imgur.com/f7IkuAX.png)
        - ![](https://i.imgur.com/K6dppcW.png)
        - LCA 最接近的祖先
        - IC information content 越接近 root 越小
    - ![](https://i.imgur.com/KKIuKQs.jpg)
- framework![](https://i.imgur.com/SYGuGtU.jpg)
- Event Classification
    - 最後利用 SVM Detection 加上 Earth Mother Distance 判斷是否在一個 clip 裏面
    - ![](https://i.imgur.com/TZqFNlG.png)
    - The EMD distance 不是 one-to-one 的對應
        - ![](https://i.imgur.com/Zm1mkQ6.png)
- Result
    - ![](https://i.imgur.com/tIiecSx.jpg)
    - ![](https://i.imgur.com/ifY5NNh.jpg)
- 視覺處理就此遇到瓶頸，分數衝不上去，所有能有的 feature 幾乎都用了，直到 deep learning 出現，時代就此改變。
 
