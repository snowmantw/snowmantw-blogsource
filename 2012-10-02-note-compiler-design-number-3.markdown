---
layout: post
title: "Note: Compiler Design #3"
date: 2012-10-02 14:16
comments: true
categories: 
- Lecture Notes
---

複習提示

* Regexp 就是 Token 的規則：合乎規則的才會到同類，例如 Number
* Context-Free Grammar
* 語法不處理是否有 main function 等議題
* Symbol Table 指得是所有 Symbol 的值、Address、Type, 保留字也可能放在這邊(如果實作需要)

工具重點

* yywrap() : 如果輸入不只一個檔案，可以處理(遇見 end-of-file)。如果 return 1 就是沒有其他檔案了，return 0 代表還有其他檔案
* yyin/yyout : stdin/stdout
* yytext : 匹配的字串( 全域指標 )。所以如果 yytext+1 ，指到下一個 word
* yyleng : 總字串長度
* Start Conditions: `BEGIN 狀態` 。等於是狀態機中的狀態機。做完之後，回到 INITIAL ( BEGIN INITIAL )

