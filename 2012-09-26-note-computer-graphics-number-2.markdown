---
layout: post
title: "Note: Computer Graphics #2"
date: 2012-09-26 13:10
comments: true
categories: 
- Course Note
---

## OpenGL Programming 基本架構

### 座標系統詞彙

* Clipping: 座標空間中所關注的立方區域，鏡頭唯一關注的區域
* Viewpoint: 繪製的座標與視窗的座標映射。螢幕上的視窗系統透過 Viewpoint 提供了映射的方式
* Project: 立體空間對視窗的投影
* Mesh: Geometry

### OpenGL 歷史

* 繪圖的工業標準，軟硬體接軌的機制
* 最初的版本是把硬體能作到的流程功能做成固定的功能，包括從頂點的立體物件資料，以及平面影像的像素資料，
作個別的修正後柵格化結合（頂點轉像素），最後處理到 Framebuffer 
* 第二版後把頂點轉換 (Vertex Shader) 與像素貼圖 (Fragment Shader) 程式化。之前只能設定狀態並丟給硬體作。程式化代表可以對這些過程的方式套用自己的方式，
不用一定按照預設的硬體方式作
* 第三版引入了 Geometry Shader 。這個流程是位於 Vertex Shader 與 Fragment Shader 中間。另外則是開始有向後相容切割的概念，
即所謂 Full/Forward Compatible Context Type
* 第四版於 Geometry Shader 前又引入兩個流程：Tessellation-Control, Tessellation-Evaluation 。前者是曲線中間可以增加點，因此更細分平滑。
從這邊看出 OpenGL 支援的越多，以前要放出去交給 CPU 運算的部份，就可以用 GPU 去算，增加效能
* 幾何資料之後細化處理另一個好處是頂點資料可以相同數目，但效果更細緻，不會增加頻寬的需求
* OpenGL - { OpenCL, WebGL, OpenGL ES }  

### OpenGL APIs

* 針對每個 OS 與視窗系統的接軌
* GLU 是比起硬體平台上更抽象的，GLUT 則是跨平台的 Toolkit
* 命名慣例：`gl` 代表 OpenGL 提供的功能；`glu` 代表 GLU 提供 
* GL - GLU || OS/Window System - GLX,AGL,WGL ：前者提供繪圖，後者提供輔助視窗必要的功能。GLUT 則是跨兩者
* `gl.h` 一直維持在 OpenGL 1.1 ；因此額外功能需要用 `glext.h` 去增加。但因為硬體實做不一致，所以該函式庫要作手動連結等。而 `glee.h` 就是自動處理的函式庫
* OpenGL 資料型別自訂浮點數等是因為要跨平台

## GLUT and Application 

* 應用結構：主函式中的主迴圈，然後透過事件處理函式去作各功能 
* 應用中都用 GLUT 設定顯示模式（如 RGB）、建立視窗、顯示事件分派函式、鍵盤事件分派函式...最後是呼叫 GLUT 的主迴圈功能
* GLUT 做好視窗的建立與模式後，還需要作 OpenGL 本身的設定。包括設定色彩深度與開啟對應狀態等
* GLUT 的顯示分派函式是用函式指標註冊進 `glutDisplayFunc` 中。這部份當有顯示需求時就會被呼叫
* `glutSwapByffers`: 前景與背景 Buffer 。後面畫完交換到前面用，也就是繪製與顯示是分開的，除非該 Buffer 被推到前面
* 要繪製通常是先清除再顯示。因此在其他的函式中作繪圖，若是之後又執行到有清除的函式，就會沒有顯示效果
* `glFlush`  是強制把繪圖指令都送出。因為 GPU/CPU 溝通上可能有同步的問題，可能 GPU 還沒畫完 CPU 就在執行下一步了。因此會用這個 
* `glBegin` 與 `glEnd` 中間的各指令就是用來畫的繪製區間
* `glutIdleFunc` 動畫時可用。因為若是沒有事件，就只有 Idle 事件
* `glutPostRedisplay` 則是產生一個事件，注意 Post 。執行後，下次進入主事件迴圈時會有一個待處理的顯示事件，因此動畫就可以順著用顯示的函式處理

## Elementary Rendering

### 幾何元件

* OpenGL 有支援幾種基本幾何元件
* 繪製時要注意頂點順序左下開始逆時針
* `glVertex3fv` 為例，命名如下
  * gl: OpenGL 前綴
  * 3: 維度，影響有多少參數
  * f: 傳入資料型別
  * v: 有的話則是傳入陣列（Vector)
* 新的寫法不再用 `glBegin` 等方式描述，而是使用 Buffer 相關的方式
* Buffer 化的表示法是用一個叫做 Display List 的概念去存，然後繪圖的時候直接畫出來

---
* 可以用一些函式作狀態與特色的設定、開閉等 
* OpenGL 座標以左下角作零點，所以滑鼠座標可能要反轉 


