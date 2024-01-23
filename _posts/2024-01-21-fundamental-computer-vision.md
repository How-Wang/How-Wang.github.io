---
layout: post
title: 基礎電腦視覺
subtitle: Why is vision so difficult? In part, it is because it is an inverse problem, in which we seek to recover some unknowns given insufficient information to fully specify the solution. We must therefore resort to physics-based and probabilistic models, or machine learning from large sets of examples, to disambiguate between potential solutions.
categories: 電腦視覺
tags: [電腦視覺, 基礎科學]
---
## 1. Camera Models

### 1.1 Pinhole cameras
![](https://hackmd.io/_uploads/r1wnELnJT.png)
- $f$ 代表 focal length
- $o$ 可以稱作 pinhole = aperture = center of the camera

![](https://hackmd.io/_uploads/S1O-SL2yT.png)
- 使用座標系來表示此系統

![](https://hackmd.io/_uploads/rJ0jrL2J6.png)
![](https://hackmd.io/_uploads/B13vFI2y6.png)
- 使用相似三角形可以以舊座標表示投影後的座標

![](https://hackmd.io/_uploads/HJ0NAUhyp.png)
- image plane 上所呈現的 Digital Image

![](https://hackmd.io/_uploads/BktNEDhJ6.png)
- 在 image plane 上的座標，改以中心點 $C_x, C_y$ 來表示其他位置

![](https://hackmd.io/_uploads/rJfZrw31T.png)
- 原本的位置，都是以距離作為單位
- 如果我們用 pixel 來表示，就需要多乘上 $k, l$ 來轉換基礎單位
- 而我們把
    - $f * k$ 寫作 $\alpha$
    - $f * l$ 寫作 $\beta$

![](https://hackmd.io/_uploads/ByRFBP2Jp.png)
- 我們可以得出 $eq.5$ 表示方式
- 但 projective 是線性轉換嗎？
    - 不是，因為 $z$ 的位置在 $P\prime$ 分母
    - 我們不可能利用線性轉換，將 $P$ 內的 $z$ 轉換到 $P\prime$ 的分母

- 那 Projective 還可以用 matrix 的形式來表達嗎？
    - 可以
    - 不使用 Euclidean coordinates 而是使用 **Homogeneous coordinates**

![](https://hackmd.io/_uploads/BkRRiwhy6.png)
- 在 Euclidean system 多加一個維度的 scalar，值為 1
    - 即為 Homogeneous system
    - 如果要轉換回 Euclidean，則統一除以此 scalar

![](https://hackmd.io/_uploads/rkzIPuhkT.png)
- 而 projective transformation 就可以用此 matrix 來表示

![](https://hackmd.io/_uploads/HJ1kOun1a.png)
- $3*3$ 的部分，就稱作 Camera matrix $K$

![](https://hackmd.io/_uploads/S1kZqFny6.png)
![](https://hackmd.io/_uploads/H1b95Y2Ja.png)


![](https://hackmd.io/_uploads/Hk3LeYnkp.png)


### 1.2 The geometry of pinhole cameras
![](https://hackmd.io/_uploads/HkKcGFnkT.png)
- 剛剛的討論，都只有相機內部的系統(camera reference system)
- 但我們也要討論外部世界的系統(world reference system)
    - 也就是圖上的 $R, T$
- 先以 $2D$ 世界作為範例

![](https://hackmd.io/_uploads/BJz9QtnJT.png)
- 以 Homogeneous coordinates 表示 $2D$ 的 shift

![](https://hackmd.io/_uploads/SynimKhJ6.png)
- $2D$ 的 scale

![](https://hackmd.io/_uploads/H1TCmY21T.png)
- $2D$ 的 rotate

![](https://hackmd.io/_uploads/HyCGEthkT.png)
- $2D$ 的 shift + rotate + scale

轉換到 3D 亦然
![](https://hackmd.io/_uploads/HkXPVK2ya.png)
- $3D$ 移動
![](https://hackmd.io/_uploads/HkZiNF3kT.png)
- $3D$ 旋轉
![](https://hackmd.io/_uploads/ByMANt3yp.png)
- $3D$ 平移＋旋轉 
    - 現實情況，Rigid 不會有 scale
    - 6 degree of freedom

![](https://hackmd.io/_uploads/SJ0sSKnya.png)
- 將 camera reference system (Internal parameter) 與 world reference system (External parameter) 兩者整合

![](https://hackmd.io/_uploads/HJ2qiFhJT.png)
- 共有 11 個 degrees of freedom

![](https://hackmd.io/_uploads/HJPAiY3J6.png)
- 轉回尤拉座標系

![](https://hackmd.io/_uploads/HJdihYhyp.png)
![](https://hackmd.io/_uploads/B156nt2kp.png)
- 當目標很遠時，會出現 Horizon line (vanishing line)
- 因此研究多點成相的時候（前面只有研究單點），可以是坐在同一個面上面

![](https://hackmd.io/_uploads/By4rTYh1T.png)
- Projective 可以簡化為 Weak perspective

![](https://hackmd.io/_uploads/Hkqs6Knyp.png)
- Weak perspective 數學上表 $m_3$ 項為 $1$

## 2. Camera Calibration
### 2.1 Camera calibration problem
![](https://hackmd.io/_uploads/BJlMF931a.png)
- Internal parameters 與 External parameters 乘開後可以得到 $M$

![](https://hackmd.io/_uploads/rkQitchka.png)
- 我們從照片的資料點，來回推 $M$ 這個 matrix，就是 Calibration problem

![](https://hackmd.io/_uploads/BJKl9qhkT.png)
- 上一章得知，$M$ 有 11 個參數，因此需要 11 個 equation 才能解出
- 而每一的點可以提估 2 個 equation (x and y)
- 因此需要 6 個點
- 但在實務上，我們會使用超過 6 個對應點，加強 Robustness

![](https://hackmd.io/_uploads/HJIlocn16.png)
- 投影點 $p_i  = [u_i, v_i]$ 與被投影點 $P_i$ 的關係

![](https://hackmd.io/_uploads/By5Woc2ka.png)
- 移項

![](https://hackmd.io/_uploads/HJYij931T.png)
- 取 $n$ 個點來解聯立

### 2.2 Camera calibration with radial distortion

![截圖 2023-12-04 下午5.01.38](https://hackmd.io/_uploads/H12cHfiBa.png)


![截圖 2023-12-04 下午5.03.12](https://hackmd.io/_uploads/rJTRBGsBa.png)
- Distortion 就會用一個 $\lambda$ 來表達

![截圖 2023-12-04 下午5.04.58](https://hackmd.io/_uploads/SJwHUziHa.png)
- 如果 $\lambda$ 只跟 camera 有關就會非常容易
- 但實際上還會跟 **2D point** 本身的位置 $(u, v)$ 有關，也就是參數 $d$
- 此外也有一個參數 $\kappa_p$ 有關

![截圖 2023-12-04 下午5.15.23](https://hackmd.io/_uploads/HyFhOziS6.png)
- 直覺方式
    - 求 $\lambda$ 的方式跟前面沒有 distortion 一樣，只是這裡將 $\lambda$ 跟 Camera matrix $M$ 合成 $Q$
- 但會遇到的問題
    - 是 $\lambda$ 跟位置 $(u, v)$ 有關
    - 所以這個式子也不再是 linear 的，沒辦法用解方程式的方式解

![截圖 2023-12-04 下午5.14.45](https://hackmd.io/_uploads/HkbcdMsS6.png)
- 可以用的方式
    - Newton Method
    - Levenberg-Marquardt Algorithm (LM)
        - 一開始先初始化
        - Esitmated 一個 solution
        - 再慢慢逼近最後的結果
- 因此我們先假設是 linear 的結果當成是初始值
    - 再進一步使用 Newton 或 LM 來繼續解


![截圖 2023-12-04 下午5.21.46](https://hackmd.io/_uploads/B184cfoB6.png)
- 傳統的假設
    - zero-skew
    - quare pixel
    - 那 $(u_0, v_0)$ 就是 image 的中心
- 那如此一來，每一個點我們可以都改寫成上面的形式

![截圖 2023-12-04 下午5.23.44](https://hackmd.io/_uploads/ry2s5zsHa.png)
- 如果我們把每一個點的 $u,v$ 來相除，那這樣就可以把 $\lambda$ 給消去
- 那系統就回到 linear 的狀態，就能把 $m_1, m_2$ 解出來


![截圖 2023-12-04 下午5.34.38](https://hackmd.io/_uploads/rJ0E6fsH6.png)
- 接著再把 $\lambda$ 跟 $m_3$ 這兩個 nonlinear 的值，利用前述的 LM 解開

## 3. Single View Geometry
### 3.1 Review calibration and 2D transformations

![截圖 2023-12-04 晚上8.05.03](https://hackmd.io/_uploads/HJJYxBiHa.png)
- 在已知 Camera Matrix (Intrinsic + Extrinsic) 的條件下，我們可以將 point 從 3D 的空間投影到 2D 的平面上
    - $O_w$ 經過 Extrincsic $R,T$ 轉換到 $C$ 這個空間
    - 再利用 Intrincsic $K$ 投影到圖像上
- 那我們可以反過來，從 2D 的點，重建回 3D 的點嗎？
    - No in general
    - 但我們可以知道 $P$ 會在哪一條線上
    - 是由 $C$ 與 $p$ 所決定的

![截圖 2023-12-04 晚上8.15.35](https://hackmd.io/_uploads/SkwxQBoHp.png)
- 假設 $R$ 為 $I$、$T$ 為 $0$
- 根據關係，我們可以得到上面的數學表示式
    - 由此可以找到在 3D 上面的 line $P_E$
    - 由 C 和 p 所定義

![截圖 2023-12-04 晚上8.36.23](https://hackmd.io/_uploads/HkB0wrira.png)
- 這是一條線的表達方式


![截圖 2023-12-04 晚上8.37.38](https://hackmd.io/_uploads/B1J7dror6.png)
- 而因為中心點就是 camera center
    - 所以出發點為 $(0, 0, 0)$
- 向量 $d$ 也可以藉此被求出
    - 所以我們只需要知道 $K$ 與 2D 在 homogenious coordinate 上的點 $p_h$
    - 就可以知道 3D 的線 $P_E$

- 以下複習 2D 的 transformation
![截圖 2023-12-04 晚上9.04.47](https://hackmd.io/_uploads/Hyc_AHiHp.png)
![截圖 2023-12-04 晚上9.05.55](https://hackmd.io/_uploads/SkkaCBjS6.png)
- Isometries
    - Rotation(1 DOF) + Translation (2 DOF) 
    - 共 3 DOF
    - Regulate motion of rigid object

![截圖 2023-12-04 晚上10.04.16](https://hackmd.io/_uploads/B1jP3IiBp.png)
- Similarity
    - 比 Isometries 多了 scale $s$
    - 4 DOF

![截圖 2023-12-04 晚上10.05.32](https://hackmd.io/_uploads/SyK3n8oB6.png)
![截圖 2023-12-04 晚上10.05.55](https://hackmd.io/_uploads/r1R6h8iHp.png)

- Affinities
    - 6 DOF
        - 可以視為
        - 2 DOF 是 Translation $t_x, t_y$
        - 2 DOF 是 scale，$S_x, S_y$
        - 2 DOF 是 Rotation，$\theta, \phi$
    - 平行 依然會維持
    - Ratio of lengths on collinear lines
        - ![截圖 2023-12-04 晚上10.10.51](https://hackmd.io/_uploads/SJ8xC8sSp.png)
        - 線上的點之間的距離會成比例
- 可以使用 $SVD$ 來分解
    - ![截圖 2023-12-04 晚上10.12.42](https://hackmd.io/_uploads/rymdA8orp.png)

![截圖 2023-12-04 晚上10.26.06](https://hackmd.io/_uploads/S1cY-DiS6.png)
![截圖 2023-12-04 晚上10.26.35](https://hackmd.io/_uploads/BkcsWPjSa.png)
- Projective
    - 多了 $v$，是一個 $1*2$ 的 row matrix，所以比 Affinities 多 2 DOF
    - $6+2=8$ DOF
    - 保持 Collinearity，也就是從 line still map to line
    - 但平行不會維持了
    - cross ratio of 4 collinear points 會維持
        - ![截圖 2023-12-04 晚上10.37.21](https://hackmd.io/_uploads/rJCQ4vsBT.png)
- example
    - ![截圖 2023-12-04 晚上10.31.39](https://hackmd.io/_uploads/H1cz7woH6.png)

### 3.2 Vanishing points and lines

![截圖 2023-12-04 晚上10.38.14](https://hackmd.io/_uploads/By_54PoBa.png)
- 一組平行線在照片上的交點
- 最遠的綠點稱作 Vanishing point
- 最遠的青線稱作 Vanishing line

![截圖 2023-12-10 晚上8.37.18](https://hackmd.io/_uploads/HkKWZ47Up.png)
- 在考慮如何表示 Vanishing line 之前
- 我們先複習如何在 2D 平面上來表示一直線
- 可以利用點 $[x_1, x_2]^T$ 的在 homogeneous coordinate 與線向量 $[a,b,c]$ 的**內積** $=0$

![截圖 2023-12-10 晚上8.49.20](https://hackmd.io/_uploads/rk207VX86.png)
- 如何找兩條線的交點
    - 使用 cross product **外積**

:::success
- 表示線用 **內積**
- 交點用 **外積**
:::

![截圖 2023-12-10 晚上8.54.53](https://hackmd.io/_uploads/BkumrVmUp.png)
- 那如何表示無窮遠的焦點呢？
    - 讓 homogenious coordinate 的 $z$ 為 0
    - 證明就是利用自己假設的兩條平行線，$l\cross l \prime$ 來求交點

![image](https://hackmd.io/_uploads/SJDhr47Ua.png)
- 補充 cross product 的公式

![截圖 2023-12-10 晚上8.59.17](https://hackmd.io/_uploads/Sk-EUVmLa.png)![截圖 2023-12-10 晚上8.59.45](https://hackmd.io/_uploads/HJ3SU4mU6.png)![截圖 2023-12-10 晚上9.00.02](https://hackmd.io/_uploads/Hk0IUE7L6.png)
- 得證，無窮遠的點的表示方法

![截圖 2023-12-10 晚上9.17.51](https://hackmd.io/_uploads/SJhY54QUa.png)
- 回頭帶入，就可以知道
    - 無窮遠的點 $x_\infty = [b, -a, 0]^T$
    - 跟線向量 $[a, b, c]$ 內積為 $0$
    - 表示會經過線 $I = [a, b, c]$
    - 一組平行線，也就是一個方向，會對應到一個 vanishing point

![截圖 2023-12-10 晚上9.22.42](https://hackmd.io/_uploads/rJxhsV786.png)
- 每一個位在無限遠的點，都會 lie on a line，這個 line 是 $l_\infty = [0, 0, 1]$
    - 因為每個 infinite point $[x_1, x_2, 0]$ 跟其內積都會 $=0$

![截圖 2023-12-10 晚上9.28.32](https://hackmd.io/_uploads/S1sbpNXLa.png)
- 在已經知道無限遠的點時，如果我們將他 project，那他還會保持無窮遠嗎？

![截圖 2023-12-10 晚上9.29.36](https://hackmd.io/_uploads/SyiSTVQ8a.png)
- 經過投影 matrix 可以知道
    - Projective 投影不會保持 infinity
    - Affine 會保持

![截圖 2023-12-11 下午1.15.08](https://hackmd.io/_uploads/Hy61jMN8a.png)
- 前面在對點做 transform 時，乘上的是 $H^T$
- 但如果要對線做 transform，需要乘上的是 $H^{-T}$
    - 如此一來，無窮遠的點才會落在無窮線上

![截圖 2023-12-10 晚上9.30.31](https://hackmd.io/_uploads/BkMtaNQUT.png)
- 如果對無窮遠的線做 Affine 與 Projective Transformation 呢？

![截圖 2023-12-11 下午1.30.23](https://hackmd.io/_uploads/ry0dCGVUa.png)
- 跟點一樣
    - Projective Transformation 不會維持 infinity
    - Affine 會維持

![截圖 2023-12-11 下午1.33.07](https://hackmd.io/_uploads/HyMQkXEUT.png)
- 移到 3D 的情況下，點和面的表示方法

![截圖 2023-12-11 下午2.30.47](https://hackmd.io/_uploads/HJHonX486.png)
- 一樣是利用 homogenious coordinate 最後一項為 $0$ 來表示位於無窮遠的點

![截圖 2023-12-11 下午2.32.07](https://hackmd.io/_uploads/BJLepX4L6.png)
- 利用一點與線向量來表示 $3D$ 上的線
- 也可以用兩張平面的交界，來表示一條直線

![截圖 2023-12-11 下午2.34.05](https://hackmd.io/_uploads/S12Da7VLT.png)
- 在理解點、線、面在 2D 與 3D 的關係後
- 此時我們將處在 3D 空間的無窮遠的點
- 投影在 2D 的平面上，結果就會是 vanishing point

![截圖 2023-12-11 下午2.49.46](https://hackmd.io/_uploads/S1KfWVEU6.png)
- 如果要找 vanishing point
    - 可以利用 3D 的 parallel line 線向量 \* camera matrix
- 而 3D 的線向量 $d$ 可以藉由 2D 投影點與 camera matrix $K$ 來計算得出

![截圖 2023-12-11 下午2.51.49](https://hackmd.io/_uploads/SyQqb44Ia.png)
- vanishing point 2D 與 3D 的圖示對應
- 之所以也可以稱作 horizon line，因為 vanishing line 可以代表觀測者的水平位置、水平軸線、地平線資訊
    - 1、2、3 個字的 horizon line 可以從圖上看到
    - [![截圖 2023-12-11 下午4.44.14](https://hackmd.io/_uploads/ryXB2HV86.png)](https://www.youtube.com/watch?v=4H-DYdKYkqk)
- infinity point 會在 infinity line 上
    - 有些垂直方向的 vanishing point 不會出現，但這些點是例外
    - ![截圖 2023-12-11 下午4.41.50](https://hackmd.io/_uploads/S1zI2SEUa.png)


![截圖 2023-12-11 下午2.57.40](https://hackmd.io/_uploads/SkcG7E48a.png)
- 如果兩線(yello)在 horizon line(orange) 上有交點，則兩線在 3D 平面上為平行線

![截圖 2023-12-11 下午3.13.34](https://hackmd.io/_uploads/r12sUVVI6.png)
- 3D 的面，投影到 2D，就會是線
- 現在我們有 2D 的 vanishing line，要回推 3D，稱為 Vanishing plane
- vanishing plane 的求法為
    - 利用 2D 的 horizon line (vanishing line)乘上 camera parameter 的 transpose $K^T$
    - 就可以找到 3D 的 vanishing plane
    - 也就是 Vanishing line 的延伸

:::warning
:100: **重點複習**
- parallel line 的交會是 infinity point
- infinity point 會在 infinity line 上（有些垂直的例外）
    - infinity point 經過投影是 vanishing point
    - infinity line 經過投影是 vanishing line
    - 另外有一個 vanishing plane 為一條 vanishing line 的延伸
:::

![截圖 2023-12-11 下午4.48.50](https://hackmd.io/_uploads/BJZW6H48T.png)
- 這裡也順便定義 infinity plane，也就是任何一條 infinity 都會經過的 plane

![截圖 2023-12-11 下午6.02.40](https://hackmd.io/_uploads/rJRrRLN8T.png)
- 在定義完所有的名詞後
- 因為我們前面知道，一組平行線，也就是一個方向都會對應到一個 vanishing point
- 因此我們可以去找尋兩個 Vanishing point 之間的角度
- 我們先前也知道 3D 的線向量 $d$ 可以藉由 2D 投影點與 camera matrix $K$ 來計算得出，因此可以將其帶入到餘弦公式

![截圖 2023-12-11 下午6.15.35](https://hackmd.io/_uploads/ByBIZDVI6.png)
- 在代入後，我們定義 $\omega = (KK^T)^{-1}$
- 並且得知，在 $\theta = 90$ 時，分子項 $v_1^T\omega v_2 = 0$

![截圖 2023-12-11 下午6.20.05](https://hackmd.io/_uploads/SJmvfwV8T.png)

- 接著我們可以來討論 $\omega$ 的 property
    - 可以得知是一個 symmetric
    - $\omega_2 = 0$ 表示 camera 沒有偏移
    - 如果 $\omega_2 = 0, \omega_1 = \omega_3$，圖像最後呈現為方形的像素點 square pixel

![截圖 2023-12-11 下午6.28.21](https://hackmd.io/_uploads/BJeWUEw4UT.png)
- 最後的 summary 表示，我們可以利用已知的 2D image、camera information 
    - 來 estimate 出 camera 
    - 跟 3D 的世界



### 3.3 Estimating geometry from a single image

![截圖 2023-12-11 下午6.40.56](https://hackmd.io/_uploads/BJe9wDELp.png)
- 接著要使用實例來解，因為我們從圖片上可以看出



![截圖 2023-12-11 下午6.49.21](https://hackmd.io/_uploads/BJKiFwVI6.png)![截圖 2023-12-11 晚上7.12.25](https://hackmd.io/_uploads/rytsRwNIT.png)
- 因為我們可以知道圖像上的相對 $90^{。}$關係，所以可以來解出 $\omega$
    - 總共是 $3$ degree of freedom，因為 up-to-scale 可以再減一個 dof
- 進而知道 $K$



![截圖 2023-12-11 晚上7.15.26](https://hackmd.io/_uploads/SyK_k_ELT.png)
- 在知道 $K$ 之後，我們接著利用圖形上可以看出的 horizon line，來求出 infinity plane

![截圖 2023-12-11 晚上7.22.40](https://hackmd.io/_uploads/BJbGWOVIa.png)
- 所以我們可以單純利用 vanishing point、vanishing line、90度資訊，以及推算出來的 camera parameter $K$
- 也就是 camera sysytem，去建構真實的結構
    - 但還是沒辦法知道實際的 scale 大小

## 4. Epipolar geometry
### 4.1 Triangulation

![截圖 2024-01-03 下午3.31.40](https://hackmd.io/_uploads/HyFPTYGda.png)
- 剛剛我們是利用 Single view
    - 去建構出 Structure of scene、Camera information $K$
    - 然而，我們必須先知道圖上 Knowledge，如 $90^{。}$ 關係，或是 infinity line 等等資訊
    - 但我們並不可能知道每張圖的這種關係，也可能未必存在
    - 在 3D 投影到 2D 容易產生 intrinsic ambiguity，例如深度資訊就很難被估計
    - 因此需要 Epipolar geometry，來判斷 Scene 的結構
- 利用雙眼可以建構出 3D 的 Scene 
    - 這樣的成像方式，稱為 triangulation

![截圖 2024-01-03 下午4.25.15](https://hackmd.io/_uploads/H1ug55z_a.png)
- 我們利用圖片上已知的資訊 $p$
- 估計出 $P^*$ 以接近實際情況的 $P$

![截圖 2024-01-18 晚上9.55.07](https://hackmd.io/_uploads/ryPTaiLta.png)


### 4.2 Example

![截圖 2024-01-18 晚上9.56.16](https://hackmd.io/_uploads/HkqPCj8Yp.png)
- 實際例子
- 在 $3D$ 情況是平行時
- $2D$ 圖片並不會平行，而是會收斂至 epipoles $e$

![截圖 2024-01-18 晚上9.58.55](https://hackmd.io/_uploads/BJqoRjIta.png)
- 在兩張圖片都 parallel 的例子
- Baseline 跟 image 不會有交點
- epipoles line 跟 $u$ 平行
- epipoles 不存在

![截圖 2024-01-18 晚上10.03.04](https://hackmd.io/_uploads/ryTRy28Yp.png)
- 兩張 image 是前後的情況，稱為 Forward translation
- 都是收斂到同一個 epipole

### 4.3 Epipolar Constraint

![截圖 2024-01-18 晚上10.08.49](https://hackmd.io/_uploads/Sy5zbnUY6.png)
- 給兩張相同物件的圖片
- 固定一張圖片的 $p$ 點，找尋 corresponding point $p\prime$

![截圖 2024-01-18 晚上10.12.58](https://hackmd.io/_uploads/S127z38Yp.png)
- 先找到對應到的 epipolar line
- 再去 fit color 來找到對應的點

![截圖 2024-01-18 晚上10.16.09](https://hackmd.io/_uploads/r143fhLKa.png)
- 基礎設定

![截圖 2024-01-18 晚上10.17.04](https://hackmd.io/_uploads/SknJ7hIK6.png)
- 兩張圖片分別對應到的 camera matrix $M, M\prime$
- Camera intrinsic 假設位在 canonical space，所以為單位矩陣

![截圖 2024-01-18 晚上10.21.53](https://hackmd.io/_uploads/rkJzEhIFp.png)
- 根據幾何關係
    - 紫色指外積 cross product，得出紅色的向量
    - 綠色指垂直，所以粉紅色與紅色向量內積為 $0$
- 最後可以得到 $[Ep. 7]$

![截圖 2024-01-18 晚上10.27.01](https://hackmd.io/_uploads/rJxHBnItT.png)
- 外積可以化簡

![截圖 2024-01-18 晚上10.27.55](https://hackmd.io/_uploads/rkPdHnLFT.png)
- 所以可以得到 $[Eq. 9]$ 的形式
- 而 $[T_x]\cdot R$ 就定義為 ==$E$, Essential matrix==

![截圖 2024-01-18 晚上10.33.24](https://hackmd.io/_uploads/rygpInIKa.png)
- 根據 $[Ep. 10]$ 我們可以先定義 $l, l\prime$，此式可以得出 $l, l\prime$ 會經過 $p, p\prime$（$p, p\prime$ 可以變動）
- 觀察圖形，即可得知 $l, l\prime$ 就是 epipolar line
- ![IMG_5914](https://hackmd.io/_uploads/S1cTqhUta.jpg)
    - 從此推論可以得知 $e$ 與 $E$ 的關係
- $E$ 的 DOF 是 $5$
    - $T$ 有 $3$ DOF
    - $R$ 有 $3$ DOF
    - 此結構為 up-to-scale，也就是如果 $P$ 的深度和 Baseline 都長度變兩倍，但他們的投影情況是一樣的，因此 up-to-scale 要剪掉 $1$ DOF
    - 所以最後的 $DOF=3+3-1=5$
    - 而由此也可知 $E$ 是 singular (rank $=2$)

![截圖 2024-01-18 晚上10.54.52](https://hackmd.io/_uploads/r1dpinLFp.png)
- 剛剛我們假設 $K$ 是位在 canonical space
- 所以剛剛算出來的 $p$ 其實是 $p_c$
- 但實際情況 $K$ 並不是在 canonical space
- 所以可以將剛剛算出來的 $p_c$ 用實際的 $p, K$ 來表示

![截圖 2024-01-18 晚上10.57.46](https://hackmd.io/_uploads/B1vuhh8Fp.png)

![截圖 2024-01-18 晚上10.59.21](https://hackmd.io/_uploads/HyBC32IFp.png)
- 經過整理後的參數們，得到 ==$F,$ Fundamental matrix==

![截圖 2024-01-18 晚上11.01.27](https://hackmd.io/_uploads/SkH8ThIt6.png)
- DOF 比 $E$ 多出兩個，就是 $K$ 與 $K\prime$

![截圖 2024-01-18 晚上11.02.22](https://hackmd.io/_uploads/Sy4JChLtp.png)
- 假設已知 $F$
- 那如果我們知道左圖的 $p$，就可以直接找到另一張圖的 epipolar line $l\prime$
- 因為 $F$ 包含了 
    - $2$ view 的 epipolar geometry 資訊
    - camera parameters

![截圖 2024-01-18 晚上11.13.06](https://hackmd.io/_uploads/S1i7gaLF6.png)
- The Eight-Point Algorithm
- 我們最少需要得到 8 組的點，才能 estimate $F$

![截圖 2024-01-19 凌晨12.31.18](https://hackmd.io/_uploads/rkmwzAUFT.png)
- 在一組情況下的列示，可以進行整理成 $[Eq. 14]$

![截圖 2024-01-19 凌晨12.32.40](https://hackmd.io/_uploads/HJN2z08t6.png)
- $8$ 組就能夠利用 SVD 來 estimate $F$

![截圖 2024-01-19 凌晨12.34.50](https://hackmd.io/_uploads/B1E4mRUKa.png)![截圖 2024-01-19 凌晨12.55.51](https://hackmd.io/_uploads/SkH7dC8YT.png)
- estimated 出來的 $\hat F$ 可能會是 full rank $(det(\hat F) ≠0)$
- 但實際上 fundamental matrix $F$ 要為 $Rank=2$
- 所以需要上圖的限制，盡量得到趨近於 $Rank=2$ 的 $\hat F$

### 4.4 Parallel image planes

![截圖 2024-01-19 下午4.42.27](https://hackmd.io/_uploads/Sye-U2PYp.png)
- 兩張 image 是平行的情況

![截圖 2024-01-19 下午4.52.34](https://hackmd.io/_uploads/Bkkwd3Pt6.png)
- 此時的 Essential matrix

![截圖 2024-01-19 下午4.53.34](https://hackmd.io/_uploads/Sk0q_hvY6.png)
- epipolar line 是 horizontal

![截圖 2024-01-19 下午4.55.28](https://hackmd.io/_uploads/rJTbt2vta.png)
![截圖 2024-01-19 下午4.55.37](https://hackmd.io/_uploads/Hy8MF2wK6.png)
- 由公式可以知道 $v= v\prime$

![截圖 2024-01-19 下午5.08.29](https://hackmd.io/_uploads/HJsGh3Dt6.png)
![截圖 2024-01-19 下午5.11.57](https://hackmd.io/_uploads/ByVN62PF6.png)
- Rectification 就是讓兩張圖片平行
- 達到 Epipolar constraint $v= v\prime$

![截圖 2024-01-19 下午5.08.02](https://hackmd.io/_uploads/rkfb3nPYa.png)
![截圖 2024-01-19 下午5.09.57](https://hackmd.io/_uploads/SkDc2hvKT.png)
- 為什麼需要 Parallel image planes？
    - 我們就可以直接利用 linear interpolation 來得出新的 View
    - 這就叫做 **View morphing**

![截圖 2024-01-19 下午5.14.47](https://hackmd.io/_uploads/ryLcTnwKa.png)
![截圖 2024-01-19 下午5.28.57](https://hackmd.io/_uploads/ByFyZpvKT.png)
- View morphing 也可以使用 Deep learning 的 model 來達成

![截圖 2024-01-19 下午5.36.08](https://hackmd.io/_uploads/ByY5GpPKp.png)
- parallel 第一個用處是產生 triangulation

![截圖 2024-01-19 下午5.30.15](https://hackmd.io/_uploads/HkrEWTPKa.png)
- 有了 parallel images 我們就可以得到 Point triangulation
- 進而計算出
    - $x$ 方向誤差 disparity $p_u-p_u\prime$
    - 深度 $z$ 等資訊

![截圖 2024-01-19 下午5.33.25](https://hackmd.io/_uploads/ry7lGpDFT.png)
- 利用相似三角形，計算表達出 $Z$ 

![截圖 2024-01-19 下午5.37.45](https://hackmd.io/_uploads/r1DgXaDKT.png)
![截圖 2024-01-19 下午5.38.56](https://hackmd.io/_uploads/ryAEXpwKa.png)
![截圖 2024-01-19 下午5.39.05](https://hackmd.io/_uploads/HJrrmpPYa.png)
- 第二個用處是能夠讓 correspondence 的任務比較簡單
    - 因為兩者就是在同一個水平面上
    - 方便直接比對

### 4.5 Correspondence problem

![截圖 2024-01-19 下午5.41.24](https://hackmd.io/_uploads/rkz0mawta.png)
- 最直覺的方式，在 epipolar line 上將顏色比對
- 相同的就是對應點
- 遇到的問題
    - line 上可能有多個相同顏色的點
    - 兩張圖片可能整體亮度會改變

![截圖 2024-01-19 下午5.50.43](https://hackmd.io/_uploads/HyWWUaDYT.png)
- 改以一個 window 來計算
- 並且使用 normalization

![截圖 2024-01-19 下午5.51.38](https://hackmd.io/_uploads/SJ_EIpvYp.png)
- 在不同 window size 下的結果

![截圖 2024-01-19 下午6.46.59](https://hackmd.io/_uploads/SyX4QRPta.png)
- 兩張 image 的投影像會遇到不佳的情況
- Shortening effect
    - 兩張圖像距離 $B$ 過遠，無法捕捉到好的細節
- Occlusions
    - object 距離 image $z$ 太近，可能兩張圖像抓到的內容會不同

![截圖 2024-01-20 上午11.38.58](https://hackmd.io/_uploads/rJkvgadKp.png)
- 為了降低 foreshortening and occlusions
    - $B$ 越小越好、$z$ 越大越好
    - $\frac{B}{z}$ 越小越好
- 然而 Measurement error
    - 會因為 $\frac{B}{z}$ 越小，從圖看出 Measurement error 反而上升（紅點與實際 GT 綠點的距離）
    - 因此兩者為 trade-off 必須取一個平衡

![截圖 2024-01-20 中午12.01.18](https://hackmd.io/_uploads/r1xjB6_YT.png)
![截圖 2024-01-20 中午12.01.48](https://hackmd.io/_uploads/rySe8TdKp.png)
- 除此之外，也會遇到其他比對上的問題
- homogenous regions，有相似顏色的區塊
- 或是 repetitive patterns，相似的 pattern 結構

![截圖 2024-01-20 中午12.04.27](https://hackmd.io/_uploads/ryKU8aOKT.png)
- 這時候我們就會需要使用 non-local 的 constraint
    1. Uniqueness，對應必須是一對一
    2. Ordering，每一個對應的內容，相對順序 order 會相同
    3. Smoothness，disparity 是一個 smooth 的 function
- 利用這三個內容來修正會遇到的種種 issue

## 5. Multi-view geometry

### 5.1 The SFM problem

![截圖 2024-01-20 中午12.13.47](https://hackmd.io/_uploads/ry6sdTuKT.png)
![截圖 2024-01-20 中午12.13.57](https://hackmd.io/_uploads/rk6iu6dF6.png)
- sturcture from motion 問題
- 利用輸入的 $m$ 張圖片，來建構出 $3D$ 結構裡的 $n$ 的點，產生出 $3D$ 點圖


![截圖 2024-01-20 中午12.16.17](https://hackmd.io/_uploads/BkeXK6dt6.png)
- $m$ 張照片就是 motion
- $n$ 個點就是 structure

### 5.2 Affine SFM

![截圖 2024-01-20 中午12.17.55](https://hackmd.io/_uploads/rybKKp_ta.png)
- Affine SFM 指的是 $3D$ 點投射到 image 上時，利用 Affine transformation

![截圖 2024-01-20 中午12.19.28](https://hackmd.io/_uploads/SyCCK6uFa.png)
- 複習 Affine 與 Perspective 兩種 transformation
- 差別在 $m_3$ 的值，Affine 比較簡單

![截圖 2024-01-20 中午12.21.22](https://hackmd.io/_uploads/SJkU56dt6.png)
![截圖 2024-01-20 中午12.21.39](https://hackmd.io/_uploads/rygvcpuKa.png)
- 目標就是
    - 根據已知的 image 上的點 $x_{ij}$
    - 預測 estimate 出正確的 $A_i, b_i, X_j$

![截圖 2024-01-20 中午12.26.07](https://hackmd.io/_uploads/Hys_opuK6.png)
- 共 $8m +3n-8$ DOF
- 分析
    - $8m$：為 $m$ 張圖片，每張有 $8$ DOF（$A$ 有 $2*3$、$b$ 有 $2*1$）
    - $3n$：為 $n$ 個 $3D$ 點，每個點有 $3$ 個座標
    - $8$：沒辦法完整預估的 constraint 限制

![截圖 2024-01-20 中午12.25.10](https://hackmd.io/_uploads/BkENjaOKa.png)
- 有兩種預測的方式
    - 先介紹 Factorization method
    - 又稱作 Tomasi & Kanade algorithm

![截圖 2024-01-21 下午6.11.49](https://hackmd.io/_uploads/H1blAwcta.png)
- 先對所有資料點做 centering

![截圖 2024-01-21 下午6.15.02](https://hackmd.io/_uploads/HJrhAw9KT.png)
![截圖 2024-01-21 下午6.23.11](https://hackmd.io/_uploads/Byn9g_5Yp.png)
- 根據 $[Eq.8]$ 推導，可以知道 
    - 我們想求的 $2D$ 投影後再減去質心的值
    - 就是計算出 $3D$ point 減掉質心、再經過 Affine transform

![截圖 2024-01-21 晚上9.36.17](https://hackmd.io/_uploads/SJT06qqF6.png)
- 可以理解為轉換 world reference system 座標

![截圖 2024-01-21 晚上9.37.16](https://hackmd.io/_uploads/SkKfC5cKp.png)
- 因為每個 camera 都有 $x, y$ 兩個方向，共 $2m$
- 又有 $n$ 個點
- 所以總共可以產生 $2m*n$ 個 data 的 matrix

![截圖 2024-01-21 晚上9.38.56](https://hackmd.io/_uploads/rk2dRqcK6.png)
- 此 matrix 也可以拆分、理解為 camera * points
- 根據幾何上的性質（$X$ 有 $x, y, z$ 三個方向），分解的兩個子 matrix 的 rank $=3$

![截圖 2024-01-21 晚上9.42.47](https://hackmd.io/_uploads/BJHPkj9tT.png)
- 分解的目標

![截圖 2024-01-21 晚上9.43.31](https://hackmd.io/_uploads/ryyqkoqtp.png)
- 利用 SVD 方式來拆分

![截圖 2024-01-21 晚上9.44.07](https://hackmd.io/_uploads/B1I2kj9tT.png)
![截圖 2024-01-21 晚上9.47.00](https://hackmd.io/_uploads/r1XwgsqFp.png)
- 因為剛剛知道 $A$ 與 $X$ 兩個 Matrix 的 $rank = 3$
- 所以我們只取部分的黃色部份來當作 estimate 結果

![截圖 2024-01-22 下午1.14.55](https://hackmd.io/_uploads/rJaRK_iFT.png)
- Affine ambiguity
- 但如果這時，我們針對 $M, S$ 分別乘上 $H, H^{-1}$
- 條件依然會成立
- 此一現象稱為 Affine ambiguity

![截圖 2024-01-22 下午1.18.38](https://hackmd.io/_uploads/Sk92cuiKT.png)
- 圖形上的觀點，可以看出兩張圖
- 他們在投影後的 $2D$ image 上的點會是一樣的
- 所以 $8m +3n-8$ DOF 中的 $8$ 就是因為此 ambiguity

### 5.3 Perspective SFM

![截圖 2024-01-22 下午1.23.48](https://hackmd.io/_uploads/S1bxndoFT.png)
- Perspective 的 $M$ 中的 data 變得更多
- 共 $11m+3n – 15$ DOF
    - 11：一個 camera $3*4 - 1$，共 $m$ 個 cameras
    - 3：一個 point $x, y, z$ 共 3 個值
    - 15：projective ambiguity

![截圖 2024-01-22 下午1.27.32](https://hackmd.io/_uploads/rkbCn_sY6.png)
- projective ambiguity 的圖示

![截圖 2024-01-22 下午1.28.42](https://hackmd.io/_uploads/BkvzT_oYp.png)
- 處理 the perspective ambiguity 的方式為 metric reconstruction，其中一個方式為 self-calibration

![截圖 2024-01-22 下午1.33.55](https://hackmd.io/_uploads/ByeLCOsKp.png)
- 現在介紹另外一種預測 SFM 的方式
- Algebraic approach

![截圖 2024-01-22 下午1.31.46](https://hackmd.io/_uploads/S1lCadoKT.png)
![截圖 2024-01-22 下午1.34.35](https://hackmd.io/_uploads/rJvdRdsta.png)
- 利用前面學過的 $2$ 個 view 的 $8$ point pairs 
- 去預測出 Fundamental matrix $F$

![截圖 2024-01-22 下午1.35.51](https://hackmd.io/_uploads/HyQpRdsYa.png)
![截圖 2024-01-22 下午1.54.38](https://hackmd.io/_uploads/SJimQKoFT.png)
![截圖 2024-01-22 下午1.55.02](https://hackmd.io/_uploads/BkgfBQKoYT.png)
- 由已知的 $F$，去得出 $[b_x]A$

![截圖 2024-01-22 下午1.56.18](https://hackmd.io/_uploads/HyCFmtiYa.png)
- 利用 SVD 求出 $b$

![截圖 2024-01-22 下午1.57.13](https://hackmd.io/_uploads/S14TXKjYT.png)
- 再求出 $A$
- 就可以知道 camera matrix $\tilde M_1, \tilde M_2$

![截圖 2024-01-22 下午1.59.17](https://hackmd.io/_uploads/rJ-BVYita.png)
![截圖 2024-01-22 下午1.59.31](https://hackmd.io/_uploads/rk1UVtsYp.png)
![截圖 2024-01-22 下午2.00.06](https://hackmd.io/_uploads/B1zdNYit6.png)
- 而 $b$ 其實就是 epipole

![截圖 2024-01-22 下午2.00.35](https://hackmd.io/_uploads/S1x9VtitT.png)
![截圖 2024-01-22 下午5.29.22](https://hackmd.io/_uploads/B1EKBhiFa.png)
- 有了 camera matrix $\tilde M_1, \tilde M_2$
- 就可以利用已知的 $x$，來預測出 $3D$ point $X$

![截圖 2024-01-22 下午5.40.07](https://hackmd.io/_uploads/SkvZ_3jtT.png)
- 剛剛都是兩個 view 的情況
- 在多個 view 時，就是做很多次的 2-view pairs
- 遇到不一致的 3D 點，$X$ 時
    - 可以使用第三種處理 SFM 的 method
    - **bundle adjustment**

![截圖 2024-01-22 下午5.59.16](https://hackmd.io/_uploads/H17Y2hsKp.png)


![截圖 2024-01-22 下午6.08.12](https://hackmd.io/_uploads/SyTqR3jtT.png)
- 在介紹 bundle adjustment 之前，先概述前面方式會遇到的問題
- **Factorization** 
    - 會需要 input 所有的資料，因此圖像不能遇到 occur 遮擋的情形，否則會出現 failure
- **Algebraic** 
    - 只適用在 2-view

![截圖 2024-01-22 下午6.15.20](https://hackmd.io/_uploads/SJ5BeTiFp.png)
- non-linear 的方式
- 就是去 minimize re-projection 的 error

![截圖 2024-01-22 下午6.25.27](https://hackmd.io/_uploads/Sk2oG6otT.png)
- minimize 的方式
    - 可以使用 Newton method
    - 或是使用 Levenberg-Marquardt Algorithm

![截圖 2024-01-22 下午6.52.38](https://hackmd.io/_uploads/rJFbtajYT.png)
- 可以克服另外兩個 method 的缺點
- 但如果初始狀態的參數太糟，computatioon cost 就會太大
- 因此我們可以先使用前面兩種方式的結果，來作為 Bundle adjustment 的初始參數，如此一來就可以解決 cost 太大的狀況

### 5.4 Self-calibration

![截圖 2024-01-22 晚上11.08.28](https://hackmd.io/_uploads/HJKeH-hFT.png)
![截圖 2024-01-22 晚上11.10.00](https://hackmd.io/_uploads/SyrUrZnYa.png)
- 為了處理 similarity 的問題
- 我們可以經過運算（較難跳過）來得出 $[Eq. 15]$ 的這個限制（也是利用  Bundle adjustment），進而解決
- 就只會剩下 similarity ambiguity 了（比例），而不會有奇形怪狀的 transformation 也符合 $2D$ image

### 5.5 Summary

![截圖 2024-01-22 晚上11.11.56](https://hackmd.io/_uploads/ryu6Bb2Fa.png)



## #參考資料
- [EE 6485 Computer Vision 計算機視覺](https://aliensunmin.github.io/teaching/cv2023/index.html)
