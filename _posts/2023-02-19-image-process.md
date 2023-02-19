---
layout: post
title: 電腦視覺與影像處理
subtitle: Each post also has a subtitle
categories: markdown
tags: [example, markdown]
---

## 延伸閱讀
- [Principal Component Analysis, PCA](https://chih-sheng-huang821.medium.com/%E6%A9%9F%E5%99%A8-%E7%B5%B1%E8%A8%88%E5%AD%B8%E7%BF%92-%E4%B8%BB%E6%88%90%E5%88%86%E5%88%86%E6%9E%90-principle-component-analysis-pca-58229cd26e71)
- [Multivariate Distances: Mahalanobis vs. Euclidean](https://waterprogramming.wordpress.com/2018/07/23/multivariate-distances-mahalanobis-vs-euclidean/)
- [Understanding binary cross-entropy / log loss: a visual explanation](https://towardsdatascience.com/understanding-binary-cross-entropy-log-loss-a-visual-explanation-a3ac6025181a)、[中文版](https://zhuanlan.zhihu.com/p/89391305)
## Ch5. Processing and Convolution
### 1. Nosie Types
![](https://i.imgur.com/1Xd03O6.png)
### 2. Low and High Pass Filter
![](https://i.imgur.com/ZNewUnx.png)
### 3. Low : Goal - Denoise
![](https://i.imgur.com/2wpsR7X.png)
#### 3.1 Low : average blur
- 對 Window 內的所有 pixel 值平均，當作中心值大小
#### 3.2 Low : median Blur
- 將 Mask 遮到的數據先做由小到大的排序，接著直接對此數列**取 Median 取代中間數據**
    - ![](https://i.imgur.com/i9i7tgN.png)
- 經常用於去除圖像或者其他信號中的雜訊，中值濾波器在脈衝雜訊（impulse）出現時，特別有用，因為脈衝雜訊看起來像是疊加在影像上的白點和黑點，所以又稱為胡椒鹽式雜訊（salt-andpepper noise）
    - ![](https://i.imgur.com/E1kov4g.png)
#### 3.3 Low : Gaussian Blur
- 前提：Normal distribution（Gaussian distribution）
    - ![](https://i.imgur.com/6iBtc0d.png)[name=][正態分佈的前世今生](https://cosx.org/2013/01/story-of-normal-distribution-1/)
    - ![](https://i.imgur.com/sSGcBnQ.png)
    - 會有這樣結果的原因為 Central Limit Theorem，不管從哪種 distribution (eg. uniform, exponential) 的母體中隨機取樣做平均，當樣本趨向無窮時，都會符合 normal distribution
    - ![](https://i.imgur.com/7ULwLTv.png)
- [Gaussian Filter](https://ithelp.ithome.com.tw/articles/10273833)
    - [定義](https://medium.com/@bob800530/python-gaussian-filter-%E6%A6%82%E5%BF%B5%E8%88%87%E5%AF%A6%E4%BD%9C-676aac52ea17)（在二維時，可以想像成兩個 gaussian distribution 相乘）：
        :::info
        ${\displaystyle G(x,y)={\frac {1}{2\pi \sigma ^{2}}}e^{-(x^{2}+y^{2})/(2\sigma ^{2})}}$
        :::
    - 計算平均值的時候，我們只需要將中心點作為原點，其他點按照其在高斯分佈曲線上的位置分配權重，就可以得到他的加權平均值
    - ![](https://i.imgur.com/bZE7CrE.png)
    - 其中 $\sigma$ [沒有辦法利用公式確定是多少，必須根據圖片因素](https://stackoverflow.com/a/3149515/18560102)
:::warning
:smiling_imp: 高斯濾波在低通濾波算法中有不錯的表現，但是其卻有另外一個問題，那就是**只考慮了像素間的空間位置上的關係**，因此濾波的結果會丟失邊緣的信息。
這裡的邊緣主要是指圖像中主要的不同顏色區域（比如藍色的天空，黑色的頭髮等），而 Bilateral 就是在 Gaussian blur 中加入了另外的一個權重分部來解決這一問題。
:::
#### 3.4 Low : Bilateral Filter
- [定義](https://en.wikipedia.org/wiki/Bilateral_filter)
    :::info
    ${\displaystyle I^{\text{filtered}}(x)={\frac {1}{W_{p}}}\sum _{x_{i}\in \Omega }I(x_{i})f_{r}(\|I(x_{i})-I(x)\|)g_{s}(\|x_{i}-x\|),}$

    而 normalization term, ${\displaystyle {W_{p}}}$ , 被定義為

    ${\displaystyle W_{p}=\sum _{x_{i}\in \Omega }{f_{r}(\|I(x_{i})-I(x)\|)g_{s}(\|x_{i}-x\|)}}$
    :::
    - $I^\text{filtered}$  表示過濾完的圖片
    - ${\displaystyle I}$ 原圖
    - ${\displaystyle x}$ 原圖座標
    - $\Omega$  以${\displaystyle x}$為中心的 window
    - $f_r$ 加權為像素色差的高斯濾波器
    - $g_s$ 加權為距離的高斯濾波器
- 為了直觀地了解高斯濾波與雙邊濾波的區別，我們可以從下列圖示中看出依據。假設目標源影像為下述左右區域分明的帶有噪聲的影像（由程式自動生成），藍色框的中心即為目標像素所在的位置，那麼當前像素處所對應的高斯權重與雙邊權重因子3D可視化後的形狀如後邊兩圖所示：
    - ![](https://i.imgur.com/986p5Zw.png)
    - 左圖為原始的噪聲影像；中間為高斯採樣的權重；右圖為Bilateral採樣的權重
    - 從圖中可以看出 Bilateral 加入了相似程度分部以後**可以將源影像左側那些跟當前像素差值過大的點給過濾掉，這樣就很好地保持了邊緣**
### 4. High : Feature Extraction - Edge Detection
![](https://i.imgur.com/gx3DRn9.png)
![](https://i.imgur.com/R8k4E2J.png)
#### 4.1 High : Sobel Filter
- 只用**圖像的梯度**作為判斷依據，且對於不同方向性的邊界是用分開的面罩(Mask)來做偵測，當梯度變化超過一個閥值，即判斷為邊界。
- [定義](https://zh.m.wikipedia.org/zh-tw/%E7%B4%A2%E8%B2%9D%E7%88%BE%E7%AE%97%E5%AD%90)：
    :::info
    ${{G_{x}} ={\begin{bmatrix}+1&0&-1\\+2&0&-2\\+1&0&-1\end{bmatrix}}* {A} \quad {\mbox{and}}\quad {G_{y}} ={\begin{bmatrix}+1&+2&+1\\0&0&0\\-1&-2&-1\end{bmatrix}}* {A} }$

    圖像的每一個像素的橫向及縱向梯度近似值可用以下的公式結合，來計算梯度的大小

    ${ {G} ={\sqrt {G_{x} ^{2}+G_{y} ^{2}}}}$
    
    用以下公式計算梯度方向
    
    ${{\Theta } =\operatorname {arctan} \left({{G_{y}} \over {G_{x}} }\right)}$

    :::
- 圖示：![](https://i.imgur.com/cOPgP8j.png)
#### 4.2 High : Scharr Filter
- 就是將 Sober 的矩陣參數改變
- 定義：
    :::info
    ${{G_{x}} ={\begin{bmatrix}+3&0&-3\\+10&0&-10\\+3&0&-3\end{bmatrix}}* {A} \quad {\mbox{and}}\quad {G_{y}} ={\begin{bmatrix}+3&+10&+3\\0&0&0\\-3&-10&-3\end{bmatrix}}* {A} }$
    :::
- 比 Sober 更加精確(accurate)
    - ![](https://i.imgur.com/8tDH7qj.png)
#### 4.3 High : Canny Edge Detector
- [定義](https://medium.com/@pomelyu5199/canny-edge-detector-%E5%AF%A6%E4%BD%9C-opencv-f7d1a0a57d19)：
    :::success
    1. 預處理圖片，轉換成灰階，並利用 ***Gaussian Blur*** 去除雜訊
    2. 利用 ***Sobel filter*** 取得圖片每個 pixel 的梯度值和梯度方向
    3. 利用非極大值抑制（***Non-maximum suppression***）尋找可能的邊緣
    4. 根據**兩個閾值**選取 strong edge（確定的） 和 weak edge（進一步判斷）
    5. 選取和 strong edge **相連**的 weak edge 當作確定的 edge
    :::
- 3.利用非極大值抑制（***Non-maximum suppression***）尋找可能的邊緣
    - 可以想像在一個 edge 的區域，附近的每個 pixel 都會具有非零的梯度值，如果將這些 pixel 都當作 edge，最後就會產生很粗的 edge
    - 因此這一步的目的是**在密集的候選位置中，找出最大值，再把其他去掉**
        >實作的方式是把每個 pixel 和梯度方向的鄰居比較梯度值，如果不是最大的，就去除。
    - ![](https://i.imgur.com/hhWjGN6.png)
- 4.5.根據**兩個閾值**選取 *strong edge*（確定的） 和 *weak edge*（進一步判斷）、選取和 *strong edge* 相連的 *weak edge* 當作確定的 *edge*
    - threshold1, threshold2，用來區分 strong edge 和 weak edge
        >通常選擇 threshold2 / threshold1 = 1/2 ~ 1/3，例如 (70, 140), (70, 210)
    - 這一步驟透過**檢驗 weak edge 是否可以連到 strong edge 來判斷這個 edge 是否保留**
        >因此演算法反過來先從 strong edge 出發將 edge 延伸的方向（也就是垂直於梯度方向）的所有 weak edge 改成 strong edge
    - ![](https://i.imgur.com/Whed9Dt.png)
- 結果：![](https://i.imgur.com/6wvZljn.png)
#### 4.4 High : Difference of Gaussian
- 是一種將 一個原始灰度圖像的模糊圖像 從 另一幅灰度圖像 進行**增強**的算法，通過 DOG 以**降低模糊圖像的模糊度**
- [定義](https://zh.wikipedia.org/zh-tw/%E9%AB%98%E6%96%AF%E5%B7%AE)：
    :::info
    一幅圖像的不同 $\sigma$ 的 Gaussian Blur 表示為：
    $g1(x,y) = G_{\sigma1}(x,y)*f(x,y)$
    $g2(x,y) = G_{\sigma2}(x,y)*f(x,y)$
    若將上面濾波得到的 $g1$ 和 $g2$ **相減**得到：
    $g1(x,y) - g2(x,y)$
    $= G_{\sigma1}(x,y)*f(x,y) - G_{\sigma2}(x,y)*f(x,y)$
    $= (G_{\sigma1} - G_{\sigma2})*f(x,y)$
    $= DoG*f(x,y)$
    在二維的情況下為
    $DoG=f(u,v,\sigma ) = {\frac {1}{2\pi \sigma ^{2}}}\exp ^{-(u^{2}+v^{2})/(2\sigma ^{2})}-{\frac {1}{2\pi K^{2}\sigma ^{2}}}\exp ^{-(u^{2}+v^{2})/(2K^{2}\sigma ^{2})}$
    :::
    - ![](https://i.imgur.com/vrTnKQW.png)
        - 它從一個窄高斯減去一個寬高斯，是**墨西哥帽小波**的一個近似
    - ![](https://i.imgur.com/fApui2q.png)
- 結果：![](https://i.imgur.com/P3hU8O7.png)![](https://i.imgur.com/w5a8PQh.png)
- 在DOG算法中，它被認為是在模擬視網膜上的神經從影像中提取信息從而提供給大腦
- 但這個算法的一個主要缺點就是在調整圖像對比度的過程中信息量會減少
:::warning
:recycle: 大部分的邊緣銳化算子使用增強高頻信號的方法，但是因為隨機雜訊也是高頻信號，很多銳化算子也增強了雜訊。
而 DOG 算法**去除的高頻信號中包含了隨機雜訊**，所以這種方法是最適合處理那些有高頻雜訊的圖像
:::
### 5. Correlation and Convolution
- filter相反，但當filter的x軸與y軸對稱時，在2-D的運算上就沒有差別了
![](https://i.imgur.com/9kiFkZo.png)
### 6. Multi-Resolution：Downsampling (Encoder)
- 這裡就會使用到剛剛提到的 DoG 來當作工具
![](https://i.imgur.com/lfMjad0.png)
### 7. AutoEncoder – Convolutional Encoder and Decoder
![](https://i.imgur.com/ve2PMia.png)
## Ch6. Image Transformes
### preliminary：Canny Algorithm
![](https://i.imgur.com/sk7lyBd.png)
:::info
:+1: 把圖形轉成線，但門檻不要設太高，否則會把某些重要資訊過濾掉
:::
### 1. Hough Transform
#### 1.1 Circle
- 把每點都轉成圓圈表示( r 待定)
![](https://i.imgur.com/aj5b4Ks.png)
![](https://i.imgur.com/JOiiVqq.png)
![](https://i.imgur.com/Nm4B7ZN.png)
- 如此一來，就找到 baby 的頭了
#### 1.2 Line
- 極座標：![](https://i.imgur.com/5SbN5V8.png)
- 表示法：![](https://i.imgur.com/vHogVVE.png)
（右上圖）影像空間中任何一個點，可以射出無限多條直線。
從原點對這些線做垂線，可以發現 $r、\theta$ 會一直變動，
（左上圖）把這些現 $r、\theta$ 記錄下來，就是在記錄一個點。
![](https://i.imgur.com/fGlpl6G.png)
如此一來，交點的 $r、\theta$ 就是代表一條影像空間中的線。
:::success
:100: 根據上述兩種方法，我們就算遇到不完整的直線或圓，也能用 Hough Transform 判斷出直線和圓的大致位置（因為是使用 voting），此外，也可以使用在不規則形上。
:::
- 做 Hough Transform 之前，通常會先使用 sobel filter，偵測出邊緣再執行
- tracking vs detection
    - 以 recognition 為例
    - (先做) dectection 是做影像前處理、整張圖片偵測位置等等
    - (後做) tracking 是對範圍比較小的部分做 prediction

### 2. World to Camera to Image Coordinates
- Rotate Transformation
    - ![](https://i.imgur.com/tYAtXgc.png)
    - ![](https://i.imgur.com/gsSml1p.png)
- Affine Transformation
    - ![](https://i.imgur.com/YPac7D7.png)
    - 需要六個式子才能解 6 個未知數，所以最少需要 3 個點 6 個座標
    - ![](https://i.imgur.com/0nXi1w8.png)
    - ![](https://i.imgur.com/UbOLAjN.png)
- Projective Transformation
    - ![](https://i.imgur.com/G94vhaf.png)
    - 非線性轉換，用線性的矩陣去逼近最佳化，越接近 groud truth 越好
    - 此時 $h_{20}、h_{21}、h_{22}$ 就會有值了，而不再是 001
### 3. Intergral Image
- $ii(x , y)$ : Sum of the pixels 左上角的 $(x , y)$.
- $ii$圖定義
    - ![](https://i.imgur.com/F3KCxbO.png)
- 已知$ii$圖，求原圖：
    - ![](https://i.imgur.com/tAtN6Ku.png)
- 求$ii$圖，先算 row 的 sum、再求 column 的 sum
    - ![](https://i.imgur.com/E3YKUuk.png)
:::info
- 可以幫助我們計算 Gaussian Model 時，**$cov[x] = E[x^2] - (E[x])^2$** 的計算速度
- 也可以加速圖形的 filter 類型的 feature 萃取 
    - ![](https://i.imgur.com/7yk73jG.png)

:::
## Ch7. Histograms and Matching
### 1. Histogram
#### 1.1 Basic Infomation
:::warning
- 2D → 1D + 1D
- 研究 probabilty
:::
- 適當的連續區間
    - ![](https://i.imgur.com/EC4EdLG.png)
    - 每一點表示，每一個 pixel 顏色的其中兩個座標（可能是HSV三個值中的其中兩個值）
- 不恰當的情況
    - ![](https://i.imgur.com/QS6Bz00.png)
- 機率標準化 Normalized to probability $p()=1.0$
    1. 整塊 histogram 的 probability density 標準化為 1.0
    2. 最高的 bin of histogram 標準化為 1.0
- 受光線影響下的 RGB 與 HSV histograms
    - ![](https://i.imgur.com/fVSVeNS.png)
    - 可以看出 HSV 相較穩定
- 四種 metrics 去計算兩個 histograms 的 matching
    - *Correlation*
        - ![](https://i.imgur.com/xPP6JFO.png)
    - *Chi-Square*
        - ![](https://i.imgur.com/zNZHTp4.png)
    - *Intersection*
        - ![](https://i.imgur.com/HNhKEBQ.png)
    - *Bhattacharyya*
        - ![](https://i.imgur.com/2DX7ce7.png)
#### 1.2 Back Projection
>A way of recording how well the pixels of a given image fit the distribution (probability) of pixels in a histogram model
- Training database
    - 如果框起藍色區域的 HS 值，可以得到右下圖的兩個 1D 的機率分布（橫軸為 H、縱軸為 S）
    - ![](https://i.imgur.com/G9Kvxcp.jpg)
- Test image（使用右上角的 distribution）
    - ![](https://i.imgur.com/Q8RlVrY.png)![](https://i.imgur.com/ORGUXsU.png)
    - 輸入左圖，可以得到右圖的機率分布

#### 1.3 Histogram Equalization
>A method that improves the contrast in an image
- original 低對比：
    - ![](https://i.imgur.com/c43Pn2l.png)
- equalized 結果：
    - ![](https://i.imgur.com/oinZmpF.png)
- 作法使用 cumulative density function 去 equalize a Gaussian distribution
    - ![](https://i.imgur.com/E6kq0O0.png)
    - ![](https://i.imgur.com/GkoPxng.png)
### 2. Matching
- 如要找到狗狗的頭
    - ![](https://i.imgur.com/L0B1xDP.png)
- 兩種方式：
    - SSD：Sum-of-Squared Differences
        - ex：Normalized by Gaussian Model (Varice)
        - ![](https://i.imgur.com/7Sai8E9.png)
    - MSE：Mean Squared Error
        - ex：Loss function
        - ![](https://i.imgur.com/iP2dbbX.png)
### 3. AI Bayesian Decision Rule
![](https://i.imgur.com/qPKugLS.png)

## Ch11. Camera Modeling and Camera Calibration
### 1. Image and Signal Processing (ISP)
- 鏡頭參數
    - ![](https://i.imgur.com/zT9q631.png)
- 螢幕解析度
    - ![](https://i.imgur.com/oxOEKrB.png) 
- Pine Hole Camera Model
    - ![](https://i.imgur.com/OuBm69B.png) 
- World to Camera to Image Coordinates
    - ![](https://i.imgur.com/d9CFvci.png)
    - ![](https://i.imgur.com/c9zL06E.png)
- Projective Geometry
    - ![](https://i.imgur.com/3FdhDmT.png)
### 2. Homogenous Coordinates
> Homogenous coordinates（Matrix） are a mechanism that allows us to 
associate points and vectors in space with vectors in $R_Real$
- $x\prime=z\prime\frac{x}{z}, y\prime=z\prime\frac{y}{z}, z\prime=z\prime$
- Location/Point u = Unit vector * Amplitude
- ![](https://i.imgur.com/GXovJuh.jpg)
- ![](https://i.imgur.com/gXiBPLv.png)
- Advantage of Homogenous
    - 用矩陣相乘的方法表達 rigid transformation
    - 很容易的做 optimization
:::info
**Solution/Optimization of Homogenous Matrix**
- *Closed-Form Solution*
    > 等於 0 用
    - $Ax = 0$ => 
    - $A^tA$ = Covariance Matrix = $SVD$ = $UWU^T$
    - Smallest eigenvalue > 0 => eigenvector
- *Pseudo Inverse*
    > 不等於 0 用
    - $Ax = b$ =>
    - $x=(A^TA)^{-1}* A^Tb$
- *Sum of Squared Difference*
    > 利用 max likelihood – exponential term 來逼近參數
    - $\min E = \sum(Ax-b)^2$
        - $Ax = b’$: estimation value. $b$: **ground truth**, $\min E = \sum( b’-b)^2$ 
            - linear approach：Pseudo Inverse
            - non-linear approach：LM（Levenberg-Marquardt Algorithm）
        - $Ax = b’$: estimation value. $b’’$: estimation value, $\min E = \sum( b’-b’’)^2$
            - EM（Expected-Maximization）
- *Lagrange Approach (outlier) with constraint*
    > ![](https://i.imgur.com/jQMpJjU.png)
    > 多一個 $\lambda(x^2 +y^2)$ 可以減少右邊兩圖 Variance 較高的情況
    - $\min E = \sum(Ax-b)^2 + \lambda(x^2 +y^2)$
:::
### 3. Camera Calibration
> 2D Image Coordinate 與 3D World Coordinate 的轉換
- 目的為產生 projection matrix, intrinsic and extrinsic parameters 的估計
    - ![](https://i.imgur.com/QKTsYTh.png)
- 方法為上方提到的 Homograph coordinate 來解
- Undistortion
    - ![](https://i.imgur.com/z2fTgPn.png)
    - 扭曲的原因
        - Radial(輻射狀的) Distortion ![](https://i.imgur.com/BG0dlL7.png)
        - Tangential(切線的) Distortion ![](https://i.imgur.com/4NfivJB.png)


:::success
:+1: 結論
**Calibration Procedure**
1. Print a pattern and attach it to a planar surface.
    > 就是把板子印出來
2. Take a few (15~20) images of the model plane under different orientations by moving either the plane or the camera.
    > 拍很多照片
3. Detect the feature points (corner points) in the images.
    >擷取出內部邊角的點
    > ![](https://i.imgur.com/X4BZnIZ.png)
    > ![](https://i.imgur.com/fkmtjrF.png)
- 下方之後為數學運算
4. Estimate the five intrinsic parameters and all the extrinsic parameters using the *closed-form solution*. 
    > 找出內部外部參數
5. Estimate the coefficients of the radial distortion by solving the linear least-squares – *Pseudo Inverse* $k = (D^TD)^{-1}D^Td$
    > 找出 distortion 參數
6. Refine all parameters by minimizing *Sum of Squared Difference SSD* $\sum_{i=1}^{n}\sum_{j=1}^{m}||m_{ij}-\hat m(A,k_1,k_2,R_i,t_i,M_j)||^2$ 
    > 4.5.兩項，利用這個方式逼近參數(如深度學習)
- Result：
    ![](https://i.imgur.com/Zh46sDW.png)
:::
- Rodrigues
    - 旋轉向量與旋轉矩陣可以通過 Rodrigues 變換進行轉換
    - ![](https://i.imgur.com/Kx8oIto.png)
## Ch12. 3D Sensor
### 1. Introduction
- Motivation
    - 藉由左右2顆攝影機的視差所求得的對應位置的 disparity，可用來估計拍攝場景中的物體的深度差異(3D)
    - ![](https://i.imgur.com/cEdsto4.png)
    - 如果物體本身沒有結構上的差異（分不出移動於否），就需要 Structured Light 結構光先打在物體上
### 2. Stereo
- 在一個 stereo system，我們有兩張左右的圖片，而目的就有： 
    - 場景的 3D structure
    - 兩個 camera 的相對位置
    > ![](https://i.imgur.com/JuDXQG8.png)
    > ![](https://i.imgur.com/1fq16Jj.png)
- Simple Stereo system
    - $Z = \frac{f * B}{d}$
        > ![](https://i.imgur.com/2j1psFv.png)
    - 利用相似三角形比例公式
        > ![](https://i.imgur.com/Dh7fTBW.png)
    - 也可以改變鏡頭的位置，不一定要平行放置
        > ![](https://i.imgur.com/uyzrAjR.png)
        > 上圖可以更利於近物的 3D 建構
    - Ground Turth：
        > ![](https://i.imgur.com/gZGwLRP.png)
    - 實際結果：
        > ![](https://i.imgur.com/J2FXiPq.png)
    - [參考影片：Simple Stereo | Camera Calibration](https://www.youtube.com/watch?v=hUVyDabn1Mg)
        > ![](https://i.imgur.com/WSpM3cv.png)
        > ![](https://i.imgur.com/lKIPq8H.png)
## Homework
### Pytorch
- 如何使用已經預訓練好的 model
    - [solving CIFAR10 dataset with VGG16 pre-trained architect using Pytorch, validation accuracy over 92%](https://medium.com/@buiminhhien2k/solving-cifar10-dataset-with-vgg16-pre-trained-architect-using-pytorch-validation-accuracy-over-3f9596942861)
- 如何從頭建 model
    - [Understanding PyTorch with an example: a step-by-step tutorial](https://towardsdatascience.com/understanding-pytorch-with-an-example-a-step-by-step-tutorial-81fc5f8c4e8e#5017)
    - [WELCOME TO PYTORCH TUTORIALS](https://pytorch.org/tutorials/)
    - [PyTorch: Training your first Convolutional Neural Network (CNN)](https://pyimagesearch.com/2021/07/19/pytorch-training-your-first-convolutional-neural-network-cnn/)
    - [如何在PyTorch上使用GradCAM進行神經網路分類依據視覺化?](https://yanwei-liu.medium.com/pytorch-with-grad-cam-6a92a54bfaad)
- 視覺化
    - [VISUALIZING MODELS, DATA, AND TRAINING WITH TENSORBOARD](https://pytorch.org/tutorials/intermediate/tensorboard_tutorial.html)
    - [PyTorch: Training your first Convolutional Neural Network (CNN)](https://pyimagesearch.com/2021/07/19/pytorch-training-your-first-convolutional-neural-network-cnn/)
- Out of memory
    - [FREQUENTLY ASKED QUESTIONS](https://pytorch.org/docs/stable/notes/faq.html)
## Final Project
### 1. GAN
- [李宏毅機器學習筆記05 GAN](https://zhuanlan.zhihu.com/p/396399148)
- [【機器學習2021】生成式對抗網路 (Generative Adversarial Network, GAN) (一) – 基本概念介紹](https://www.youtube.com/watch?v=4OWp0wDu6Xw)
- [【機器學習2021】生成式對抗網路 (Generative Adversarial Network, GAN) (二) – 理論介紹與WGAN](https://www.youtube.com/watch?v=jNY1WBb8l4U)
- [【機器學習2021】生成式對抗網路 (Generative Adversarial Network, GAN) (三) – 生成器效能評估與條件式生成](https://www.youtube.com/watch?v=MP0BnVH2yOo)
- [【機器學習2021】生成式對抗網路 (Generative Adversarial Network, GAN) (四) – Cycle GAN](https://www.youtube.com/watch?v=wulqhgnDr7E)
### 2. Vanilla GAN
- [Generative Adversarial Network系列: Vanilla GAN和Divergence](https://syhuang1990.medium.com/generative-adversarial-network%E7%B3%BB%E5%88%97-vanilla-gan%E5%92%8Cdivergence-43e3b088c511)
### 3. StyleGAN & StyleGAN2
- [GAN — StyleGAN & StyleGAN2](https://jonathan-hui.medium.com/gan-stylegan-stylegan2-479bdf256299)
- [A Style-Based Generator Architecture for Generative Adversarial Networks](https://arxiv.org/abs/1812.04948)
- [NVlabs/stylegan](https://github.com/NVlabs/stylegan)
### 4. StyleGAN-XL
- [autonomousvision/stylegan_xl](https://github.com/autonomousvision/stylegan_xl)
## OpenCV
- [python-OpenCV寻找角点findChessBoardCorners](https://blog.csdn.net/qq_35565669/article/details/106606661)
- [Cv2 findChessboardCorners fails to find corners](https://stackoverflow.com/questions/66225558/cv2-findchessboardcorners-fails-to-find-corners)
- [Camera Calibration - OpenCV](https://docs.opencv.org/4.x/dc/dbb/tutorial_py_calibration.html)
- [二維模式相機校正 (2D Pattern Camera Calibration) 2020-04-06  Liu, An-Chi 劉安齊](https://tigercosmos.xyz/post/2020/04/cv/camera-calibration/)
- [Step 4: Calibrate Camera](https://learnopencv.com/camera-calibration-using-opencv/)
- [理解numpy中的meshgrid()方法](https://wangyeming.github.io/2018/11/12/numpy-meshgrid/)
- [Python的 numpy中 meshgrid 和 mgrid 的区别和使用](https://www.cnblogs.com/shenxiaolin/p/8854197.html)
- [Simple Stereo | Camera Calibration](https://www.youtube.com/watch?v=hUVyDabn1Mg)
- [Locate specific pixel from left and right view on the disparity map](https://answers.opencv.org/question/234639/locate-specific-pixel-from-left-and-right-view-on-the-disparity-map/)
- [Python-OpenCV hw2筆記](https://hackmd.io/@-uoCoKkVTp2zUnRuNFpEBg/Python-OpenCV%E7%AD%86%E8%A8%982)
- [OpenCV imshow()](https://docs.opencv.org/4.x/d7/dfc/group__highgui.html#ga453d42fe4cb60e5723281a89973ee563)
## 參考資料
- [國立成功大學資訊工程學系 連震杰教授](https://www.csie.ncku.edu.tw/zh-hant/members/25)：[2022 Fall 影像處理、電腦視覺及深度學習概論](http://robotics.csie.ncku.edu.tw/Course/Course2022_Fall_Bs/course_2022_Bs.htm)
