---
layout: post
title: "Note: Computer Graphics #3"
date: 2012-10-03 13:07
comments: true
categories: 
- Lecture Notes
---

## OpenGL programmable pipeline

* 原本的繪圖方式效率不高，雖然以函式呼叫畫頂點接近使用者習慣。 
* Pipeline: Vertex Processing .. Rasterizer .. Fragment Processing .. ( pixels ) 
* 其中 Vertex Shader 先於 Vertex Processing；Fragment Shader 加入 Fragment Processing 流程
* OpenGL 目前先進的概念將程式流程變成下列幾個
  * Create shader programs: 自己去寫 Vertex Shader 與 Fragment Shader
  * Create buffer objects and load data into them: Buffer 物件取代重複執行函式呼叫繪圖的動作。舊有作法因需要大量中斷(切換到 GPU/CPU)，效率不高。
    而那些函式呼叫中的資料現在可以包成 Buffer 物件
  * 連結資料的位置與 Shader 函式

### 用新法表達立體物體

* 表達幾何物體：四個維度資料而不僅是三個
* VBOs: vertext buffer objects
* VAOs: vertext array objects 
* 最基本的形狀是三角形，因此所有形狀都需要換算過，包括頂點數目、色彩數目、點數等
* 像表達例方體，就有 36 個頂點，同樣數目的色彩
* 資料都會先存在 CPU 空間中。像前數裝頂點與顏色的陣列就先是簡單的資料結構
* glGenVertextArrays() 用以於 GPU 空間中建立 VAO
* glBindVertextArray() 是把 VAO 綁上來用
* glGenBuffers() 等函式對 Buffer 的效果亦同
* glBufferData() 則是真正把 CPU 資料送給 GPU，指定了整個 VBO 的資料。glSubBufferData 則是在其中再送
* 接著要使 Vertex Shader 與資料做連結。最後就 glDrawArrays 去顯示
* WebGL 與 OpenGLES 只有新寫法可以用

### Shading Language

* 在 GPU 中執行
* 有一些修飾型別如 in/out ，是因為指定 Vertex Shader 輸出輸入; 而不變部份則是 uniform
* 最簡單 Vertex Shader 
  * 對每個 Vertext 做處理。看不到針對哪個三角形做處理
  * main function
  * in: 要取得哪些資訊，例如 vPosition, vColor
  * out: 要往後階段送的資料，例如 color ( 變數)
  * `in = out` 代表直接導向 in 的資料
  * 最後一定要給 `gl_Position` 賦值指定其位置是否有變化(形變亦算)。因為最主要的是要把其往下傳
* 最簡單 Fragment Shader
  * 語法類似前述 Vertext Shader
  * 位置不重要。因為他已經在 FrameBuffer 裡了。現在要處理的是顏色與其他屬性
* 執行的時候只要呼叫把準備好的資料繪圖就好了。準備好的資料可以用其他軟體做先期處理
* 複雜的 Shader 可以做到諸如加上打光等效果，就可以這些效率程式中做

## 幾何轉換

* 向量對表達幾何物體不夠：沒有座標的概念
* 向量與位置可以轉換，就是座標相減等於新的向量那種作法
* 這就是為何三維之外需要多一個點的資訊作為向量出發點
* P(a...z..) 是所謂的參數表示法。P(a) 代表線或線段
* 光線線段表示：P(a) = Q + a ( R-Q ) ，表示 (R , Q) 之間，a 介於 ( 0 , 1 ) 之間。這之間所有的點就是光線點集。
  * 如果 a == 0 代表 Q 點; a == 1 就是 R 點
* 以前數 PQ 點集可以檢測凸多邊形：若是線段中間有點落在形狀之外就代表不是凸多邊形
* Convex Hull: 所有頂點最大的外圈 
* 格柵化就是依靠著 Convex 特性
* P(a,b) = R+au+bv 定義出三角形, R: 點, u,b: 向量。也可以換成 P(a,b)=R+a(Q-R)+b(P-Q) ，只是把兩點換成向量 Q,R
* Convex Sum of P,Q = S(a) -- 得出線段
* Convex Sum of S(a),R = T(a,b) -- 得出平面(三角形)
* 外積產生法向量，可以作為兩個向量所謂「正向」的方向 
* Frames: 表示成 (P0, v1, v2, v3)。每個向量在其中都可以這組點與基底向量做表示
* 每個其中的點也是相同：用 P0+a1v1+b2v2... 去表示。跟向量很像，但差別在於向量不用參考點，其維度資訊是 0 。
* `Vector = [a1, a2, a3, 0]T`; `Point = [b1, b2, b3, 1]T`; 且還可以表現為 `Point = [wx wy wz w]T` 等同前方式表示
* 這就是所謂 Homogenous Coordinates 。還有一個好處是移動的分量因為在缺少最後一個元素時要多做一次加法，現在可以直接放在矩陣乘法中
* 座標系統的轉換，例如從物體本身的座標，到有其他物體與客觀世界而引入所謂 World Space ，再到按照視線所見等不同的視角，座標就不同的轉換多次
* 轉換中就是以不同的基底去描述同樣的向量
* 先把 Frame 與其轉換的參數用矩陣表示，轉換就可以直接使用相乘(移動、轉動、縮放)
* 所以那個轉換矩陣的產生就很重要
* 乘法中要注意 Column Major 的問題：乘法與其他運算的時候取索引要注意
