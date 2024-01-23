---
layout: post
title: 社群網路
subtitle: realize the complex “connectedness” of modern society
categories: 基礎科學
tags: [網路]
---

## 1. Overview
- Graph Theory and Social Network
    - 2.Graph
    - 3.Strong and Weak Ties
    - 4.Networks in Their Surrounding Contexts
    - 5.Positive and Negative Relations
- Game theory
    - 6.Games
    - 9.Auctions
- Markets and Strategic Interaction in Network
    - 10.Matching Markets
    - 12.Bargaining and Power in Networks
- Network Dynamics: Population Models
    - 16.Information Cascade
    - 17.Network Effects
    - 18.Power Laws and Rich-get-richer Phenomena
- Network Dynamics: Stuctural Models
    - 19.Cascading Behavior in Networks
    - 20.The small-world phenomenon
    - 21.Epidemics

## 2. Graph

### 2.1 Basic definitions
- [圖形理論 筆記](https://hackmd.io/aKMDyTdyQeao-xlkrwhugw?view)
- A graph is way of **specifying relationships** among a collection of items
    - ![](https://hackmd.io/_uploads/ByZR5DZka.png)
    - Nodes
    - Edges
        - The number of edges connecting to a node is called the degree of that node
    - Adjaceny Matrix

### 2.2 Paths and connectivity
- Path = Simple path
- Directed and Undirected
- Coponent
- A **giant component** is a connected component that contains a significant fraction of all nodes in the network
    - 有兩個 giant component 的機率為0
    > ![](https://hackmd.io/_uploads/BJAiWdW16.png)
    > ![](https://hackmd.io/_uploads/HJXaWd-1T.png)

### 2.3 Distance and breadth-first search
- **Distance** between two nodes is defined as the length of the shortest path between them
    - **Breath-first search**
        - ![](https://hackmd.io/_uploads/Byw_GdW16.png)
        - ![](https://hackmd.io/_uploads/B1NAfdbkp.png)
:::success
🌎 **Small world property**
- 世界隨機選兩個人的關聯 distance，雖然有數億人，但實際 distance 很短。
:::
- Stanley Milgram，利用寄信實驗
    - 認識就直接寄給收件人
    - 不認識就寄給「你認為會認識收件人者」
    - 結果平均為 6 步
        - ![](https://hackmd.io/_uploads/By62E_bkT.png)
        - ![](https://hackmd.io/_uploads/BJpkBdbyT.png)
- Small-world phenomenon in **other social networks**
    - `Microsoft Instant Messenger accounts`
        - 彼此相互在一個月內，有沒有傳訊息
        - 240 million user
        - ![](https://hackmd.io/_uploads/ryFez3LJp.png)
        - 中位數為 7
    - `Mathematician collaboration networks`
        - 數學家間是否有合寫過論文？
        - 數十萬筆
        - ![](https://hackmd.io/_uploads/SJOnfhIyp.png)
        - Erdos number
            - 大家距離數學家 Erdos 的長度(Erdos 發表論文量最高共 1500 篇、與 500 人合寫過論文、closeness centrality 最高)
            - 大部分皆為 4、5
    - `Kevin Bacon and the movie-star network`
        - Kevin Bacon 在中間

## 3. Strong and Weak Ties
- Ph.D. thesis of Mark Granovetter
    - 訪問人如何獲得新的工作，消息來源為 Strong 或是 Weak Ties (From friends or acquaintances)
    - 結果出乎意料，為關係薄弱的人 acquatintances 點頭之交 較多
- 在這一章 Through **the study of job-seeking**, we study the structure of social networks
    - ![](https://hackmd.io/_uploads/ryGaDhIJp.png)

### 3.1 Triadic closure
- ![](https://hackmd.io/_uploads/BJNKunIyT.png)
- social network 容易形成封閉三角形的結構，就是 Triadic closure
- **Clustering coefficient** measures of the abundance of triangles in a social network，用來描述三角形的多寡
- Reason
    - Opportunity for two people to meet if they have a common friend
    - Trust
    - Incentive
### 3.2 The strength of weak ties
- 好的工作很 scarce 稀有
    - 下圖 $A, B$ 之間的關係
- **Bridges** are edges, deleting which would causes the network to break into two disconnecting components，但這樣太嚴格了
    - ![](https://hackmd.io/_uploads/Skp2j2Iy6.png)
- **Local bridges** 
    - Whose end points have no common friends
    - and Span of a local bridge when deleting is $≥ 3$ between the two end points，線剪斷的時候 span 要 $≥ 3$
        - In the example figure, the span of local bridge when delete $A-B$ is $4$
    - ![](https://hackmd.io/_uploads/ByyNsn8ka.png)
    - Property
        - **Scarce** information such as good jobs come from local bridges
        - Local bridges are **usually weak** ties
- **Strong triadic closure** property
    - ![](https://hackmd.io/_uploads/BkAVeaUy6.png)
- $A-B$ 是 Strong 的話，STC、Local Bridge 不能同時滿足
    - ![](https://hackmd.io/_uploads/HkqVZpLJa.png)
- Network 常見的結構
    - ![](https://hackmd.io/_uploads/Syrj-p8JT.png)
### 3.3 The strength and network structure in large-scale data
- Onnela 使用 who-talks-to-whom 的 network
    - edge 的強度用通話時間來表達
    - local bridge 用 **Neighborhood overlap** 來定義範圍 ![](https://hackmd.io/_uploads/HypoMTIkT.png)![](https://hackmd.io/_uploads/BJ69maI1T.png)
- **Local bridges vs. neighborhood overlap**
    - edge 強度、local bridge 彈性變大（不再是單純的二分法，而是數值表達）
    - ![](https://hackmd.io/_uploads/rkPKVpLka.png)
- Onnela 社群圖，一個一個「較 weak」的 edge 拿掉，比一個一個拿掉「較 strong」，Network 還快解體。
### 3.5 Closure, structural holes, and social capital
- 討論社群圖的內部點的角色，優勢劣勢
- ![](https://hackmd.io/_uploads/HyGnS68kT.png)
    - 比較 AB 關係
    - **Embeddedness**
        - Embeddedness of an edge is defined to be the number of common neighbors shared by the two endpoints，就是邊上兩個點的共同好友數
        - A-B edge has an embeddednesss of 2
        - **Local bridges** 是 zero embeddedness
    - **Tightly-knit groups**
        - All A’s edges have significant embeddedness
        - A 關係比較完善穩固，不敢欺騙背叛，有嚇阻力
        - 但「同值性」太高，所以稀缺工作機會介紹，反而出現的機率比較低（大家都想幫忙，但都沒用...）
    - **zero Embeddedness**
        - 與 A 相反
        - B 的利益跟他人不完全一致
        - 行爲比較複雜，會受多個 group 影響
        - Creativity 比較高
        - 獲得的新資訊速度比較快
        - **Structural holes** 比較多
            - ![](https://hackmd.io/_uploads/SJDaOaI1T.png)

## 4. Networks in Their Surrounding Contexts
- **Surrounding contexts**
    - 節點的「個人特質」描述
    - 種族、性別、財富等等
### 4.1 Homophily
- **Homophily**
    - 相似性 Similarity
    - ![](https://hackmd.io/_uploads/r10Dvj9kp.png)
:::info
- 成為 connection 的因素
    - ![](https://hackmd.io/_uploads/SyYz_s5yT.png)
    1. Triadic closure 
        - provides an intrinsic tendency for the link B-C to form
    2. Homophily 
        - suggests that B and C are similar to A in a number of dimensions due to the friendship A-B and A-C
:::
- **Homophily Test**
    - 判斷一個圖形是否有 Homophily（男生傾向跟男生當朋友，女生亦然）
        > ![](https://hackmd.io/_uploads/ryi_ts9ka.png)
        > ![](https://hackmd.io/_uploads/S1qXFj51a.png)

### 4.2 Mechanisms underlying homophily: selection and social influence
- **Selection**
    - 根據 similarity characteristic 來選擇 connection 對象
- **Mutable and Immutable**
    - Mutable 可更改
        - 行為
        - 教育
    - Immutable 不可更改
        - 種族
- **Socialization and social influence**
    - people may modify their behaviors to align with the behaviors of their friends 的過程
- **Longitudinal studies**
    - 我們怎麼知道他們是因為相似度高變成朋友，還是因為變成朋友才相似度高
    - 用長時間追蹤，tracking a social network over a long time，就是 Longitudinal studies
    - Cohen and Kandel suggested that both effects are present in the data, while social selection（選擇） is comparable (***sometimes greater than***) the effect of social influence（影響）

### 4.3 Affiliation
- So far, surrounding contexts have been viewed as **“outside**” of the network
    - 把 outside context 放進網路，就是 Affiliation
    - social activities 又稱作 foci (focal points)
- Social-affiliation networks
    - ![](https://hackmd.io/_uploads/S1AnRiqkp.png)
- Bipartite 版本
    - ![](https://hackmd.io/_uploads/SJK3Tj51a.png)
    - 人跟人之間沒連結，社團跟社團之間也無
- 彼此之間的關聯性
    - ![](https://hackmd.io/_uploads/rywgJ2qkp.png)

### 4.4 Tracking link formation in online data
- ![](https://hackmd.io/_uploads/H1r2sJex6.png)
    - For each 𝑘, identify all pairs of nodes 擁有k個共同好友 in the first snapshot, 但不相連
    - Define $𝑇(𝑘)$ to be the fraction of these pairs that have formed an edge(變成朋友了) by the time of the second snapshot
- Kossinets and Watts 實驗
    - ![](https://hackmd.io/_uploads/rJUz6kgxa.png)
    - $T_{baseline} = 1 - (1-p)^k$
        - $p$ 為一對三角關係不成為朋友的機率
        - 共有 $k$ 組
- Quantifying the interplay between selection and social influence
    - Crandell 利用維基百科的編輯者朋友關係
    - ![](https://hackmd.io/_uploads/S1Yi1xllp.png)
    - 成為變成朋友前後的相似性
        - 都很高
    - 下方藍色為隨機取樣
        - 低

### 4.5 A spatial model of segregation
- Mobius and Rosenblat 研究美國芝加哥黑人住宅分部
    - ![](https://hackmd.io/_uploads/BJy7xegep.png)
    - segregation 隔離現象
- Geometric grid 
    - ![](https://hackmd.io/_uploads/H1em-lgea.png)
- The dynamics of movement
    - ![](https://hackmd.io/_uploads/HJ_rZexxT.png)
    - 標 star 的想要搬家
    - X 會想要跟 X 待在一起，O 亦然
    - End up with segregation qualitatively
    - ![](https://hackmd.io/_uploads/SygImeee6.png)
    - ![](https://hackmd.io/_uploads/HJPPmgle6.png)

## 5. Positive and Negative Relationships
### 5.1 Structurally balance
- ![](https://hackmd.io/_uploads/Sy0SExlxp.png)
    - 除了有好朋友 $(+)$ 的關係，也有敵人的關係 $(-)$
    - $(b)$
        - 可能A會聽信另一個人的意見，跟一人決裂
        - 也有可能A作東家，三者都成為好朋友
        - 不穩定
    - $(c)$
        - 三國演義穩定


### 5.2 Characterizing a structurally balanced network
- A complete (fully connected) structurally graph
    - example：![](https://hackmd.io/_uploads/S1Kv9xeea.png)
    - Balance Theorem
        - the nodes 可以被分成兩群, 𝑋 and 𝑌, such that every pair of nodes in 𝑋 都是朋友, every pair of nodes in 𝑌 也一樣, and everyone in 𝑋 is 敵人 of everyone in 𝑌
        - ![](https://hackmd.io/_uploads/rJJP9gxgp.png)
    - proof：如果有一點 A 跟 BC 是朋友、跟 DE 是敵人，為了維持 balance，他們彼此的關係會產生 clique![](https://hackmd.io/_uploads/Hk1N2glgT.png)
    

### 5.5 Advanced materials: generalizing the definition of structural balance
- Theory on structural balance
    - Networks containing **only cycles with even numbers of minus signs** are said to be structurally balanced, or balanced。就是 cyle 負號的個數是偶數
    - A network is said to be **clusterable** if the set of vertices 𝐸 can be partitioned into two disjoint sets 𝑋 and 𝑌...，就是上述的規定
    - Harary’s balance theorem
        - A signed network is **balanced if and only if** the **network is clusterable** or the network contains only positive edges 兩者相同
    - ![](https://hackmd.io/_uploads/HkzF0xelp.png)

## 6. Games
### 6.1 What is a game?
- 大部分的社會行為 involve with decision making or optimization
- Game theory 設計去處理 situations in which the outcomes of a person’s decisions depend not just 他們如何自己選擇, but also **on the choices of made by other people** with whom they interact
    - John Forbes Nash 提出
- example
    - > If you study, your expected grade is a 92, while if you don’t study, your expected grade is an 80. For the presentation you are working jointly with a partner. If both you and your partner prepare for the presentation, you will get a 100. If just one of you prepares (and the other doesn’t), you will get a 92. If neither of you prepares, your expected grade is 84
    - ![](https://hackmd.io/_uploads/r1FhG-xla.png)
    - > 表格內的結果，是各自兩個分數的平均



### 6.2 Reasoning about behavior in a game
- Everything that a player cares about is summarized in the payoffs
    - 只在乎 payoffs 的值
    - 所以心理因素也要 **量化** 放入 payoffs 考慮
- This model of individual behavior is called **rationality**
    - 都是理性的

### 6.3 Best responses and dominant strategies
- ![](https://hackmd.io/_uploads/r1FhG-xla.png)
    - 在對方選擇 Presentation 時，我選 Exam 92 較 Presentation 90 高
    - 在對方選擇 Exam 時，我選 Exam 88 也較 Presentation 86 來的高
    - 選 Exam 就是 Dominant strategies
    - 儘管對方知道你願意犧牲做 Presentation，對方還是會選擇 Exam 來拿到 92，你比一開始拿到的 88 更低
    - :::info
        We say that a **dominant strategy** for player 1 is a strategy that is a best response to every strategy of player 2
        :::
- The prisoner's delemma
    - ![upload_a97796384f890126762615c3db38a46b.png](https://hackmd.io/_uploads/BytEljI7a.png)


- Let $𝑆$ be a strategy chosen by player $1$, and $𝑇$ be a strategy chosen by player $2$
    - Let $𝑃_1(𝑆,𝑇)$ be the payoff to player $1$ as this pair of strategies are used
    - Similarly, let $𝑃_2(𝑆,𝑇)$ be the payoff to player $2$
    - ![](https://hackmd.io/_uploads/Hy4WA7Fx6.png)
- Strategy 𝑆 of Player 1 is a **strict** best response to a strategy 𝑇 for Player 2, if the inequality is strict
    - ![](https://hackmd.io/_uploads/BJFT0QYe6.png)
- 只有一個人有 dominent strategy，另一個人沒有
    - ![](https://hackmd.io/_uploads/HyrC1EYxT.png)
- 兩個人都沒有 dominent strategy
    - ![](https://hackmd.io/_uploads/SyVtBVYlp.png)

### 6.4 Nash equilibrium
- ==best responses to each other==
- We say that this pair of strategies (S,T) is a Nash equilibrium if S and T are best responses to each other
- 兩個人都沒有 dominent strategy
    - ![](https://hackmd.io/_uploads/SyVtBVYlp.png)
    - It can be checked that (A,A) is the only Nash equilibrium of this game

### 6.5 Multiple Nash equilibria: coordination games
- 不只一個 Nash equilibria
    - 彼此要先規定討論
    - 用外在因素決定
    - ![](https://hackmd.io/_uploads/ryH0D4Yep.png)
    - ![](https://hackmd.io/_uploads/r1nOFEtl6.png)
        - 台灣統一開右邊
        - 英國開左邊
- Variations: **unbalanced** coordination game
    - ![](https://hackmd.io/_uploads/rylst4Yg6.png)
    - 也是一樣 coordinate 用外在因素決定
- Variations: **battle of the sexes game**
    - ![](https://hackmd.io/_uploads/ryrb9NYx6.png)
    - 也是一樣 coordinate 用外在因素決定
- Variations: **mis-coordination** games
    - ![](https://hackmd.io/_uploads/HyoIqVYe6.png)
    - 也是一樣 coordinate 用外在因素決定

### 6.6 Multiple Nash equilibria: the Hawk-dove game
- ![](https://hackmd.io/_uploads/rkIMsNKg6.png)
    - 反斜對角是 Nash
    - 正斜對角不是

### 6.7 Mixed strategies
- Mixed
    - :::info
        :bulb: 如果只考慮 pure strategies(玩家一定只會選一個選項)，沒有 Nash equilibria 的情況
        We will enlarge the set of strategies，加入機率，to include randomized strategies（隨機策略） called Mixed strategies
        :::
    - 而 $p$、$q$ 的選擇是什麼呢？
- An example – matching pennies game
    - The payoffs sum to 0 in every outcome
        - Zero-sum games
    - 丟躑銅板
    - ![](https://hackmd.io/_uploads/Sy6Vifax6.png)
        - Player 1 丟出
            - 頭是 $p$
            - 背是 $1-p$
        - Player 2 丟出
            - 頭是 $q$
            - 背是 $1-q$
        - Player 1 
            - 選 H 的期望值 $(−1)𝑞+(1)(1−𝑞)=1−2𝑞$
            - 選 T 的期望值 $(1)𝑞+(−1)(1−𝑞)=2𝑞−1$
            - :::success
                :100: 如果兩者不相等，就對 Player 1 比較好，那 p 就會是 1 或 0，就回到 Pure strategy，那就不是 Nash equilibrium，不行
                :::
            - 故 $1−2𝑞=2𝑞−1⟹𝑞=1/2$
            - The pair of mixed strategies $(𝑝,𝑞)=(1/2, 1/2)$ is the only possibility for a Nash equilibrium
            - *Indifference is a central principle behind the computation of mixed strategy equilibria when there are no equilibria involving with pure strategies*
- Another example – rock, scissors, paper game
    - ![](https://hackmd.io/_uploads/ryZiaVYl6.png)
### 6.8 Mixed strategies: examples and empirical analysis
- The run-pass game – American football
    - ![](https://hackmd.io/_uploads/rkJVzXTgT.png)
    - ![](https://hackmd.io/_uploads/SyFGemTxa.png)
    - Offence
        - Pass：$(0)(𝑞)+(10)(1−𝑞)=10−10𝑞$
        - Run：$(5)(𝑞)+(0)(1−𝑞)=5𝑞$
        - 兩者必須相等 To make the offense indifferent between its two strategies, the defense should choose $𝑞=2/3$
    - Defense
        - Pass：$(0)(𝑝)+(−5)(1−𝑝)=5𝑝−5$
        - Run： $(−10)(𝑝)+(0)(1−𝑝)=−10𝑝$
        - To make the offense indifferent between its two strategies, the defense should choose $𝑝=1/3$
- The penalty-kick game
    - ![](https://hackmd.io/_uploads/HkIFzX6xa.png)

### 6.9 Pareto optimality and social optimality
- Pareto optimality
    - A strategy profile is not optimal if there is an alternate profile that makes at least one player better off without harming any player
        - ==如果有讓兩人都更好的，就不是 optimal，其他都是==
    - ![](https://hackmd.io/_uploads/rkCEUULZp.png)
    - 左上正對角 vs 右下正對角
        - 兩個值一個 strickly better 然後另外一個並不差
        - 所以左上是 Pareto optimal
    - 斜對角也找不到更好的 Pareto 故各自也是 Pareto optimal
- Social optimal
    - 就是加起來最大的值

### 6.10 Advanced material: dominated strategies and dynamic games
- 每個 player 都有一個 payoff function $𝑃_𝑖$ that maps outcomes of the game to a numerical payoff for 𝑖 $𝑃_𝑖 (𝑆_1,𝑆_2, ⋯,𝑆_𝑛)$ for player 𝑖 when outcome consists of $(𝑆_1,𝑆_2, ⋯,𝑆_𝑛)$ 
- 我們會稱 strategy $𝑆_𝑖$ 是 **best respons**e by player 𝑖 去選擇一個策略 $(𝑆_1,𝑆_2,⋯,𝑆_{𝑖−1},𝑆_{𝑖+1},⋯,𝑆_𝑛)$ by all the other players if $𝑃_𝑖 (𝑆_1,𝑆_2,⋯, 𝑆_{𝑖−1}, 𝑆_𝑖, 𝑆_{𝑖+1}, ⋯, 𝑆_𝑛 )≥𝑃_𝑖 (𝑆_1,𝑆_2,⋯, 𝑆_{𝑖−1},𝑆_𝑖\prime, 𝑆_{𝑖+1}, ⋯, 𝑆_𝑛)$ for 所有可能的策略 $𝑆_𝑖\prime$  available to player $𝑖$
- A strategy is **strictly dominated** if there is some other strategy available to the same player that produces a strictly higher payoff in response to every choice of strategies by the other players
- **Facility location game**
    - 蓋店家拉客人
        - ![](https://hackmd.io/_uploads/Bki2j8I-6.png)
    - Reduction of the facility location game
        - ![](https://hackmd.io/_uploads/SyECsI8Wp.png)
        - F 跟 A 一定不是 nash，先移除
        - 發現 C, D 是 dominant strategy
- **Weakly dominated strategies**
    - 大於等於即可，不一定要大於
    - ![](https://hackmd.io/_uploads/rJ4_kwLWT.png)
- **Dynamic games**
    - example
        - ![](https://hackmd.io/_uploads/B1_liqsWp.png)
    - Game tree
        - ![](https://hackmd.io/_uploads/SkFNociZT.png)
    - Game 是由上往下進行，分析則是由下往上
        - player 2 一定會跟 player 1 選相反的
        - player 1 知道 player 2 會跟自己選相反的，故 player 1 選 A payoff 比較高
- **Subgame perfect equilibrium**
    - ![](https://hackmd.io/_uploads/ByEl7ssZp.png)
    - ![](https://hackmd.io/_uploads/BkKfmssb6.png)
    - player 2 在 
        - player 1 選擇 Enter 的情況會，cooperate
    - player 1 選擇 enter payoff 較高

## 9. Auctions
- 拍賣
### 9.1 Types of auctions
- 一個賣家多個買家
    - 網路拍賣會
- 一個買家多個賣家
    - 清大要換電纜
- Four type
    - Ascending-bid auctions (also called English auctions)
        - 升價競標
        - 錢超過就退
    - Descending-bid auctions (also called Dutch auctions)
        - 降價競標
        - 有人買就賣
    - First-price sealed-bid auctions
        - 寫小紙條
        - 得標者付自己寫的錢
    - Second-price sealed-bid auctions (also called Vickrey auctions)
        - 寫小紙條
        - 得標者付第二高者的錢

### 9.2 When are auction appropriate?
- ![](https://hackmd.io/_uploads/S1yohisW6.png)
- **買家賣家都賺**
### 9.3 Relationships between different auction formats
- 在數學上 Descending-bid = first-price auctions
    - ![](https://hackmd.io/_uploads/SJFm6ijbp.png)
    - 最高的賣
- 在數學上 Ascending-bid = second-price auctions
    - ![](https://hackmd.io/_uploads/S1CI6oj-T.png)
    - 覺得太貴的退出
    - 留下最後一個人買
- 為什麼有賣家要使用 second-price auction?、賺的錢比較少？
    - 不會
    - 因為買家的策略也會改變
### 9.4 Second-price auctions
- ![](https://hackmd.io/_uploads/HJM_yhoWp.png)
    - 認為價值 $v_i$ 多少，出價 $b_i$ 就多少
    - 如果不是得標者
        - payoff：$0$
    - 是得標者
        - second-price bid：$b_j$
        - payoff：$v_i - b_j$
- ![](https://hackmd.io/_uploads/rkJoeqyGp.png)
    - 出比較高價 $b_i\prime$
        - 如果 $b_i\prime$ 以上有人出價
            - payoff 跟 $b_i$ 一樣 $0$
        - 如果 $b_i$ 與 $b_i\prime$ 之間有人出價 $b_j$
            - 那 payoff 為 $v_i - b_j \leq 0$，虧
        - $b_i$ 與 $b_i\prime$ 之間沒有人出價
            - payoff 跟 $b_i$ 一樣 $v_i - b_j$
    - 出比較低價 $b_i\prime\prime$
        - 如果 $b_i$ 以上有人出價
            - payoff 跟 $b_i$ 一樣 $0$
        - 如果 $b_i$ 與 $b_i\prime\prime$ 之間有人出價 $b_k$
            - payoff 原本是 $v_i - b_k > 0$
            - 現在 payoff 為 $0$，虧
        - $b_i\prime\prime$ 以上沒有人出價
            - payoff 跟 $b_i$ 一樣 $v_i - b_k$
    - ==都不會比直接心理中的 $v_i$ 定為 $b_i$ 好==
### 9.5 First-price auctions and other formats
- Truthfulness is no long a dominant strategy
    - 如果 $v_i = b_i$
    - 輸的時候 payoff 是 $0$
    - 贏的時候 payoff 也是 $0$
- First-price auction
    - 如果 $𝑏_𝑖$ 沒有贏，payoff 是 $0$. 
    - 如果 $𝑏_𝑖$ 贏，payoff 是 $𝑣_𝑖 – 𝑏_𝑖$ 
- All-pay auctions
    - 如果 $𝑏_𝑖$ 沒有贏，payoff 是 $−𝑏_𝑖$ 
    - 如果 $𝑏_𝑖$ 贏，payoff 是 $𝑣_𝑖−𝑏_𝑖$
    - 都更投標前，要做模型

### 9.6 Common values and winner’s curse
- 前面的出價都是 independent，但如果要 resale，狀況就會有所不同
- 大家有市場價的概念
    - 轉賣價 resale value 事先不知道
    - 假設有一個 true value $v$，但並不知道
    - 每個 bidder 會根據自身的資訊
        - 估 estimate value：$v_i = v + x_i$
        - $x_i$ 是一個平均為 $0$ 的 random variable
    - 有可能會產生高估的情況
- **Winner’s curse**
    - 因為得標的人出價一定最高
    - $\Rightarrow$ 所以估價常常是高估，而不是低估
        - bidder 很多，所以就算是 second-price auction 也一樣
    - $\Rightarrow$ 所以得標者常常會在 resale 時 lose money
- 我們知道在獨立出價的情況下，truthful bidding is a dominant strategy for auction
    - 但 Truthfulness is not optimal for auction **with common values**（有公道價、要轉賣的情況）
    - 因為我們不知道最後能夠賣多少錢，不確定真實的價格 true value $v$
    - 理性的 bidders 要自己去考慮到 Winner’s curse
        - 所以 bidders 應該要 **shade their bids downward**
        
### 9.7 Advanced material: bidding strategies in first-price and all-pay auctions
- 每個人自己的出價都是 independent and identically distributed
    - 每個人心中也會有一個對物品的 private value $v_i$
    - 分佈表示為 cumulative distribution function (CDF) $𝐹(∙)$
    - i.e. $𝐹(𝑥)=𝑃(𝑣_𝑖 ≤ 𝑥)$
- bidders 會出價的策略可以用函數來表示 $𝑠(𝑣)=𝑏$
    - 出價者的 true value $𝑣$ 
    - nonnegative bid $𝑏$
    - 假設每個人的策略都一樣
    - 函數的特徵
        - 嚴格遞增 strickly increase and differentiable
        - 出價不會比心中的價還高 $𝑠(𝑣) ≤ 𝑣$ for all $𝑣$
- If player 𝑖’s 心中的價格是 $𝑣$ 而 bid 是 $𝑏$, the conditional expected payoff that player 𝑖 receives
    - $(𝑣−𝑏)𝑃($ player $𝑖$ 的 $𝑏$ 贏 $)$
    - $=(𝑣−𝑏)𝑃(𝑠(𝑣_𝑗)<𝑏, ∀𝑗=1, 2, ⋯,𝑛, 𝑗≠𝑖|$ $𝑖$’s value is $𝑣$, his bid is $𝑏)$
        - 因為 player $i$ 要得標，表示其他人 $j$ 的出價都要比 $b$ 小
    - $=(𝑣−𝑏)𝑃(𝑣_𝑗 < 𝑠^{−1} (𝑏), ∀𝑗=1, 2, ⋯,𝑛, 𝑗≠𝑖|$ $𝑖$’s value is $𝑣$, his bid is $𝑏)$
        - 利用 inverse function 來表達 $v_j$
    - $=(𝑣−𝑏) 〖[𝐹(𝑠^{−1} (𝑏))]〗^{𝑛−1}$
        - n-1 個 P 都是彼此獨立，因此將機率相乘
        - 就可以使用到 cumulative distribution function (CDF) $𝐹()$ 來表達（已經照順序排好）
    - 利用微分，求使用 strategy $s(v)$ 時可以得到最大值
        - $\Rightarrow \frac{d}{d b}[$conditional expected payoff of player $i]|_{b=s(v)} = 0$
        - $= −[𝐹(𝑠^{−1} (𝑏))]^{𝑛−1}+(𝑣−𝑏)(𝑛−1)[𝐹(𝑠^{−1} (𝑏))]^{𝑛−2} 𝐹^′ (𝑠^{−1} (𝑏)) \frac{d}{db} (𝑠^{−1} (𝑏))|_{𝑏=𝑠(𝑣)}=0$
        1. 最後可得
            - 在 first-price auction $𝑠(𝑣)=(\frac{𝑛−1}{𝑛})𝑣 = b$
            - 在 second-price auction $s(v)=v=b$
        2. 而根據 Ordered statistics 我們知道 
            - independent uniformly distributed random variables $𝑋_1, 𝑋_2,⋯, 𝑋_𝑛$ on interval [0, 1] 時 $E(X_{(k)}) = \frac{k}{n+1}$
        - 故根據 1. 2. 可以求出
            - In the first-price auction the expected seller revenue is ![](https://hackmd.io/_uploads/Hy21TD8MT.png)
            - In the second-price auction the expected seller revenue is ![](https://hackmd.io/_uploads/r1k-TPIM6.png)
- **Reserve prices**
    - 價格沒有高於 $u$，交易取消
    - Truthful bidding 仍然是 dominant strategy
    - 在考慮只有一個 bidder 的情況下，true value 為 $[0, 1]$ 的 uniform distribution
        1. With probability 𝑟, the bidder’s value 會低於 𝑟, 產品沒有被賣出
            - seller in this case 的期望值是 $𝑟u$
        2. With probability $1−𝑟$, the bidder’s value is above $𝑟$, and the item will be sold to the bidder at a price of $𝑟$
            - seller in this case 的期望值是 $(1−𝑟)𝑟$
        - The total expected revenue is $𝑟(1−𝑟)+𝑟𝑢$
        - 微分可知，期望值最高的情況是 $𝑟=(1+𝑢)/2$
- **All-pay auction**
    - player i 的期望值
        - 假設 true value 為 $[0, 1]$ 的 uniform distribution
        - ![](https://hackmd.io/_uploads/HJl-owLMT.png)
        - 可以利用微分計算出最好的策略為 $𝑠(𝑣)=(\frac{𝑛−1}{𝑛})𝑣^n$
        - 可以看出當 $𝑛$ 快速上升時，bidders 會出價下降得非常多 
        - The expected value of a 單一 bidder’s contribution to seller’s revenue is ![](https://hackmd.io/_uploads/rJ7upD8zT.png)
        - The total revenue 是 ![](https://hackmd.io/_uploads/S1W2TPUfT.png)
        - 跟 first-price auction 和 second-price auction 結果一樣

## 10. Matching Markets
- 不同的人對物品有不同的喜好
- 可以利用價格來分配給人

### 10.1 Bipartitle graphs and perfect matchings
- ![](https://hackmd.io/_uploads/H1p-21rf6.png)
    - bipartite 兩邊只能互相連，不能單邊互連
    - Perfect Matching 都分配剛好，滿足一對一
- ![](https://hackmd.io/_uploads/rJr2YVyma.png)
    - Let $𝑁(𝑆)$ be the set of neighbors of nodes in $𝑆$
    - **Constricted**：$|N(S)|<S$
    - **Matching Theorem**
        - If a bipartite graph（左右兩邊的 Node 想圖） 沒有 perfect matching
        - 那他一定有 constricted set

### 10.2 Valuations and optimal assignments
- ![](https://hackmd.io/_uploads/rkKWo4JmT.png)
    - 達到最大的 valuations 品質
- ![](https://hackmd.io/_uploads/r14Vn4kmT.png)
- ![](https://hackmd.io/_uploads/ByxCGpNJm6.png)
- ![](https://hackmd.io/_uploads/r1nS2N1Q6.png)
    - Buyer 會比較想要跟誰買房子
    - 連起來的圖就是 Prefer-seller graph
    - 有可能沒有 prefer seller（都虧錢不如不買）

### 10.3 Prices and the market-clearing property
- Market-clearing prices
    - 可以都把房子賣給對的人
    - 房子的總和最高
    - 一定都可存在
    - Total valuation 一定是 optimal
- ![](https://hackmd.io/_uploads/BJLItH1mp.png)
    - C 這個 matrix 一個 row 只會有一個 1，其他都是 0
    - Total Payoff of $𝑀$ = Total Valuation of $𝑀$ – Sum of all Prices
    - 因為 Sum of all prices 是定值，所以最大化 valuation 就是最大化 payoff
    - An alternate view：如果也把 Seller 的 payoff（Sum of all Prices）也加入，那 Total Payoff 就是 Total Valuation of $M$

### 10.4 Constructing a set of market-clearing prices
- Bipartite graph auction model
    > 1. Initially all sellers set their prices at 0 一開始都設定為 0
    > 2. Buyers react by choosing preferred sellers, and we look at the resulting preferred-seller graph 開始配對
    > 3. If this graph has a perfect matching, we are done ：perfect matching 就結束了
    > 4. 不然 Otherwise, there is a constricted set of buyers 𝑆
    > 5. The sellers in 𝑁(𝑆) raise their prices by 1 unit simultaneously 賣家只要大於一個買家就升價1元
    > 6. Reduction operation: If the smallest price is 𝑝 and 𝑝>0, subtract 𝑝 from each price to reduce the lowest price to 0 全體平移，讓最低的價格變零。不然升價會沒上限！
    > 7. Iterate until we find a set of prices with a perfect matching 從頭再來一次
- ![](https://hackmd.io/_uploads/ryBxANJmT.png)
- Potential energy
    - 一開始的 energy 很高，但 iteration 越來越多的時候，能量越來越被消耗
    - 如果最後 Energy =0 就會停下來，找到最佳解
- 在過程裡面，有升價降價，能量就會有升有降，誰大？
    - ![](https://hackmd.io/_uploads/SJh3_f0Ma.png)
    - 統一降價，seller buyer 影響的量一樣
    - 因為升價的過程中
        - 雖然對單一 seller 來說，能量會上升
        - 但 buyer 數量較多，能量會下降更多
    - iteration 越多、總體能量下降

## 12. Bargaining and Power in Networks
### 12.1 Power in social networks
- Power 是社會學的重要 issue
    - 職位
    - 薪水
    - 個人身體狀態
- Network exchange theory
    - 利用分錢來判斷 power
    - The value may be divided equally or unequally between the two parties
    - 兩人分錢的方法 can be viewed as a kind of social exchange
    - Power then corresponds to the imbalance of the division
- Satiation
    - ![](https://hackmd.io/_uploads/SJAqZQCf6.png)
    - B becomes satiated
    - B 要拿比較多錢，以維持AC的關係
    - B 的權力比較大

### 12.2 Experimental studies of power and exchange
- one-exchange rule
    - 實驗
    - 桌上有一筆固定的錢
    - 可以選一個 partner 分錢
    - 先找到 match
    - 再討論如何分錢
    - 談完才有錢
    - The experiment is run for multiple rounds
    - High-information version：可以看到別人談的過程，low 就看不到
- example
    - 兩人
        - ![](https://hackmd.io/_uploads/rk_mQm0f6.png)
        - 結果一人一半
    - 三人
        - ![](https://hackmd.io/_uploads/BJMIQXCza.png)
        - 結果 B 拿 $\frac{5}{6}$ 
        - A 或 C $\frac{1}{6}$
    - 四人
        - ![](https://hackmd.io/_uploads/BJOim7Rzp.png)
        - AB+CD or BC
        - B 比較有 power，但比三人的版本弱，因為還有一個強者 C。代表 BC 要分錢的時候，C 不會讓。
        - B 是 $\frac{7}{12}$ 到 $\frac{2}{3}$ 
    - 五人
        - ![](https://hackmd.io/_uploads/r1swVXAGa.png)
        - C 在中間反而也是弱
        - BD 會去跟 AE 最弱者配
    - 其他
        - ![](https://hackmd.io/_uploads/r1k64QRGa.png)
            - BD 幾乎不會一起
            - DE 一半一半
            - B CA 分 $\frac{5}{6}$ $\frac{1}{6}$
        - ![](https://hackmd.io/_uploads/ByaWrmCza.png)
            - 通常 AB 一起配
            - CD 一起配
    - unstable
        - ![](https://hackmd.io/_uploads/rkuYr7CGa.png)

### 12.3 Results of network exchange experiments
- ![](https://hackmd.io/_uploads/rJd8IXRz6.png)
    - 有些圖可以改用 bipartite 來表示

### 12.5 Modeling two-person interaction: the Nash bargaining solution
- ![](https://hackmd.io/_uploads/r1JMOmAM6.png)
    - 兩者談的狀況比 outside option $x, y$ 好，就談得成
    - Assume that $𝑥+𝑦≤1$ and the surplus $s$ is $1−𝑥−𝑦$
        - $𝑥+\frac{𝑠}{2}=\frac{(𝑥+1−𝑦)}{2}$ to A
        - $𝑦+\frac{𝑠}{2}=\frac{(𝑦+1−𝑥)}{2}$ to B
- 如果實驗設計者讓參與者「吹牛」
    - 一個膨脹 status 
    - 另一個相反 status
    - Experimentally, it is found people inflate or deflate their outside options according to what they believe the status their opponent has

### 12.6 Modeling two-person interaction: the ultimatum game
- 範例：![](https://hackmd.io/_uploads/BJMIQXCza.png)
    - 結果 B 拿 $\frac{5}{6}$ 
    - A 或 C $\frac{1}{6}$
    - 欲解釋這樣的現象，為什麼 AC 還是會拿到不少的 $\frac{1}{6}$
- Ultimatum game
    - 前提範例：
        1. A is given a dollar and is told to propose a split of this dollar with B. A 提價錢問 B 要不要分
        2. B is given the option of approving or rejecting the proposal. B 決定要不要接受
        3. If B approves, each person keeps the proposed amount.  If B rejects, both get nothing. 接受就成交，否決就都沒錢
    - 從正常的 Nash 來說，A 是先出價的，所以他可以把自己的價格開的很高，B只要不是拿到 0 元就會接受
    - 但事實不然。實驗結果看出 A often offered fairly balanced split (about  $\frac{1}{3}$) to B，B 還是要拿到一定的價格才會接受。
    - 需要把情緒的部分考慮進去，並非純粹理性
### 12.7 Modeling network exchange: stable outcomes
- **Stability**
    - no node $X$ can propose an offer to some node $Y$ that makes **both** $X$ and $Y$ better off
    - 沒人可以讓彼此都更好
- example
    - ![image.png](https://hackmd.io/_uploads/S1e69bM7p.png)
        - $(a).$ C 可以 propose 他跟 B 分，B 拿 2/3、C 拿 1/3
        - $(a).$ BC edge 就是 instability
    - ![image.png](https://hackmd.io/_uploads/HkuQaWMma.png)
        - no stable outcome
        - 一組分完，另外一人就對弱勢出手、給大餅



### 12.8 Modeling network exchange: balanced outcomes
- Stable 沒辦法解釋
    - ![image.png](https://hackmd.io/_uploads/BJvORWfma.png)
    - 因為目前是 stable
    - 但 $B$ 的位置會比 $A$ 強，真實世界 $B$ 會拿比較多
    - 本章介紹 balanced outcomes 來解釋
- ![image](https://hackmd.io/_uploads/Hklrkroma.png)
    - $AB$ 兩人談得成就 ok
    - 談不成就去拿各自的 outside option
- **Balanced outcomes**
    - surplus 就是兩個減掉 outside option 剩的值
    - $B$ 分的比例：surplus 的 $1/2$ 加自己的 outside option
    - $A$ 分的比例：surplus 的 $1/2$ 加自己的 outside option
- ![截圖 2023-11-10 下午1.35.44](https://hackmd.io/_uploads/H1RVbBoQ6.png)
- ![截圖 2023-11-10 下午1.38.03](https://hackmd.io/_uploads/SyKT-rsX6.png)
- **Stem graph**
    - ![截圖 2023-11-10 下午1.41.51](https://hackmd.io/_uploads/B10izSjX6.png)
- In any network with a stable outcome, there is also a balanced outcome

### 12.9 Advanced material: a game-theoretic approach to bargaining
- 要解決的問題也是![截圖 2023-11-10 下午1.44.53](https://hackmd.io/_uploads/BJZw7Si7T.png)
- Formulate bargaining as a dynamic game
    - ![截圖 2023-11-10 下午1.45.56](https://hackmd.io/_uploads/rJZsmBs7a.png)
- **Breakdown probability 𝑝**
    - 需要一個機制來促進兩人認真考慮對方的 offer
    - 每一次 period 結束後，有機率 p 會使遊戲 breakdown，breakdown 後就是拿各自（原先的 outside option $x, y$ ）
- Finite-horizon games vs. infinite-horizon games
    - Finite
        - period 的個數是固定的
        - AB 其中一個可以先提，另外一個人決定是否拒絕
        - 由後往前分析
    - infinite 
        - 由前往後分析
    - 找出 subgame perfect equilibrium
        - is Nash equilibrium
- 跟現實的差別
    - 限制時間而不是 breakdown prob
    - Experiments usually involve with negotiations over multiple edges by multiple nodes 不是只有兩個人
- **Analysis of a two-period bargaining game**
    - 如果 breakdown，那就拿最新的那個分配
    - ![截圖 2023-11-10 下午2.06.46](https://hackmd.io/_uploads/rk7Yurjma.png)（分析順序由後往前）
    - $𝑧=𝑝𝑦+(1−𝑝)(1−𝑥)$
        - 根據 Nash，當 p = 1/2 時，是最佳解
- **Infinite-horizon bargaining games**
    - Finite-horizon games
        - ![image](https://hackmd.io/_uploads/rkF3LYeEa.png)
    - Infinite-horizon games
        - stationary stretegy：stretegy 跟時間無關
        - ![image](https://hackmd.io/_uploads/S1X1wtgV6.png)
        - 如果兩個人都用 stationary stretegy，所形成的 Equilibriums 叫做 stationary equilibria
- **Analysis of stationary equilibria of bargaining games**
    - A is scheduled to propose, he offers a split $(𝑎_1,𝑏_1), 𝑎_1+𝑏_1=1$
    - Whenever B is scheduled to propose, she offers a split $(𝑎_2,𝑏_2), 𝑎_2+𝑏_2=1$
    - ![截圖 2023-11-14 下午1.43.20](https://hackmd.io/_uploads/B1H-FYxVT.png)
    - 已知
        - $b_1 = \bar b$, A will offer the least he can to get B to accept his offer.
        - $a_2 = \bar a$, B will offer the least she can to get A to accept her offer.
    - 可知
        - $\bar b =py+(1−p)(1-\bar a)$
        - $\bar a =px+(1-p)(1-\bar b)$
    - 把 $b_1 = \bar b = 1 - b_2$ 與 $a_2 = \bar a = 1 - a_1$ 代換，兩個未知數、兩個式子解連立
        - $a_1=\frac{(1−p)x+1−y}{2−p}$
        - $b_2=\frac{(1−p)y+1−x}{2−p}$
    - As the breakdown probability p converges to 0
        - $(\frac{x+1−y}{2},\frac{y+1−x}{2})$
        - 就是前面 Balanced outcomes 的情況
## 16. Information Cascades
### 16.1 Following the crowd
- 每個人的 opinion、political position、activities 等等資訊都會被其他人所影響
    - 並不是 $ch.17$ 越多人用越好、而是單純被其他人影響
    - 有可能是當事人、第三人跟你說、也有可能你觀察到別人的行為，進而推理
- ![截圖 2023-12-15 下午2.02.33](https://hackmd.io/_uploads/Sygv2wF8p.png)
    - 你查到歐洲旅遊書推薦左邊，到現場發現右邊的餐廳都是人
    - 通常正常人會選擇右邊
    - 這就叫做 herding 或是 information cascade 發生了
        - cascade 就是指放棄原來的選擇，選擇新的
### 16.2 A simple herding experiment
- 放棄自己的想法，跟從別人的想法，就是 herding
- **process**
    1. 需要做決定
    2. 人們照順序做決定，可以看掉前面的人的決定
    3. 每個人都有 private information（自己有先做功課，沒有公開這些自己的資訊）
    4. 每個人看不到其他人的 private information，但可以根據他人的決定來猜測他人的 private information
- **experiment**
    - ![截圖 2023-12-19 下午1.34.58](https://hackmd.io/_uploads/H1e5oiAUp.png)
    - 共有兩種可能，每種都各 $50%$
    - 一個一個人進去有遮罩的投票棚子裡抽球，大聲講出來要猜是 Majority red 或是 Majority blue，其他人只會聽見、不會看見真的球顏色。
    - 為了鼓勵大家不要亂講，最後猜對的都有獎！
- **Analysis**
    - 第一個同學
        - 看到什麼顏色就猜哪個顏色球多
    - 第二個同學
        - 看到顏色跟前面相同，那就繼續猜那個顏色球比較多
        - 看到顏色跟前面不同，出現的機率平手，沒有一個特別有優勢，那我們就設定他選擇自己看到的顏色，相信親眼所見
    - 第三個同學
        - 如果聽到前面的都是不同顏色，就猜測兩個人拿到的不同顏色，那他就是看到什麼顏色就猜哪個顏色球多
        - 如果前面都是同一個顏色
            - 他抽到也是同一個顏色，那就繼續猜同一個顏色多
            - 他如果抽到不一樣的顏色，那還是持續猜前面那個顏色，儘管抽到不同的顏色(information cascade)
    - 第四位同學
        - 這裡關注邊緣的情況，前兩位抽到藍色、第三位猜到紅色
        - 但他知道第三位有可能 information cascade，所以不管第三位同學
        - 但目前這個 round，第四位同學就算如果抽到紅色，根據前兩位同學，她還是會講猜藍色(依然是information cascade)
    - information cascade 在第三個同學就開始了
- principle
    - information cascade 很容易發生
    - 根據上圖示，有 $\frac{1}{9}$ 的機率會發生整體全錯（前兩個都抽到少數）
    - 如果突然有兩個人作弊，把自己抽出來的不同顏色球 show 出來，那大家就會又從頭開始相信自己
### 16.3 Bayes’ rule: a model of decision making under uncertainty
- 條件機率
    - ![截圖 2023-12-19 下午2.08.29](https://hackmd.io/_uploads/H15vQ2RI6.png)
    - ![截圖 2023-12-19 下午2.06.49](https://hackmd.io/_uploads/SJv-730IT.png)
    - ![截圖 2023-12-19 下午2.08.53](https://hackmd.io/_uploads/HJzF72RI6.png)
- Bayes' rule
    - ![截圖 2023-12-19 下午2.10.00](https://hackmd.io/_uploads/By467nCI6.png)
    - 右邊容易算，來得出左邊的機率


### 16.4 Bayes’ rule in the herding experiment
- 我們已知
    - ![截圖 2023-12-19 下午2.27.58](https://hackmd.io/_uploads/S1ql_2CIp.png)
    - ![截圖 2023-12-19 下午2.28.10](https://hackmd.io/_uploads/SyD-_n0I6.png)
- Bayes' rule
    - 左邊並不好算，我們利用右邊來求![截圖 2023-12-19 下午2.27.05](https://hackmd.io/_uploads/SydaP2AUT.png)
    - 因為![截圖 2023-12-19 下午2.29.54](https://hackmd.io/_uploads/BJGO_3RIp.png)
    - 所以可得![截圖 2023-12-19 下午2.30.34](https://hackmd.io/_uploads/rkU5uh08T.png)
- 接著分析比較關鍵的第三位同學
    - 前兩位跟第三位抽的不一樣![截圖 2023-12-19 下午2.35.13](https://hackmd.io/_uploads/HkRit2AUa.png)
        - ![截圖 2023-12-19 下午2.36.36](https://hackmd.io/_uploads/Sybbq2AL6.png)
        - ![截圖 2023-12-19 下午2.36.56](https://hackmd.io/_uploads/ByIzq2CLT.png)
    - 可得![截圖 2023-12-19 下午2.38.06](https://hackmd.io/_uploads/Bkc85hAIT.png)
    - 因此第三位同學儘管抽到 red，還是猜測跟自己不同的情況，majority-blue

## 17. Network Effects
- **Informational effects**
    - 別人吃得有效，我也要去吃
- **Direct-benefit effects: also called network effects**
    - 大家一起用有好處，只有一台就沒用
    - 你用 apple 我也用 apple 可以來 airdrop
    - 傳真機普及，大家簽名可以傳來傳去
- 現在開始討論整體的概念
### 17.1 The economy without network effects
- 這個章節先不討論 network effect
- In this chapter we shall consider the market for a good without network effect
    - 每個人都要上編號
    - all real numbers in the interval $[0,1]$
    - 沒有 networks effect 的情況下，每個人想要買的意願就都是 intrinsic interest
        - 不考慮有多少人想買
- **Reservation price**
    - 如果產品低於 reservation price，就會買。高於就否
    - 願意買的最高價格
    - 使用者與其 reservation price 圖![image](https://hackmd.io/_uploads/Sy2eV9e4T.png)
        - 左邊代表越願意買，狂熱粉絲
- **How the market operates**
    - 價格都是固定的
    - 太高會沒人買、太低有成本問題
    - $p > r(0)$連狂熱粉絲都不買，那就沒人買
    - $p < r(1)$黑粉都買，那就大家都買
- **Socially optimal**
    - ![image](https://hackmd.io/_uploads/r1kaU9xVT.png)
    - ![image](https://hackmd.io/_uploads/r1c0UceE6.png)
### 17.2 The economy with network effects
- 除了 intrinsic interest、還有多少人使用了這個商品會影響出價
    - $r(x)$：對 consumer $x$ 的 intrinsic
    - $f(z)$：整個群體有 fraction $z$ 使用的好處
    - 對 consumer 的 reservation price： $r(x)f(z)$
        - 如果都沒有人用，那商品就沒有人想要出價買 $r(x)*0 = 0$
    - $r(x)f(z) \geq p*$ 就會買
- **Self-fulfilling expectations equilibrium**
    - 會自我實現的期望
    - 消費者共同預期產品的使用人數比例是 $z$
    - 如果每個人根據這個預期做出購買決策，結果確實有 $z$ 比例的人口購買了產品，那麼這就形成了一種自我實現的預期均衡。換句話說，如果每個人都預期會有 $z$ 比例的人購買，那麼這個預期最終會因為人們的行為而成真。
- An example
    - ![截圖 2023-11-14 下午3.05.06](https://hackmd.io/_uploads/HyJ42ql4T.png)
    - Remarks on the three equilibria：0, $z\prime$、$z\prime\prime$
        1. 如果$p∗ > 1/4$，則沒有符合$p∗ = z(1 − z)$的$z$值（因為$z(1 − z)$的最大值只有1/4）。在這種情況下，唯一的均衡是$z = 0$，意味著產品太貴，沒有人會購買
        2. 如果$p∗$在0和$1/4$之間，則會有兩個符合$p∗ = z(1 − z)$的$z$值。這兩個z值對應於抛物線$z(1 − z)$與水平線$y = p∗$相交的點。這意味著在這種情況下，可能有三種均衡：$z = 0$，$z′$和$z′′$。
    - 有買沒買的人都不會後悔
    - z 是代表的「人的比例」
### 17.3 Stability, instability, and tipping points
- ![image](https://hackmd.io/_uploads/rJAhxUqEp.png)
- **nonequilibrium z的動態**：
    - 如果 $z$ 在 $0$ 和 $z′$ 之間，存在 downward pressure 向下的壓力。因為在這個區間，$r(z)f(z) < p∗$，意味著消費者認為該產品的價值低於市場價格 $p∗$，從而導致需求下降。
        - downward pressure，是在談論消費者購買產品的比例下降，這在圖表上體現為水平軸（消費者比例軸）上的左移。
    - 如果 $z$ 在 $z′$ 和 $z′′$ 之間，存在 upward pressure 向上的壓力。因為在這個區間，$r(z)f(z) > p∗$，尚未購買的消費者會認為他們應該購買該產品，這會推動需求上升。
    - 如果$z$高於 $z′′$，又會出現向下的壓力，原因同 $z$ 在 $0$ 和 $z′$ 之間的情況。
- **equilibrium $z′$ 和 $z′′$ 的 stability**：
    - $z′′$ 是一個 stable 的 equilibrium。如果購買者略多於 $z′′$，需求會自然回歸到 $z′′$；如果略少於 $z′′$，需求也會上升回到 $z′′$。
    - 相比之下，$z′$ 是一個 unstable 的 equlibrium。如果略多於$z′$的人購買，需求會增加到$z′′$；如果略少於$z′$，需求會下降到 $0$ 。因此，$z′$ 是一個 critical point 或 tipping point 轉折點。
- **價格策略**：降低價格 $p∗$
    1. 使低均衡點 $z′$ 向左移動（即需求增加），這使得超越這一關鍵點更容易。
    2. 同時，高均衡點 $z′′$ 會向右移動，這意味著一旦超過關鍵點，用戶群的最終規模會更大。
    - $\Rightarrow$ 雖然初期設定較低的價格可能會導致虧損，但作為長期策略的一部分（例如，通過提供免費試用或低引入價格），這可能是一個可行的策略。
### 17.4 A dynamic view of the market
- 在之前的討論中，我們假設消費者**能夠正確預測商品的實際使用者數量**，從而達到均衡。
- 但這一節引入了一個新的情境
    - 消費者對於將有多少人使用這個商品**有一個共同的信念 $z$**，這個**信念 $z$ 可能錯誤**
    - 實際參與的數量是 $\hat z$
- 公式
    - 我們可以得出方程式
        - ![image](https://hackmd.io/_uploads/ByP6jP9Ep.png)
    - 並且定義出
        - ![image](https://hackmd.io/_uploads/H1By3v5NT.png)
        - 也就是給定共同的信念 $z$ 與價格 $p*$，求出真實狀況的 $\hat z = g(z)$
- 根據 `17.3` 的例子
    1. $𝑟^{−1} (𝑥) = 1 – 𝑥$
    2. 已知$𝑟(0)=1, f(z)=z$, and so the condition $\frac{𝑝*}{𝑓(𝑧)} ≤ 𝑟(0)$ $\Rightarrow$ $𝑝* \leq f(z)*r(0)$ $\Rightarrow$ $p* \leq z$
    - $1.+2. \Rightarrow$ ![image](https://hackmd.io/_uploads/rJXGJuqEp.png)
    - 可以得出圖形![截圖 2023-11-22 上午1.48.35](https://hackmd.io/_uploads/SyxFpP946.png)
    - 圖表進一步解釋了在市場中，消費者的共有預期和實際的市場參與之間的動態關係。
    1. 這裡，我們可以看到，當預期與實際的市場參與程度相匹配時，會形成一個 self-fulfilling 的 expected equilibrium
    2. 當實際的市場參與率低於預期時（$\hat z = g(z)$低於$\hat z = z$），會有向下的壓力，導致市場參與減少。
    3. 當實際的市場參與率高於預期時（$\hat z = g(z)$高於$\hat z = z$），則有向上的壓力，導致市場參與增加。
- 這不僅適用於特定的函數形式，而且是一般性的，特別是在有 Network effect 網絡效應的情況下
    - 例如，預期更多的人使用社交媒體平台會增加平台的價值，這進而又吸引更多的用戶加入。
    - 而當預期的用戶數量達不到某個點時，可能會造成用戶流失，從而導致平台價值下降。
    - 更 general 的圖示：![截圖 2023-11-22 上午2.11.14](https://hackmd.io/_uploads/S1Cpzdq4p.png)
- **Dynamic behavior**
    - 使用社群軟體來實驗追蹤使用者的使用量
    - $z_{t+1} = g(z_{t})$
    - ![截圖 2023-11-22 上午2.30.34](https://hackmd.io/_uploads/Hyv8vd9Ep.png)
    - 連續的更新會造成使用者的 size 收斂到 stable equilibrium point (並且 move away from the vicinities of unstable ones)
    - 這種分析方式雖然是圖形化的，但它提供了一個完全嚴謹的分析框架，讓我們可以更直觀地理解參與者規模**如何隨著時間和人們預期的變化而變化**。


### 17.5 Industries with network goods
- **Social Optimality with Network Effects**
    - 在一個沒有網絡效應的標準市場中，均衡通常是社會最優的，因為每個消費者根據自己的偏好和產品的價格做出獨立決策，並不影響其他人。
    - 在有網絡效應的市場中，一個產品的價值會隨著使用該產品的人數增加而增加。
    - 它會導致市場均衡不一定達到社會最優，因為在決策時，人們通常不會把這種外部效應計算在內。這導致了市場均衡可能不會反映出所有可能的社會福利，從而不達到社會最優。
        > ![截圖 2023-11-22 上午2.53.48](https://hackmd.io/_uploads/rJ66hdcE6.png)
- **Network Effects and Competition**
    - 可以考慮兩個提供類似服務的社交網絡站點，它們各自的價值取決於使用它們的人數。
    - 當產品競爭中存在網絡效應時，通常會有一個產品主導市場，這是因為第一個達到臨界點（tipping point）並因此吸引消費者的產品，會使其他競爭產品相對不那麼吸引人。
    - 達到臨界點並成為市場主導者比產品的絕對品質更重要。
## 18. Power Laws and Rich-get-richer Phenomena
- Five fundamental properties
    - Clustering
    - **Power law degree distributions**
        - 本章學習
    - Small world property (logarithmic path lengths)
    - Nonzero degree correlations
    - Existence of community structures


### 18.1 Popularity as a network phenomenon
- 我們的行為會被周遭影響
- 類似模仿的行為
- Popularity is extreme imbalances
    - 能夠有影響力的人非常少
- 網頁很好作為示範
    - 利用 in-link 作為衡量標準
    - out-link 不重要，無法公平衡量
    - ![截圖 2023-11-21 下午1.35.15](https://hackmd.io/_uploads/B1QobaYNT.png)
- 每個 page 的 in-link 為 k 個
    - k 的分佈為何？normal-distribution?
    - ![image](https://hackmd.io/_uploads/rkidM6FNT.png)
    - ![image](https://hackmd.io/_uploads/rJBcf6KNT.png)
- 中央極限定理
    - ![image](https://hackmd.io/_uploads/HyNB7TKN6.png)

### 18.2 Power laws
- 根據實驗
    - in-link 為 $k$ 的佔 $1/k^2$
    - 但 normal distribution 應該為 $exp(-(k-u))^2/ \sigma$
    - 表示沒有像 normal distribution 極端值沒那麼難發生
    - 並不是 normal distribution
- A function that decreases as 𝑘 to some fixed power, such as $\frac{1}{𝑘^2}, \frac{1}{𝑘^3}...$ in the present case, 這就叫做 a power law
    - 電話號碼
    - 書籍拍賣
    - natural science 跟 normal distribution 有關
    - popularity 跟 power laws 比較有關
- Let $𝑓(𝑘)$ be the fraction of items that have value $𝑘$, and suppose you want to know whether the equation $𝑓(𝑘) = \frac{𝑎}{𝑘^𝑐}$  approximately holds
    - $log\ f(k)=log\ a-c\ logk$
    - ![image](https://hackmd.io/_uploads/B14aP6tVT.png)
    - 這樣的雙對數圖表可以快速地顯示數據是否大致遵循 power law

### 18.3 Rich-get-richer models
- 為什麼不是 normal distribution 而是出現 power law 的結果呢？
    - normal distribution 彼此是互相獨立
    - 但在 population 的角度，人們在做決定時傾向於模仿之前做過類似決定的人的行為，**彼此的選擇會 feedback**，所以會互相影響。
- **Copying model**
    - ![截圖 2023-11-21 下午2.13.25](https://hackmd.io/_uploads/B1f9c6KNp.png)
        - $2(b)$ 等效，跟 page 連接的機率，跟他的 in-link 個數成正比：![截圖 2023-11-21 下午2.34.21](https://hackmd.io/_uploads/S1T_k0FV6.png)
        - ![截圖 2023-11-21 下午2.46.48](https://hackmd.io/_uploads/r15vz0K4T.png)
        - 被稱為 **preferential attachment**，意味著新頁面更傾向於鏈接到那些已經很受歡迎的頁面。這種模仿行為解釋了為什麼一些頁面會變得非常流行，因為它們有更多的機會被新頁面選擇並建立鏈接。
        - 可以注意到，每個頁面都只會有一個 out-link

### 18.4 The unpredictability of rich-get-richer effects
- ![截圖 2023-11-21 下午2.55.01](https://hackmd.io/_uploads/r1dIEAYNa.png)
    - 如果我們可以回到15年前，然後再次推進歷史，哈利波特書籍是否會再次賣出數億本，還是其他兒童小說作品會取得巨大成功？如果歷史能夠多次重演，最受歡迎的項目可能並不總是相同的。
    - 如果書在早期取得優勢，那有極高可能持續領先
    - 所以如果可以重新選擇，一開始的 Uniform 很重要，造成了 unpredictablility
- 另外一個實驗，創建了一個音樂下載網站，上面有48首不同質量的歌曲
    - 網站訪問者會隨機被分配到網站的八個副本之一，每個副本開始時都具有相同的歌曲和下載次數為零。然而，每個副本隨著用戶的到來而不同地演化。
    - 這個實驗顯示，當你能夠將歷史向前推進八次時，48首歌的流行度有明顯的變化。

### 18.5 The Long Tail
- 長尾效應描述了一個產品的銷售分佈
    - 其中少數幾個熱門產品（如暢銷書或流行音樂）佔據了市場的大部分銷售
    - 但同時還有**大量銷量較小的產品加起來也能創造顯著的總銷量**。這種分佈模式對於擁有大量庫存的媒體公司來說尤其重要，因為它們可以在不同的市場縫隙中找到利基市場。
- power law 通常聚焦在最流行的項目上，而 long tail 則將注意力轉移到不那麼流行的項目上。這種視角的轉換意味著，當我們觀察銷售量越來越大的項目時，我們其實是在探索銷量較低的產品群。
    - power law 的視覺化圖形，關注銷售出去 $k$ 個，有幾種商品：![image](https://hackmd.io/_uploads/Bk-RPQfS6.png)
    - 將 $x$ 軸和 $y$ 軸互換，得出 long tail 的圖形，關注各個單一商品，銷售出去幾個：![image](https://hackmd.io/_uploads/B13-ImGHT.png)

### 18.6 The effect of search tools and recommendation systems
- 搜尋引擎會讓 Rich-get-richer 更嚴重
- 讓人更容易碰觸到 unpopular 的 item，那就比較能對抗 Rich-get-richer
### 18.7 Advanced material: Analysis of rich-get-richer processes
- 目的是試圖解釋 power law 的起源
- 可見 `18.3` Copy model
- 新節點鏈接到既有節點的整體機率是 $\frac{p}{t}+\frac{(1−p)X_j(t)}{t}$，其中 $p$ 是隨機選擇鏈接的機率，$t$ 是網路中的總鏈接數，$X_j(t)$ 是節點 $j$ 在時間 $t$ 的入鏈接數。
    - 因為每個頁面都只會有一個 out-link，所以總鏈結數 $t=$ 時間 $t$
- ![截圖 2023-11-21 下午3.07.33](https://hackmd.io/_uploads/BJ4BvAY4a.png)
- 為了簡化分析，這裡使用了deterministic，就是時間以連續方式進行，並用連續函數來近似節點 $j$ 的 in-link 數量。這個函數的行為通過微分方程 $\frac{dx_j}{dt}=\frac{p}{t}+\frac{(1−p)x_j}{t}$ 來模擬，這個方程描述了 $x_j$ 的增長率。
    - 這種 deterministic approximation 使得我們能夠預測 in-link 數量的平滑增長，而不是處理隨機變量的隨機跳躍。
    - ![截圖 2023-11-24 下午1.40.35](https://hackmd.io/_uploads/HJMDP364a.png)
- 解微分方程式
    - ![image](https://hackmd.io/_uploads/ByoeyEzS6.png)
    - ![image](https://hackmd.io/_uploads/ryV-yNzB6.png)
- Qestion：多少比例的頁面 $x$，在 $t$ 時間點有 $k$ 個 in-link？
    - 也就是 what fraction of all functions $x_j$ satisfy $x_j(t) ≥ k$ ?
    1. ![截圖 2023-11-27 下午11.57.57](https://hackmd.io/_uploads/ryI534zrT.png)
        - 這裡已經可以看到 power law 的型態，因為 $p, q$ 是定值，所以 $x_j(t)$ 超過 $k$ 的比例，跟 $k^{-\frac{1}{q}}$ 成正比。
    2. 接著是從一個
        - 至少 $k$ 個入鏈接的節點的分數 $F(k)$
        - 轉換到恰好有  $k$ 個入鏈接的節點的分數 $f(k)$ 的過程
        - 因為當有一個累積分佈函數（CDF）$F(k)$ 表示隨機變量**累積到某個值**的機率時，可以微分得到機率密度函數（PDF）$f(k)$。而 PDF 給出了隨機變量**確切等於某個值**的機率。
    - ![截圖 2023-11-28 上午12.25.31](https://hackmd.io/_uploads/BJj-XrzHa.png)
    - 最後跟 k 相關的 term 為 $\frac{1}{k^{1+1/(1-p)}}$，也就是 power law 的來源
        - 當 $𝑝$ is close to $1$，分母的值趨近於無窮大，整個值、$k$ 影響的機率趨近於 $0$，代表k幾乎不影響，所以幾乎都是 uniform random choices 在影響
        - 而當 $𝑝$ is close to $0$, the growth of the network is strongly governed by rich-get-richer behavior
- 這種方法的優點是能夠清晰地看到預期變化如何導致 power law 中的指數分佈。
    - 這提供了一個有力的工具，用於研究和理解複雜網絡中的流行度分佈
    - 並有助於解釋為何某些網頁或者產品能夠成為極其流行的現象

## 19. Cascading Behavior in Networks
### 19.1 Diffusion on networks
- Spread of new technologies, new practices, opinions and etc., from person to person through a social network
- 兩種
    - Informational effects
        - 我看到你穿潮牌很猛，我也想穿
        - The novelty and initial lack of understanding made it risky to adopt
        - It is highly beneficial, so people follow
    - Direct-benefit effects
        - 我直接也拿到好處了，所以我也想要
        - Expert effect
        - Majority effect
        - Why some innovations fail to spread?
			- Complexity for people to understand and implement
			- Observability so that people can become aware that others are using it
			- Trialability so that people can mitigate the risks of using it
			- Compatibility with the social system

### 19.2 Modeling diffusion through a network
- 討論新的想法，在社群上面散播，利用微觀角度來研究
- Diffusion of innovations based on informational effects can be modeled by epidemic network
    - Infectious diseases spread over a social network
- In this section we build a model to study the direct-benefit effects in networks 
- $V$ 可以選擇 $A$ 或是 $B$
    - ![截圖 2023-11-24 下午2.10.16](https://hackmd.io/_uploads/H1I80n6V6.png)
    - ![image](https://hackmd.io/_uploads/HkfuolmH6.png)
    - $𝑝$ fraction of $𝑣$’s neighbors adopt $A$
    - $(1−𝑝)$ fraction of neighbors adopt $B$
    - Let $𝑑$ be the degree of $𝑣$
    - Node $𝑣$ adopts $A$ if
        - ![截圖 2023-11-28 下午1.33.11](https://hackmd.io/_uploads/B13ijg7HT.png)
        - $q$ 就是決定要選擇 $a$ 還是 $b$ 的 threshold
- **Cascading behavior**
    - 隨著時間，陸續散播
    - An example with $a=3$ and $b=2$
    - ![image](https://hackmd.io/_uploads/SkUETlXr6.png)
    - 一開始的 Initial Adaptor 是 $v$ 跟 $w$，設定為 $A$，他們是不玩這個 Game 的，不會被其他人影響，所以不會因為其他人 $B$ 多，他改成 $B$
    - 接著計算 $r、t$ 周圍人使用 $A$ 的比例 $p$，如果 $p$ 大於 $\frac{b}{a+b}$，並且會改成 $A$
    - 其他點也陸陸續續更動
    - ![image](https://hackmd.io/_uploads/r1zbAlXrp.png)
    - 另外一個例子
    - ![image](https://hackmd.io/_uploads/S1DVAxXr6.png)
    - ![image](https://hackmd.io/_uploads/rJ6BAlQBa.png)
- **Adoption usually stops at the boundaries of communities**
    - People have an incentive to be on the sites their friends are using, even when large parts of the world are using something else
    - Certain industries heavily use Apply Macintosh computers despite Microsoft Windows is more prevalent
- **Strategies to improve spreading**
    1. 讓 change the payoff 𝑎 升高
    2. convince some people (fashion leaders) in the part of network using B to switch to 
- **Population-level network effects vs. network cascades**
    1. Population-level：everyone is evaluating their adoption decisions based on the fraction of the entire population 
    2. Network cascades：you only care about what your immediate neighbors are doing
### 19.3 Cascades and clusters
- 在 tightly-knit communities 裡，很困難去產生 diffusion of innovations
- **Clusters**
    - a cluster of density $𝑝$ is a set of nodes such that each node in the set has at least a fraction $𝑝$ of its network neighbors in the set
    - 每一節點，$\frac{在 cluster 內的相連接鄰居的數量}{所有相連接鄰居}$ 超過 $p$
    - ![截圖 2023-11-28 下午1.58.43](https://hackmd.io/_uploads/SJbjbbXra.png)
    - 缺點
        - 全部的 Node 是一個 cluster of density $p=1$，因為所有的鄰居都一定會被納入
        - The union of two density-𝑝 clusters is also a cluster of density 𝑝，如圖上第一、三圈也是同一個 cluster with $p$
- **Remaining network**
    - consists of the portion of the network other than the initial adopters
    - 就是 intial adopters 之外的部分
- **A claim**
    - Consider a set of initial adopters of behavior $A$, with a threshold $𝑞$ for nodes in the remaining network to adopt behavior $A$
    1. If the remaining network 包含一個 cluster 他的 density greater than $1−𝑞$, 那 initial adopters 就不會 cause a complete cascade，因為 $A$ 一定會遇到無法衝破 threshold $q$ 的情況
    2. 反過來敘述也對，Moreover, whenever a set of initial adopters does not cause a complete cascade with threshold $𝑞$, the remaining network must contain a cluster of density greater than $1−𝑞$


### 19.4 Diffusion, thresholds, and the role of weak ties
- **聽到跟接收**
    - ![image](https://hackmd.io/_uploads/r1-NjW7Bp.png)
    - x 軸為時間、y 軸為比例
    - 兩者概念並不相同
        - ![截圖 2023-11-28 下午2.40.10](https://hackmd.io/_uploads/S1YIoWXH6.png)
- **Diffusion and weak ties**
    - ![截圖 2023-11-28 下午2.51.46](https://hackmd.io/_uploads/BJEzRbQSa.png)
    - Weak ties $𝑤−𝑢$ and $𝑤−𝑣$ 讓 $𝑢$ 跟 $𝑣$ 很好的從 $w$ 接收新知，在他們原本的 cluster 很難接收的資訊
    - 然而如果有一個很高的 threshold，diffusion 很難再 two weak ties 傳播。
    - 例如政治活動相較於網路笑話，threshold 高很多。

## 20. The Small-World Phenomenon
### 20.1 Six degrees of separation
- 6 步轉信，可以讓收信人收到
    - Short path 很多、很abundance
    - 大家都不太知道 global 的狀況，不太知道朋友的朋友有誰
- What is a suitable model for social networks?
	- A huge number of nodes and edges
	- Homophily 
	- Transitivity
	- Power law degree distribution
	- **Abundance of short paths** 在這章獲得滿足
### 20.2 Structure and randomness
- 最 naive 的設計 model，abundant short paths 跟 a large number of nodes
    - 比較 random，path 較短![image](https://hackmd.io/_uploads/HkrLgM7S6.png)
    - 比較 regular，path 較長，要繞很久才繞的到目的地![image](https://hackmd.io/_uploads/HJFIgMXBp.png)
- **Regular vs Random**
    - Regular networks are full of triangles
        - However, they have long distances between two arbitrary nodes
    - Random networks have few triangles (asymptotically)
        - However, they have a lot of short paths
    - ![截圖 2023-11-28 下午3.07.44](https://hackmd.io/_uploads/ryyC-zQHp.png)
- ![截圖 2023-12-01 下午1.31.40](https://hackmd.io/_uploads/S1opJePBp.png)
    - $(a)$ 把某些線拆掉，重新跟新的點連結，rewiring
    - $(b)$ 是改良版，不把原本的線拆掉，以免造成數學的困擾，而是直接連接新點
- ![image](https://hackmd.io/_uploads/HyhRfMXS6.png)
    - $(b)$ 
        - 細線是 regular，多三角
        - 粗線是 random short cut，path 較短，也是看成 weak tie
        - 每一個 node 有 $k$ 個 random edge
        - 圖示 $k=5$
    - 若改成每 $k$ 個 node 有一個 random edge
        - ![截圖 2023-12-01 下午1.45.05](https://hackmd.io/_uploads/rkklXxwra.png)
        - sufficient abundance of short paths between two arbitrary nodes 效果差不多
        - On average, each node has $1/𝑘$ random edges
        - To see why, conceptually group $𝑘× 𝑘$ subsquares of the grid into “towns”. Each town has $𝑘^2$ nodes. Each town has 𝑘 random links to other towns.
        - This is like the previous model.

### 20.3 Decentralized search
- Decentralized search 去中心化搜索，這是指在缺乏完整網絡地圖的情況下，個體如何能夠找到通往特定目標的短路徑
- 一開始 node $𝑠$ 只知道 location of $𝑡$ on the grid, but, crucially, 他不知道 random edges out of 其他 node
- ![image](https://hackmd.io/_uploads/BkkaVgPrT.png)
    - Constantly reducing the distance to the target
    - 因為不知道下一個人的 path 有哪些，所以 short path 不能太 random，不然無法找到適合越來越短的 path。
    - 所以下一個選擇的人的 path，短的要越來越多，要成一定比例，不是真的 random
    - 所以下面的章節就是要討論這樣多了一個機率的模型

### 20.4 Modeling the process of decentralized search
- **Model**
    - The length of the random links in Watts-Strogatz model is too random and too long
    - Watts 的不太好，本書作者提出改良版
    - For two nodes $𝑣$ and $𝑤$, let $𝑑(𝑣,𝑤)$ be the distance
        - i.e. number of grid steps, between them
    - The probability of generating a random link out of $𝑣$ that reaches $𝑤$ is proportional to $𝑑(𝑣,𝑤)^{−𝑞}$
        - **機率跟距離有關**，不是 Watts 的 uniform
        - 這裡使用一個 cluster component $q$
- **cluster component q 值的討論**
    - Watts-Strogatz model corresponds to $𝑞 = 0$
        - 就是完全 random 的狀況
    - 如果 $q$ 很大，那每步距離就會變得太短，哪也很難碰到很遠的點
    - $q$ 就是一個中間適合的距離最好
    - $q$ 大小的圖式
        - ![image](https://hackmd.io/_uploads/B18hIlvS6.png)
        - 左邊 $q$ 很小，可能結果太 Random，reducing the network's ability to create effective shortcuts across distant parts of the network.
        - 右邊 $q$ 很大，不適合做長距離的搜尋，There's a higher preference for very long-range links, leading to fewer useful shortcuts for gradual, step-by-step progression towards the target.
    - Cluster component $q$ 與 到目的地時間 $T$ 的關係圖
        - ![image](https://hackmd.io/_uploads/H1kSwlwBa.png)
        - 大約選擇 $2$ 會最好
- **計算連接 probability**
    - ![image](https://hackmd.io/_uploads/BJUTvlvBT.png)
    1. 由於平面上的面積隨半徑的平方而增長，這個群組中的節點總數與 $d^2$ 成正比
    2. 另一方面，$v$ 與群組中任一節點連接的機率取決於具體距離，但每個個別概率與 $d^{-2}$ 成正比
    - $1+2 \Rightarrow$ 每一圈區域中的節點數量，和與其中任一節點連接的機率大致抵消
    - 所以隨機連接到這個環中某個節點的 probability 大致與 $d$ 的值無關



### 20.5 Emperical analysis and generalized models
- 這個章節要討論實例與更 general 的 model
- Is there evidence that real world networks have exponent $𝑞 = 2$ ?
    - ![image](https://hackmd.io/_uploads/ryc_U4nH6.png)
    - 以美國 LiveJournal data 為範例
    - 但並不是完整的棋牌格平均分佈，美國東西岸的人都比較多
- **Alignment**
    - 所以需要改變，地圖跟棋盤格做 alignment
    - is to determine link probabilities not by physical distance but by rank
    - 第幾近的，不是用距離
    - $𝑟𝑎𝑛𝑘(𝑤) =$ the number of other nodes that are closer to $𝑣$ than $𝑤$ is
        - ![image](https://hackmd.io/_uploads/SJisDVhr6.png)
- We have shown that $𝑞 = 2$ makes random links uniform in probability in grid model
    - linking to w with prob. $d^{-2}$
    - 那如果換成 $rank$
    - 就會是 $rank(w)^{-1}$
    - 可以從上圖 $(b)$ 看出，$rank$ 已經是 $d^2$ 了
    - 所以這就是 generalized 的 model，節點 $v$ 以與 $rank(w)$ 的 $-p$ 次方成正比的 probability 選擇節點 $w$ 作為隨機連接的另一端，$p$ 就是 $-1$
- 實驗結果
    - ![image](https://hackmd.io/_uploads/Bk3ZY4nHp.png)
    - x 軸是 $rank\ r$，表示人跟人的關係
    - y 軸是 $P(r)$，表示這群資料裡 pairs of nodes 距離 $r$ 還是朋友的比例 
    - 點是 dataset 的數據
    - 會介於兩個 line 之間，就大約為 $rank(w)^{-1}$
    - 其他實驗 Rank-based friendship 在 Facebook，結果也是接近 $rank(w)^{-1}$ 

### 20.6 Core-periphery structures and difficulties in decentralized search
- Watts 的模型的人，非常 uniform，沒有考慮到 Race, age, sex, affluence, occupation, hobby, opinion, and et
- 現實社會中的結構
    - ![image](https://hackmd.io/_uploads/ByuicEhH6.png)
    - Core-periphery structures 核心-邊緣結構
        - 其中高地位的人在一個密集連接的核心中相互連接，而低地位的人則分散在網絡的邊緣
    - 中心的達官顯貴連結較多，邊陲的低端連結較少
        - 高地位的人擁有廣泛旅行、通過共同 focal 相遇（如俱樂部、興趣、教育和職業追求）的資源，並更普遍地在網絡中建立跨越地理和社會界限的連接
        - 低地位的人形成的連接則更加聚集和局部
    - Watts 並未捕捉此種結構
    
### 20.7 Advanced material: analysis of decentralized search
- 分析 Decentralized search
    - 這裡的範例都先使用一維度分析，再拓展至多維
    - 在這種一維分析中，最佳搜索指數 $q$ 等於維度，因此將使用指數 $q = 1$ 而不是 $q = 2$
- ![截圖 2023-12-05 下午1.54.31](https://hackmd.io/_uploads/B1IXsE3Bp.png)
    - 環狀的 Watts 結構，也是最早提出的版本
    1. 節點排列：$n$ 個節點排列在一維環上，每個節點通過有向邊與它旁邊的兩個節點相連。
    2. 長距離連接：每個節點 $v$ 還有一個指向環上某個其他節點的單一有向邊；$v$ 連接到任何特定節點 $w$ 的概率與它們在環上的距離 $d(v, w)$ 的 $-1$ 次方成正比。
    3. 網絡結構：整體結構是一個帶有隨機邊的環，類似於我們在二維網格中看到的結構。
- **Myopic search**
    - 每個人都知道其他人在什麼地方
    - 黑線稱為 local contact
    - 但不知道其他人的紅線 Long-rang contact
    - ![image](https://hackmd.io/_uploads/SJVc3E2ra.png)
    - 用轉傳的方式
        - greedy 選擇傳給 **最接近目的地** 的相連接朋友
        - 並不是最佳的
        - 但距離一樣可以縮的很短，以下內容就是在分析 Myopic search
#### 20.7 A. The Optimal Exponent in One Dimension
- **Analyzing Myopic Search: The Basic Plan**
    - 問題定義：
        - 在該網絡中隨機選擇起始節點 $s$ 和目標節點 $t$
        - 近視搜索找到目標所需的步數是一個隨機變量 $X$，我們關注的是這個隨機變量的期望值 $E[X]$ 多大？
    - 分析步驟：
        - 根據此方式，我們想要去追蹤、分析移動的狀況
        - 所以定義「測量從起始點到目標點距離減半」的狀態叫做 phase、階段
        - 當 message 從 $s$ 移動到 $t$ 時，如果它與目標的距離目前在 $2^j$ 到 $2^{j+1}$ 之間，則稱它處於搜索的第 $j$ 階段
        - 所以 $j$ 是遞減的
    1. 階段數量：
        - number of 階段最多是 $log_2 n$，即從 $1$ 增長到 $n$ 所需的倍數次數、經歷過的 phase
        - 將 X 表示為不同階段所需時間的總和：$X = X_1 + X_2 + ... + X_{log_2n}$
    2. 期望的線性：
        - 期望的線性指出，隨機變量之和的期望等於它們各自期望的總和：$E[X] = E[X_1] + E[X_2] + ... + E[X_{log_2n}]$。
    3. 每個階段的期望值：
        - 關鍵在於展示每個 $E[Xj]$ 內的經過次數，最多與 $log_2n$ 成正比。
    - $1+2+3\Rightarrow$ This would show that $𝐸[𝑋]$ is of the order $(log⁡𝑛)^2$
        - 在這裡 simply 使用 $logn$ 來代表 $log_2n$
        - 因為每個 $E[X]$ 本身跟 $log_2n$ 成正比，又有 $log_2n$ 個 $E[X]$
    - ![截圖 2023-12-07 中午12.38.59](https://hackmd.io/_uploads/BJHd2aCBT.png)
    - 這表明在給定的連接分布下，即使整個網絡有 $n$ 個節點
        - 近視搜索構建的路徑長度卻顯著更短：$(log⁡𝑛)^2$
        - 這樣的分析結果證明了 Myopic Search 在這種網絡環境中的高效性
- **Intermediate Step: The Normalizing Constant**
    - 我們知道節點 $v$ 連接到 $w$ 的機率會與 $d(v, w)^{-1}$ 成正比，但這個比例的常數因子是多少呢？
    - 所以我們設機率為 $\frac{1}{z}d(v, w)^{-1}$，而 $Z$ 的值就是所有 node of pairs 的 $d(v, w)^{-1}$ 的和
        - 也就是「全部的點距離的比例」分配概念
    - 注意到從 $v$ 到距離為 $1$ 的節點有兩個，距離為 $2$ 的有兩個，以此類推，直到 $n/2$。假設 $n$ 是偶數，距離為 $n/2$ 的節點（環上與 $v$ 直徑相對的節點）只有一個。因此，我們可以得出不等式![截圖 2023-12-07 晚上8.09.47](https://hackmd.io/_uploads/BJ5MINy8p.png)
    - 又我們已知![截圖 2023-12-07 晚上8.10.22](https://hackmd.io/_uploads/H16NIV1UT.png)
    - 所以可以得出![截圖 2023-12-07 晚上8.12.07](https://hackmd.io/_uploads/HyHi8VJUa.png)
    - 此時，我們可以把 $Z$ 代回原式 $\frac{1}{z}d(v, w)^{-1}$，得到真實的 probability ![截圖 2023-12-07 晚上8.15.22](https://hackmd.io/_uploads/S1wPvVyIa.png)
- **Analyzing the Time Spent in One Phase of Myopic Search**
    - ![截圖 2023-12-07 中午12.38.59](https://hackmd.io/_uploads/BJHd2aCBT.png)
        - 我們知道，當目前的點 $v$，距離目標點 $t$ 還有距離 $d$ 時，如果 $d$ 介於 $2^j$ 到$2^{j+1}$ 時，那 $v$ 就是在 phase $j$，當 $d < 2^j$ 時，phase $j$ 就會結束
        - 如果 $v$ 的 long-range contact 連接到的點 $w$ 與 $t$ 的距離能夠 $<d/2$ 的話，這個 phase 就會馬上結束，下面就會證明發生這種跳躍的機率很高
    - ![截圖 2023-12-07 晚上9.25.10](https://hackmd.io/_uploads/ry7avByL6.png)
        - 在 $t$ 左右兩邊的 distance $\frac{d}{2}$，就是 $w$ 希望能夠在的區間範圍，也就是 $v$ 的 long-range contact 希望能夠觸及到的範圍，如此一來才能跳出 phase $j$
        - 這範圍中共有 $d+1$ 個 node (包含 $t$)
        - 距離 $v$ 最遠的是最左邊的點，距離是 $\frac{2d}{3}$，也就是機率最小的情況，根據前面的 probability 運算可以知道其機率為 ![截圖 2023-12-07 晚上11.42.09](https://hackmd.io/_uploads/HJJJ_PJI6.png)
        - 而範圍內共有 $d$ 個點，所以其中一個點是 long-range contact 連接到的機率 at least 是![截圖 2023-12-07 晚上11.45.19](https://hackmd.io/_uploads/HJaqdwkUp.png)
    - 上述情況是每走一步會進入範圍的情況，如果今天站在第 $i$ 步，還有 $i-1$ 步要走，而每一步都沒有跳去下一個 phase，機率為![截圖 2023-12-07 晚上11.51.58](https://hackmd.io/_uploads/Sk97qDkL6.png)
    - 所以在第 $j$ phase 的情況下，要去分析在 $j$ phase 內要走幾步，那就是「走1步的機率 \* 走1步的步數 + 走2步的機率 \* 走2步的步數 + ...」，列式可得![截圖 2023-12-07 晚上11.56.23](https://hackmd.io/_uploads/B14NoPkL6.png)
    - 那也可以改成下面這種表示法![截圖 2023-12-07 晚上11.55.56](https://hackmd.io/_uploads/r1FfiwyIp.png)
    - 綜合前面的結果我們可知![截圖 2023-12-07 晚上11.57.22](https://hackmd.io/_uploads/rJWdsv18a.png)
    - 右邊會收斂成![截圖 2023-12-07 晚上11.58.49](https://hackmd.io/_uploads/r1I6owyIT.png)
    - 因此我們得到，在 $j$ phase 的情況下 ![截圖 2023-12-07 晚上11.59.47](https://hackmd.io/_uploads/HJg-2D1UT.png)
    - 因為 $E[X] = E[X1] + E[X2] + ... + E[X_{log_2n}]$，所以 $E[X] \leq 3(logn)^2$，成功證明了 `20.7 A.` 一開始的假想推論！
#### 20.7 B. Higher Dimensions and Other Exponents
- **The Analysis in Two Dimensions**
    - 當拓展到其他 dimension 維度，$p =$ underlying dimension，searching 的效果最好
    - 在 $2$ 維的世界，距離 target $\frac{d}{2}$ 數量的 nodes 會跟 $d^2$ 成正比
        - 為了跟平方項抵銷，probability 就會跟 $d(v,w)^{−2}$ 成正比
    - 而 normalizing constant $Z$ 依然會跟 $log\ n$ 成正比，與 $d$ 無關
    - ![截圖 2023-12-09 晚上7.40.07](https://hackmd.io/_uploads/B1L7G0WIp.png)
        - 一維的 ring 的結論，可以直接繼續存在於 two-dimensional grid
        - 一步進入到 set 的機率相當大
- **Why Search is Less Efficient with Other Exponents**
    - 以下開始考慮 $q \neq$ best 的情況，也就是不等於 dimension 數
    - ![截圖 2023-12-09 晚上8.19.47](https://hackmd.io/_uploads/BkHuiA-IT.png)
        - 以 dimension 為 $1$、$q=0$ uniformly 舉例（其他範例也亦然）
        - $K$ 是距離目標 $t$，$\sqrt n$ 以內所有 node 的 set
        - $K$ 範圍外的一點 $v$ 想要 long-range contact 到 $K$ 範圍內的一點機率為
            - 點的個數 \* 點的機率
            - $2\sqrt n * \frac{1}{n} =\frac{2\sqrt n}{n} = \frac{2}{\sqrt n}$
        - 因此我們會需要至少 $\frac{\sqrt n}{2}$ steps 才能找到一個 node 它的 long-range contact in $K$，at least proportional to $\sqrt n$
        - 所以在步數需要很多才能 access 到 long-range contact in $K$ 的情況，我們只能利用 local contacts 一步一步走很久才能走到 $K$
        - 在其他 $0<p<1$ 的情形下，都會遇到這樣的情況
    - 此外，若 $p > 1$，long-range contact 的機率提升很多，但問題是 long-range contact 的距離反而會太短，一樣需要花費大量時間才能抵達 $K$
    - 總而言之，當 exponent $p \neq 1$, 就會有一個 constant $c > 0$ 讓到達目標的 expectation step 跟 $n^c$ 成正比，$c$ 取決於真實的 $p$ 的大小


## 21. Epidemics
- 這一章在研究流行病學，不僅涉及生物學問題，還包括社會學問題
### 21.1 Diseases and the networks that transmit them
- 傳染病的傳播模式不僅取決於
    - 病原體的特性（如傳染性、感染期長度和嚴重程度）
    - 還取決於受影響人群中的網絡結構。人際社交網絡（記錄誰認識誰）在很大程度上決定了疾病如何從一個人傳播到另一個人
- Epidemics 藉由病毒與社群網路傳播
    - 所以人跟人有接觸，那就有可能傳染
    - 傳播是 random 的，不能夠自己做 decision
- Idea 或 innovation 的傳播稱為 social contagions
    - 人們可以自己決定要不要接收
### 21.2 Branching processes
- 先介紹一個簡單的模型 Branching process model，來看看他的結果
- 傳播機率為 $p$、每一個 wave 傳播給 $k$ 個人
- ![截圖 2023-12-08 下午1.45.12](https://hackmd.io/_uploads/HJYd6XxI6.png)
    - 每波都會有三個接觸者，但不一定有傳染
    - 左下的 probability $𝑝$ 比較強，容易傳染
    - 右下的 probability $p$ 比較弱，就不容易傳染
- Branching process model 只有兩種可能
    1. 直到一個 wave 就停止繼續傳播
    2. 無止盡的一直傳播下去
- $𝑅_0=𝑝×k$
    - $R_0$ 的意義就是，每一個染疫的人，會再傳染給多少人
    1. 如果 $𝑅_0 \leq 1$，the disease 在經過一定的 waves 之後會停止
    2. 如果 $𝑅_0 > 1$，每一個 wave 至少會有一個人染病
    - 所以 $R_0$ 在處於 $1$ 附近時非常關鍵，儘管只有一點點改善，都會對傳染並有極大的影響
### 21.3 The SIR epidemic model
- SIR 的意義
    - Susceptible 健康、但有風險被傳染
    - Infectious 被傳染的、也有能力去傳染人
    - Removed 痊癒或過世、不可能二次感染
- ![image](https://hackmd.io/_uploads/SJtneNxIa.png)
- ![截圖 2023-12-08 下午2.02.38](https://hackmd.io/_uploads/rJCKZ4gIT.png)
    - (紅色加框為 $I$、紅色為 $R$、白色為 $S$)
    - 一開始大多人都是 $S$ 狀態
    - 在 $I$ 狀態的人，會維持 $t_i$ 的時間，在時間內有機率 $p$ 會傳染給別人
    - $t_i$ 的時間後，node 會進入 $R$
- Extensions to the SIR model
    - 不同階段有不同的傳染機率
    - 傳染機率跟 edge 的性質有關
    - 感染期為隨機長度，被感染的節點在感染期間的每一步都有一定的機率 $q$ 恢復
    - 等等其他的設定
- The role of the basic reproduction number
    - 前面講到 $R_0 > 1$ 就會一直傳染下去，但這個假設結構為 tree
    - 這裡使用別的結構，證明 $R_0$ 的 claim 為錯誤
    - ![截圖 2023-12-08 下午2.10.29](https://hackmd.io/_uploads/SJfDQVgUT.png)
    - ![image](https://hackmd.io/_uploads/H1JkxdB8a.png)
        - die out 的機率
        - $第一層 dies\ out + 第二層 dies\ out + ...$
        - 故 $R_0>1$ 還是 dies out
- **SIR epidemics and percolation**
    - ![image](https://hackmd.io/_uploads/r1BgQOHU6.png)
    - 每一個邊都會根據其機率，先預丟銅板，決定會不會成功傳
    - 接著才真的開始一步一步傳播、滲透 percolation
    - 但有沒有先預丟不會影響結果

### 21.4 The SIS epidemic model
- 沒有 R 狀態，得了免疫期可能很短、得了會再得
- 狀態圖：![image](https://hackmd.io/_uploads/rJ8QVdBIp.png)
- 利用時間軸分類：![image](https://hackmd.io/_uploads/ryApVuH8a.png)

### 21.5 Synchronization
- **The SIRS Epidemic Model**
    - 用於模擬疾病在感染個體後提供暫時性免疫的情況
    - $SIRS$ 模型將 $SIR$ 和 $SIS$ 模型的元素結合在一起，使得感染後的個體在返回易感（S）狀態前，會經歷一段移除（R）狀態。
    - 節點在流行病進程中會按照 $S-I-R-S$ 的順序經歷這些階段
- **Small-World Contact Networks**
    - 在這種網絡中，暫時性免疫可以在網絡的局部地區產生振蕩現象，隨著大量感染集中於特定區域，其後跟隨著免疫的區域。
    - 然而，要使這種振蕩如果要在整個網絡層面產生大規模波動，疾病的爆發必須在不同地方大致同時發生。
    - 一個自然的機制是擁有豐富的長距離連接的網絡，這些連接將網絡中相隔較遠的部分連接起來。
- **模型討論**
    - 根據前方 20 章的 Watts 環形模型結構來討論
    - 機率 $c$ 控制了網絡中作為 long-range contact 的比例
        1. 當 $c$ 非常小時，疾病通過網絡的傳播主要通過短距離局部邊進行，因此網絡一部分的疾病爆發永遠無法與其他部分協調。
        2. 隨著 $c$ 增加，這些爆發開始同步，並且由於每次爆發產生大量具有暫時免疫的節點，因此隨後會出現低谷。
        - ![截圖 2023-12-14 下午3.13.15](https://hackmd.io/_uploads/SJGXimuU6.png)
- **實驗研究**
    - 梅毒的盛行率呈現出在 8-11 年周期內的顯著振蕩，而淋病則幾乎沒有周期性行為。然而，這兩種疾病影響相似的人群，並且應該受到非常相似的社會力量影響。
        - 這些差異與梅毒感染後賦予有限的暫時性免疫的事實相符，而淋病則不會。
    - 流行病同步化研究的進一步方向包括試圖模擬更複雜的時間現象
        - 例如，有關麻疹等疾病的數據顯示，要解釋這些性質，僅僅長距離接觸是不夠的，有可能跟免疫接種、預防計劃和其他醫療干預如何利用這些時間特性來影響結果。

### 21.6 Transient Contacts and the Dangers of Concurrency
- 在疾病的傳播裡，有時候我們也需要去考慮網路交互作用的時間
- 如性傳染病，就會因為多伴侶、不同時間，產生出不同可能的結果
- ![截圖 2023-12-14 下午3.42.53](https://hackmd.io/_uploads/ryp-G4_IT.png)
    - edge 上的數字範圍表示交互作用的時間
    - 假設 $u$ 一開始的帶原者
        - 那左圖就有可能會傳染給 $y$
        - 右圖就不會
### 21.7 Genealogy, genetic inheritance, and mitochondrial Eve
- 每個人都連到自己的母親，母親也去連母親的母親
- 那大家會連到同一個人嗎？
- ![image](https://hackmd.io/_uploads/rkoM8OBIT.png)
    - 使用粒線體內的 DNA（粒線體只有媽媽遺傳的），證明會！
    - 大約在 $10$ 到 $20$ 萬年前有 Mitochondrial Eve 粒線體夏娃
    - Mitochondrial Eve 粒線體夏娃，但她可能不是唯一一個女性，可能其他同時期的女人絕種了
- ![image](https://hackmd.io/_uploads/S1uJOdS8T.png)
    - current generation 生小孩
    - 也可以看成 new generation uniformly 挑媽媽
- Wright-Fisher model 維度變更大
    - ![image](https://hackmd.io/_uploads/ByTwuuSUT.png)
    - ancestries line，換一下位置，可以清楚找到共同祖先
        - ![image](https://hackmd.io/_uploads/rJDFO_S8T.png)

### 21.8 Advanced material: analysis of branching and coalescent processes
#### A. Analysis of branching processes
- $𝑋_𝑛$ 是在 layer $𝑛$ 被感染的人數
- $𝑋_𝑛$ 的期望值 $𝐸[𝑋_𝑛]=(𝑅_0)^𝑛$, where $𝑅_0=𝑝*𝑘$，證明可以見下
- 此外，我們定義
    - $𝑞_𝑛=Pr⁡(𝑋_𝑛≥1)$ 表示在第 $n$ 層的個數大於 $1$ 的機率
    - $q^* = lim_{n\rightarrow\infty}P_r⁡(𝑋_𝑛≥1)$
- $𝐸[𝑋_𝑛]=(𝑅_0)^𝑛$ 的證明
    - 定義 $𝑌_{𝑛𝑗}$ 是一個 random variable
        - 等於 $1$ 時，表示在 layer $n$ 的第 $j$ 個 node 被感染
        - 等於 $0$ 則反之
    - 所以我們可以得知
        - $𝑋_𝑛=𝑌_{𝑛1}+𝑌_{𝑛2}+⋯+𝑌_{𝑛𝑚},\ 𝑚=𝑘^𝑛$
            - 第 $n$ 層的 $X$ 就是由每一個 $Y$ 所決定 
        - $𝐸[𝑋_𝑛]=𝐸[𝑌_{𝑛1}]+𝐸[𝑌_{𝑛2}]+⋯+𝐸[𝑌_{𝑛𝑚}]$
            - 期望值也可以由此表示
        - ![截圖 2023-12-14 下午4.47.06](https://hackmd.io/_uploads/BJof-SOI6.png)
            - 由圖可知，當 node $j$ 被傳染時，他的祖先的道路也都要開通
            - 所以 $𝐸[𝑌_𝑛𝑗]=1×Pr(𝑌_{𝑛𝑗}=1)+0×Pr(𝑌_{𝑛𝑗}=0)=Pr (𝑌_{𝑛𝑗}=1)=𝑝^𝑛$
        - ![image](https://hackmd.io/_uploads/H1yXGSOUa.png)
            - 因為第 $n$ 層，共有 $k^n$ 個 node
            - 所以 $𝐸[𝑋_𝑛 ]=𝑝^𝑛 𝑘^𝑛=(𝑝𝑘)^𝑛=𝑅_0^𝑛$
- 不等式
    - 根據公式
        - ![截圖 2023-12-07 晚上11.56.23](https://hackmd.io/_uploads/B14NoPkL6.png)
        - ![截圖 2023-12-07 晚上11.55.56](https://hackmd.io/_uploads/r1FfiwyIp.png)
    - 可以得知第一項 $P_r[X_j \geq1]$ 就是 $q^*$ 
        - 所以 $P_r⁡(𝑋_𝑛≥1)=q^*\leq{E[X_n]}$
- 以下要證明
    - 如果 $R_0 < 1$ 則 $q∗ = 0$
    - 如果 $R_0 > 1$ 則 $q∗ > 0$
##### A.1. 當 $R_0<1$ 時
- 因為 $E[X_n]=(𝑅_0)^𝑛$，所以 $lim_{n\rightarrow\infty}E[X_n] = 0$
- 再根據 $q^*\leq{E[X_n]}$
- 可以得知 $q^* = 0$
##### A.2. 當 $R_0 > 1$ 時
- 可以知道當 $n\rightarrow \infty, 𝑅_0>1$ 時，$𝐸[𝑋_𝑛]=(𝑅_0)^𝑛$ 也會趨近於無窮大
    - 但這不足以確認 $q^*$ 也會趨近於無窮大
    - 例如
        - 機率 $2^{−𝑛}$ 最後一層 node 數 $𝑋_𝑛=4^𝑛$
        - 其他情況 最後一層 node 數 $𝑋_𝑛=0$
        - $𝐸[𝑋_𝑛 ]=2^𝑛 \rightarrow \infty$
        - 但 $Pr⁡(𝑋_𝑛≥1)=2^{−𝑛} \rightarrow 0$
- 因此 $𝑞^∗$ 需要進行更多的分析
    - 我們沒辦法單純用 $p$、$k$ 來表示 $q_n$
    - 但可以多利用 $q_{n-1}$ 來表達
- 如何利用$p$、$k$、$q_{n-1}$ 表達 $q_n$？
    - ![image](https://hackmd.io/_uploads/SyDu_SOUp.png)
        1. 從 blue tree 的角度，最底層 (blue tree 的第 $n$ 層) 有 infected node 的機率為 $q_n$
        2. 從 red tree 的角度，先看到最左邊的 tree，如果他能夠傳到最後一個 layer (red tree 的第 $n-1$ 層) 的機率是 $𝑝𝑞_{𝑛−1}$
            - 雖然可以找出 $1$ 個 tree 的情況，但我們有 k 個 tree，不能正面去表述
            - 所以反面來說，$1$ 個 tree 不能到達最底層的機率是 $1−𝑝𝑞_{𝑛−1}$
            - $k$ 個都不能抵達的機率是 $(1−𝑝𝑞_{𝑛−1})^k$
            - 所以最底層能夠最少有一個的機率是 $1-(1−𝑝𝑞_{𝑛−1})^k$
        - $1.+2. \Rightarrow q_n = 1-(1−𝑝𝑞_{𝑛−1})^k$
        - 我們假定 root 一開始是 infected 所以表示 $q_0=1$
- 定義 $𝑓(𝑥)=1−(1−𝑝𝑥)^𝑘$
    - $𝑞_𝑛=𝑓(𝑞_{𝑛−1})$，代表我們可以一步一步一直代值，去 trace 出最後的機率 $q$，也就是經過漸進的描點 $1, f(x), f(f(x)), f(f(f(x)))...$
    - 三個畫圖條件
        1. 因為機率 $q$ 會介於 $0$ 到 $1$ 之間，代值進入後可得，$f(0) = 0$ and $f(1) = 1−(1−p)k < 1$
        2. 如果我們對 $f(x)$ 微分 $f′(x) = pk(1 − px)k$，知道在 $0$ 到 $1$ 之間，是正值但遞減
        3. 在 $x=0$ 時 $f′(x) = pk = R_0$，也就是圖形的斜率，根據討論的條件，我們知道 $R_0 > 1$
    - 根據 $1.+2.+3.\Rightarrow$ 得出圖形，並得知會和 $y=x$ 有交點
        - ![截圖 2023-12-14 晚上8.11.27](https://hackmd.io/_uploads/HJ6gWOuLa.png)
        - 如果我們 follow 圖形上的紅色虛線，從 $(1,1)\rightarrow(1,f(1))\rightarrow(f(1),f(1))\rightarrow(f(1),f(f(1)))$
        - 其實就是 $(q_0,q_0)\rightarrow(q_0,q_1)\rightarrow(q_1,q_1)\rightarrow(q_1,q_2)$
        - $\Rightarrow[1,f(1),f(f(1)),...] = [q0,q1,q2,...,]$
        - 根據圖形，我們就可以知道，當 $n\rightarrow\infty$，那 $q_n$ 就會趨向一個 positive number
        - 所以得證：$R_0 > 1$ 則 $q∗ > 0$
- 補充，如果 $R_0 < 1$，也可以用此方式來解
    - 三個畫圖條件
        1. 不變
        2. 不變
        3. 更動，在 $x=0$ 時 $f′(x) = pk = R_0$，也就是圖形的斜率，根據討論的條件，我們知道 $R_0 < 1$
    - 得到圖形![截圖 2023-12-14 晚上10.46.42](https://hackmd.io/_uploads/SJkvH5u8a.png)
    - 根據圖形可以得到結論，$R_0 < 1$ 時，當 $n\rightarrow\infty$，那 $q_n$ 就會趨向 $0$


#### B. Analysis of coalescent processes
- ![截圖 2023-12-20 下午2.40.54](https://hackmd.io/_uploads/r1TFhbxPT.png)
    - 接著我們想要計算，多久所有人在 backward trace 的時候，會發生 collision 的時間，這就稱作 coalescent process
    - 而因為計算全部的點太過困難，我們只取 $k$ 個點來判斷何時會有相同的祖先，也就是 coalescent 發生，而假設總數量 $N>>k$
- **Lineages Collide in One Step**
    - ![截圖 2023-12-23 晚上10.27.06](https://hackmd.io/_uploads/ByIBCPVwT.png)
    - 在展開之後，我們可以得到![截圖 2023-12-23 晚上11.00.29](https://hackmd.io/_uploads/rk9fUdVPa.png)![截圖 2023-12-23 晚上11.05.09](https://hackmd.io/_uploads/HymNwOVD6.png)
    - 當 $N$ is much larger than $j$，後項根據前項的大小，可以忽略，因此能夠寫成![截圖 2023-12-23 晚上11.07.17](https://hackmd.io/_uploads/r1Mhv_Vwp.png)
- 我們根據機率
    - ![截圖 2023-12-24 凌晨1.09.06](https://hackmd.io/_uploads/ry1BNcNwa.png)
        - 一個 two-way collision 的機率是 $\frac{j^2}{N}$
    - ![截圖 2023-12-24 凌晨1.08.29](https://hackmd.io/_uploads/S1y7VqVP6.png)
        - 兩個 two-way collision 的機率是 $\frac{j^4}{N^2}$
        - 一個 three way collision 的機率是 $\frac{j^3}{N^2}$
    - 可以得知在每一層不可能會有 more than a single two-way collision
- 可以得到示意圖![截圖 2023-12-23 晚上11.51.40](https://hackmd.io/_uploads/rytMMYVvT.png)
    - 當目前有 $k$ 個 distinct lineages，他的產生一個 collision 的機率為 $\frac{k(k−1)}{2N}$
    - 有 $k-1$ 個時，機率為 $\frac{(k-1)(k−2)}{2N}$
    - 直到最後一個的機率為 $\frac{2}{2N} = \frac{1}{N}$
- 可以列示![截圖 2023-12-24 凌晨12.00.15](https://hackmd.io/_uploads/SyoMNt4va.png)![截圖 2023-12-24 凌晨12.10.40](https://hackmd.io/_uploads/Hy3FUKNwp.png)
    - $W_j$ 是一個 random variable 表示有 $j$ distinct lineages 時所需要經過的 generation
    - 每一個 $W_j$ 可以想成第一次發生的 collision 開始，慢慢累積到目前恰好有 j distinct lineages 所需要的 generation
    - 每一個 generation 的機率近似於 $p = j(j−1)/2N$
- 所以可以改列式，近似的表示方法![截圖 2023-12-24 凌晨12.20.02](https://hackmd.io/_uploads/H1R2OtVwa.png)![截圖 2023-12-24 凌晨12.21.26](https://hackmd.io/_uploads/rkzzttEva.png)
- 近似的 random variables $X_j$，可以想成我們有一個硬幣，機率 $p = j(j−1)/2N$ 會產生正面，而我們想要知道大概要躑多少次 expected number 才能真的出現一次正面
- 根據公式
    - ![截圖 2023-12-07 晚上11.56.23](https://hackmd.io/_uploads/B14NoPkL6.png)
    - ![截圖 2023-12-07 晚上11.55.56](https://hackmd.io/_uploads/r1FfiwyIp.png)
    - ![截圖 2023-12-24 凌晨12.35.26](https://hackmd.io/_uploads/Hy98hF4w6.png)
        - 也就是超過 $1$ 次的機率 $+$ 超過 $2$ 次的機率$($第一次沒中 $1-p)+$ 會超過 $3$ 次的機率$($連兩次沒中 $(1-p)^2)+...$
        - 這個結果也很 intuitive，因為如果機率是 $1/3$，結果可能就是 $3$ 次才會看到正面
    - 因此 ![截圖 2023-12-24 凌晨12.49.46](https://hackmd.io/_uploads/B1d3y94vT.png)![截圖 2023-12-24 凌晨12.50.58](https://hackmd.io/_uploads/S11WeqEDa.png)![image](https://hackmd.io/_uploads/rJCtx5EwT.png)
    - 得到結果![截圖 2023-12-24 凌晨12.54.22](https://hackmd.io/_uploads/HJ2ag5NDa.png)
    - 我們可以根據結果得知
        1. 當 $k$ 很大時，expected number 幾乎只跟 $N$ 有關
        2. 如果把 $X$ 分解成 $X_{k} +X_{k-1} +···+X_{2}$，發現時間花最多的會是在接近 $k$ 的 $X$，$X_2$ 附近的速度很快（需要的 generation 很少）
        3. ![截圖 2023-12-24 凌晨1.18.59](https://hackmd.io/_uploads/rkpcI5Vwp.png)
## #參考資料
- [國立清華大學資訊工程學系 李端興教授](http://bcc.cs.nthu.edu.tw/lds_profile/index.htm)：[2023 Fall 11210CS 530600 社群網路 Social Networks](http://bcc.cs.nthu.edu.tw/pages/111-social-networks.html)
- [David Easley and Jon Kleinberg, “Networks, Crowds, and Markets: Reasoning about a Highly Connected World,” Cambridge University Press, 2010.](https://www.cs.cornell.edu/home/kleinber/networks-book/networks-book.pdf)

