---
layout: post
title: "Note: Seminar - A Comparison Study on Semantic Web Services and e-Business"
date: 2012-09-27 15:12
comments: true
categories: 
- Seminar Notes
---

講者：大同大學系主任葉慶隆教授

* ebXML - E-Business Standard 
* Web Services = WWW + XML ( in ebXML )
* HTTP, HTML, URI 即是 WWW 的基礎，構成龐大的應用
* XML technologies : Namespace, Schema, Transformation, Publishing, Query, Security
* Web Service = SOAP, WSDL, UDDI: 後兩者是遠端服務呼叫的相關技術
* 這些的問題都在於缺乏語意。XML 有清楚的文法，可是語意依然缺乏

---
* ebXML 以 Web Services 做基礎，把商業程序與 IT 的職責切開，中間用介面互通
* CPPA: 描述供應商與需求方的一堆程序與需求，即是可以提供的功能介面彼此協議
* BPSS: 各參與角色的商業協同合作
* Semantics Web Services Standard - WSMO 標準
* RDF：類似關聯資料那種作法，表達關聯。而到了現代可以用 XML/HTML5 的語意功能把一個物事的關係放在文件裏面
* Semantic Web: 現在是資料存在各種格式中，而經過映射轉換，變成比較抽象的格式，也就是 RDF ER 模型
* 因為 RDF 的預設範圍是全球化的，因此可以很容易與其他檔案合起來協作
* Semantics Web Services 指軟體用語意標籤，使得機械處理可以知道其所要的服務如何取得，也可以互相組裝成完整的服務
* Choreography 是描述文件流的自動狀態機與規則語言

---
* ebXML 與 WSMO 的標準關聯
* 事實上 ebXML 所定義的 Core Components 都轉成 Semanitic 技術所可以處理的 Ontology 格式
* CPPA -- Goal || BPSS -- Choreography || Abstract State Machine 可以描述各代理人參與者 
* 可以把 FSM 轉成 ASM 規則語言，類似一連串流程的語言
* Rule-base ASM 可以取代 ebXML 的所謂 schema-based 、圖畫式的 BPMN 流程描述

---
* 做這些最主要是要克服多量應用所產生格式，全球無法互通的問題，也很難在缺少語意的情況下做應用的發展
* 關鍵字等非語意技術可以達到足夠的應用品質，在不需要的時候當然就夠了。可是重點是電腦可以更加的利用，而不像現在必須要人的介入 
* 服務的描述功能等比較抽象的規格，實際上與技術層面的函式呼叫等是有距離的

---
* (私人感想)：這類東西的辭彙都太多了...而且與實際的用途到底有沒有接起來 
* 我個人深切的希望這些過大與過度制式化的標準可以輕一點。讓那些有需要如此制式化的官僚與商業體系去運作他們的標準，
衝在前面的開拓者需要比較輕的工具，讓這一切用意良好的原石可以真正琢磨出價值。這種龐大的東西往往就像所謂玻璃鎚那樣(from "Better,Faster,Lighter Java")。


