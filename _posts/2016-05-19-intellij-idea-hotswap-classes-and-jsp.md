---
layout: post
title: IntelliJ IDEA 設定 Hotswap Classes and Jsp
modified:
categories: 
description:
tags: []
image:
  feature:
  credit:
  creditlink:
comments:
share:
date: 2016-05-19T05:07:05-04:00
---

在 IDEA 中設成存檔後，自動將異動的 jsp 與 classes 或其他 resources 安裝到執行中的 Application Server，可依以下步驟進行

1. 打開 "Run/Debug Configurations" 設定
2. 切到 "Deployment" Tab
3. "Deploy at Server Startup"，移除 app-name:war
4. 按下 add 按鈕，新增 "artifact"，選擇 app-name:war exploded
5. 切到 "Server" tab
6. 將 "On frame Deactivation" 設定調整為 "Update resources" 或 "Update Classes and Resources"
    - Update resources: 所有變動的 resources 都會更新到 Application Server
    - Update classes and resources: 會更新所有變動的 resources；而變動的 classes 會重新 compile。要特別注意的 assets 的更新方式要看不同的 Application Server。以 Tomcat 為例會自動重新更新 html/xhtml 與 jsp 檔案，但是 servlet 與 jsp 對應的 classes 則不會被自動更新，必需使用 dynamic classloader
7. 你也可以自行調整按下 "Update" 按鈕之後的行為

現在只要修改任何檔案後且焦點離開 IDEA 後，IDEA 會自動將變動的檔案更新到 Application Server，仔細觀查可以在 status bar 看到 hotswap 更新狀態的訊息。最後重新在 browser 重新更新就看到最新的結果

另外有比較方便的作法是結合 Tomcat 與 On frame deactivation 的方式 ，這種方式可以讓me deactivation 被更新，或透過 Update 按鈕更新異動的 classes

