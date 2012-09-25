---
layout: post
title: "Note: Compiler Design #2"
date: 2012-09-25 21:57
comments: true
categories: 
- Course Note
---

**原稿遺失**，補記一些重點

---
* Lexeme: 語法剖析的元素
* 語法剖析出來的 Token 代表 key/value ，即是該 Lexeme 屬於那一類 Token ，其值為何
* Identifier 就是一大類 Token 。而如 IntegerConstant 那樣，可能會有很多類中有很多種值
* Keyword/Reserved Word 差異：前者有先定義但可重載；後者不可重載

---
* Formal Language 就是研究這些 Lexeme 對應到的類別之間關係
* 單字構成字串，字串符合文法者稱之句子。所有（有可能無限可數）句子構成語言
* Formal Language 的規則確保所建構出來的語言，針對任意字串都是可決定其是否為句子的
* Regexp 用以從文法建構出句子；而 Compiler 則是從句子辨認出文法

---
* 自動狀態機分為確定與不確定。兩者的差異在於其中的狀態移轉，是否存在同輸入而多個可能移轉的狀態
* 確定的版本，雖然可以允許有多個結束狀態，但一定要在輸入全部使用完畢時達到結束狀態，才算完成
* 不確定者，其遇到輸入有多個可能移轉時，要「執行」全部可能的移轉。而只要其中一個到達結束狀態時輸入也剛好完畢，就算成功
* 前者所述，如果其中一個移轉到達結束狀態，但輸入還未完畢，其他可移轉者要繼續移轉
