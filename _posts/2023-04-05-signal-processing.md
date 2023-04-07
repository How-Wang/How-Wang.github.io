---
layout: post
title: 訊號與系統
subtitle: 訊號與系統是指對訊號表示、轉換、運算等進行處理的過程，就是要把記錄在某種媒體上的訊號進行處理，以便抽取出有用資訊的過程，它是對訊號進行提取、轉換、分析、綜合等處理過程的統稱。
categories: 基礎科學
tags: [數學, 多媒體]
---

## 1. Basic Concepts

### 1.3 Classifications of Signals
- Continuous vs Discrete
    - continuous time signal $x(t)$
        - ![](https://i.imgur.com/tT6VgS2.png)
    - discrete time signal $x[n]$
        - 在特定時間上才有值，通常都為固定在 continuous-time 做 signal sampling 得出
        - signal is defined at particular instants(立即) of time
        - 值仍是 continuous
        - 需要做 quantization 完才會是 discrete signal 表值與時間皆為 discrete
        - ![](https://i.imgur.com/e8lNgHH.png)
        - discrete time 表示法
            - $x[k] = x[kT]$
            - $x[k]$ 表第 k 個取樣
            - $x[kT]$ 表第 kT 時間取樣
            - $x[kT]$ 的表示法比較好
                - 可以直接看出時間點
                - 未來也可以與其他數據結合搭配，所以時間單位再結合時，也需要校正
- Periodic and Nonperiodic Signal
    - periodic continuous $x(t) = x(t+nT)$
        - ![](https://i.imgur.com/wwpx8OK.png)
    - periodic discrete $x[n] = x[n+N]$
        - ![](https://i.imgur.com/Bw1eSTN.png)
- <span style="background-color: #e2f8f0; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">【補充】Euler’s Identities</span>
    - $e^{j\theta} = cos\theta + jsin\theta$
    - $e^{-j\theta} = cos\theta - jsin\theta$
    - ![](https://i.imgur.com/bS3TNQI.png)
    - ![](https://i.imgur.com/BqUSNvD.png)
- An analog signal vs A digital signal
    - An analog is a continuous time signal in which the variation with time is analogous (or proportional) 時間與值都是連續的
    - is a discrete time signal that can have a **finite number** of values (usually binary).時間與值都不是連續的
        - 需要 sampling and quantization
- Energy vs Power Signals
    - ![](https://i.imgur.com/JERkkHR.png)
    - A signal $x(t)$ or $x[n]$ is an **energy signal** if and only if `代E公式會介於0到無窮大` and `代P公式會等於 0`
    - A signal $x(t)$ or $x[n]$ is a **power signal** if and only if `代P公式會介於0到無窮大` and`代E公式會等於無窮大`
    - <span style="background-color: #ffd7c1; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">所以當題目給一個 $x(t)$ 或是 $x[n]$ 時，就直接帶 $E$ 或 $P$ 的公式，看哪一個會介於0到無窮大之間</span>
- Even vs Odd smmetry
    - even：$x(t) = x(-t)$
    - odd：$x(t) = -x(-t)$
    - 每一個 signal 都可以被分為 even part 跟 odd part
        - $x(t) = x_e(t) + x_o(t)$
        - $x_e(t) = \frac{1}{2}[x(t) + x(-t)]$（把odd part 部分給消掉）
        - $x_o(t) = \frac{1}{2}[x(t) - x(-t)]$（把even part 部分給消掉）

### 1.4 Basic continuous-time signals
- **Unit impulse function（delta function）**
    - ![](https://i.imgur.com/kxacMTT.png)
    - $\int_{0-}^{0+} \delta(t) \,dt = 1$
    - sampling
        - ![](https://i.imgur.com/ICQQwCV.png)
- **Unit step function**
    - ![](https://i.imgur.com/glbaOYT.png)
- **Unit ramp function**
    - ![](https://i.imgur.com/m7ixblY.png)
- <span style="background-color: #c8d8df; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">3 種函數關係</span>
    - $r(t)$ 微分變 $u(t)$, $u(t)$ 微分變 $\delta(t)$
    - $\delta(t)$ 積分變 $u(t)$, $u(t)$ 積分變 $r(t)$
- 其他延伸的 function
    - <span style="background-color: #e2f8f0; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">**Rectangular Pulse Function**![](https://i.imgur.com/8i9mFVt.png)</span>
    - **Triangular Pulse Function**
        - ![](https://i.imgur.com/Yzc7ZcP.png)

### 1.5 Basic discrete-time signals
- **Unit impulse sequence**
    - ![](https://i.imgur.com/FEXZ7TO.png)
- **Unit step sequence**
    - ![](https://i.imgur.com/IDIcnrh.png)
- **Unit ramp sequence**
    - ![](https://i.imgur.com/8YMIW2n.png)
- 三者相對關係
    - ![](https://i.imgur.com/QS80vza.png)
    - ![](https://i.imgur.com/hz5nJbq.png)
- 其他函數圖形
    - **Sinusoidal sequence**
        - ![](https://i.imgur.com/fSA0Eum.png)
    - **Exponential Sequence**
        - $x[n] = Ae^{-anT} = A\alpha^n, \alpha = e^{-aT}$
        - ![](https://i.imgur.com/uhHaVSt.png)

### 1.6 Basic operations on signals
- **Time Reversal**
    - ![](https://i.imgur.com/8o9aeby.png)
- **Time Scaling**
    - ![](https://i.imgur.com/y7EPJkJ.png)
- **Time Shifting**
    - ![](https://i.imgur.com/Q87hmFp.png)
- **Amplitude Transformations**
    - ![](https://i.imgur.com/2ycEkPU.png)
    - ![](https://i.imgur.com/xOSVgfR.png)

### 1.7 Classification of systems
- ***Continuous Time and Discrete Time Systems***
    - ![](https://i.imgur.com/5DZX0MA.png)
- ***Causal and Noncausal Systems***
    - A causal system is one whose present response does **not depend on the future values** of the input
- ***Linear and Nonlinear Systems***
    - Homogeneity + Additivity
    - ![](https://i.imgur.com/fvMNXJq.png)
- ***Time Varying and Time Invariant Systems***
    - vary：to change or cause something to change in amount or level, especially from one occasion to another
    - ![](https://i.imgur.com/XcPJ1QG.png)
    - time-invariant
        - ![](https://i.imgur.com/kzRcESm.png)
    - time-varying
        - ![](https://i.imgur.com/1aF9MzM.png)
- ***Systems with and without Memory***
    - When the output of a system **depends on the past or future input**, the system is said to have a memory.

## 2. Convolution
- [But what is a convolution?](https://www.youtube.com/watch?v=KuXjwB4LzSA)

### 2.2 Impulse response
> The impulse response to an LTI (linear, time invariant) system is **`the output of the system to a unit impulse function`**.
- Impulse response（green part）
    - ![](https://i.imgur.com/uhD8b8c.png)

### 2.3 Convolution integral
- The convolution of two signals $x(t)$ and $h(t)$ is usually written in terms of the operator $*$ as
    - ![](https://i.imgur.com/93R2cLh.png)
    - <span style="background-color: #ffd7c1; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">我們 input signal $x(t)$ 與 impulse function $\delta(t)$，經過 LTI 系統的 transform，我們可以得到一個 impulse response $h(t)$，接著 $x(t)$ 再與 $h(t)$ 做 convolution 後，就可以得到 output $y(t)$</span>
    - 若 $x(t) = 0$ for $t < 0$, 且 the system is causal, $h(t) = 0$ for $t < 0$（此處的 $\tau$ 為變數）
        - 則![](https://i.imgur.com/aTrR7we.png)
        - 或是也可寫成 $y(t) = x(t)*h(t) = \int_{0}^{t}x(t-\tau)h(\tau)d\tau$

### 2.4 Graphical convolution
- 使用到前方提過的函數技巧
    ![](https://i.imgur.com/KOtJ9m4.png)
- 需要分段討論的範例
    - ![](https://i.imgur.com/T2eyDqx.png)
    - 根據定義可列
    - ![](https://i.imgur.com/4CMS8ZT.png)

### 2.5 Block diagram representation for continuous
![](https://i.imgur.com/vg5LsPg.png)

### 2.6 Discrete-time convolution
- 定義
    - `2.2、2.3 的離散版本`
    - ![](https://i.imgur.com/5auesKV.png)
- **範例** Find $y[n] = x[n]*h[n]$ ![](https://i.imgur.com/6z8Lilc.png)
    - **`法一分析`** ![](https://i.imgur.com/Sv1H1JX.png)
    - **`法二圖解`** ![](https://i.imgur.com/hvaWvoe.png)
        - <span style="background-color: #e2f8f0; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">意義上為，將 $h(\tau)$ 先做 mirror(對y軸對稱)，再分別向右平移 $0\sim t$、每次都與 $x(\tau)$ 相乘，最後再合成。
        </span>
        - 推廣在 $matlab$ 的運算方式![](https://i.imgur.com/8B6oSyZ.png)

### 2.7 Block diagram realization for discrete
![](https://i.imgur.com/aH2GEom.png)
- **範例** Let $x[n] = \{3, 0, 2, 6\}$ and $y[n] = \{6, 12, 25, 20, 38, 42\}$. Find $h[n]$
    - 法一長除法：![](https://i.imgur.com/fdn1g2h.png)![](https://i.imgur.com/doQOWDs.png)
    - 法二遞迴：![](https://i.imgur.com/3VPhQne.png)

## 3. The Laplace Transform

### 3.1 Introduction
- Laplace Transform 是將 linear system 轉換為 **`frequency-domain`** 的表達方式
- 能夠將常微分方程式（ordinary differential equations）轉為代數方程（algebra equations），以利於運算
- 讓 convolution 成為簡單的乘法
- 在 continuous-time LTI (Linear Time-invariant) system 產生 transfer function

### 3.2 Definition of laplace transform
- Laplace Transform：![](https://i.imgur.com/Dv6L0cP.png)
- Inverse Laplace Transform：![](https://i.imgur.com/FVRHlus.png)
- Laplace transformable：![](https://i.imgur.com/0eKJP0t.png)
    - Region of Convergence(ROC)：Laplace transform 就是會收斂的範圍 $Re(s) = σ >σ_c$![](https://i.imgur.com/nGTGGYn.png)
    - example：![](https://i.imgur.com/MLD07Tt.png)![](https://i.imgur.com/27mzcrB.png)![](https://i.imgur.com/pxDEEGh.png)![](https://i.imgur.com/rIicIeL.png)

### 3.3 Properties of the laplace transform
- ***Linearity***：![](https://i.imgur.com/klec6Cg.png)
    - ![](https://i.imgur.com/0eLU9zm.png)
- ***Scaling***：![](https://i.imgur.com/KLsjMi5.png)
    - ![](https://i.imgur.com/5ocdoy8.png)
- ***Time Shifting***：![](https://i.imgur.com/B99c37h.png)
    - ![](https://i.imgur.com/mV6TsNe.png)
- ***Frequency Shifting***：![](https://i.imgur.com/GC6Lczw.png)
    - ![](https://i.imgur.com/56e2J4X.png)
- ***Time Differentiation***：![](https://i.imgur.com/uvyQIBZ.png)
    - ![](https://i.imgur.com/wFVRE2y.png)
- ***Time Convolution***：![](https://i.imgur.com/oTnTLn4.png)
    - ![](https://i.imgur.com/Ed82dE1.png)
- ***Time Integration***：![](https://i.imgur.com/eX79Cve.png)
    - ![](https://i.imgur.com/dtqhXzm.png)
- Initial and Final values：已知![](https://i.imgur.com/uvyQIBZ.png)，當![](https://i.imgur.com/z733Wow.png)![](https://i.imgur.com/1hbh2QF.png)
- all Properties：
    - ![](https://i.imgur.com/dJEslYP.png)
    - ![](https://i.imgur.com/j2AAxrL.png)


### 3.4 The inverse laplace transform
- ***Definition***：![](https://i.imgur.com/kCAjv4p.png)
- ***Simple Poles***：
    - 已知：<span style="background-color: #c8d8df; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">我們已知![](https://i.imgur.com/pxDEEGh.png)，故在 Simple poles 可以直接從 $X(s)$ 回推 $x(t)$</span>
    - formate：![](https://i.imgur.com/cUbk2t0.png)
- ***Repeated Poles***
    - 已知：<span style="background-color: #ffd7c1; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">因為 $(s+p)^n$ 出現，因此需要 **`微分`** 來找 $k$，且![](https://i.imgur.com/ZtJAEUu.png)
</span>
    - format：![](https://i.imgur.com/KXc6jnj.png)
    - 補充：當看到 $L^{-1}[\frac{1}{s^2}] = t$ 也是用此 pole
- ***Complex Poles***：
    - 已知：<span style="background-color: #e2f8f0; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;"> ***Frequency Shifting*** ![](https://i.imgur.com/UaEfH5N.png)
、![](https://i.imgur.com/UcX0v4P.png)故 Complex Poles 可以應用</span>
    - formate：**先從分母找 $\alpha$、$\beta$，再調整分子看 A B**![](https://i.imgur.com/cw3KFQM.png)
    - 延伸：$sin$ 跟 $cos$ 可以合併![](https://i.imgur.com/XIJsLa3.png)

### 3.5 Transfer function
- 定義：<span style="background-color: #ffd7c1; display: block; padding: 2% 2% 0.5% 2%; border-radius: 15px;">$H(s)$為輸出結果 $Y(s)$ 與輸入結果 $X(s)$ 的比值，如此一來，再利用 Inverse Laplace Transfer，就可以輕鬆找到 $h(t)$</span>
    - ![](https://i.imgur.com/OXWPVfj.png)
- ***Cascade connection***：![](https://i.imgur.com/nPuj0EC.png)
- ***Parrallel interconnection***：![](https://i.imgur.com/3pc3rYq.png)
- ***Feedback interconnection***：![](https://i.imgur.com/Az2MVQo.png)

### 3.6 Integro-Differential equations
![](https://i.imgur.com/z22FJPc.png)

## 4. Fourier Series
## 5. Fourier Transform
## 6. Discrete Fourier Transform
## 7. z-Transform
