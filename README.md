# zhihu403_HeaderEditor

## 遇到什麼問題

打開知乎時有些圖片403，無法顯示

## 解決方法

Header Editor 插件
https://chrome.google.com/webstore/detail/header-editor/eningockdidmgiojffjmkdblpjocbhgh

在HeaderEditor的Export and import中下載本github的HeaderEditor.json即可

## 解決思路

查看知乎的html代碼發現以下CDN:

```html
<link rel="dns-prefetch" href="//static.zhimg.com">
<link rel="dns-prefetch" href="//pica.zhimg.com">
<link rel="dns-prefetch" href="//picx.zhimg.com">
<link rel="dns-prefetch" href="//pic1.zhimg.com">
<link rel="dns-prefetch" href="//pic2.zhimg.com">
<link rel="dns-prefetch" href="//pic3.zhimg.com">
<link rel="dns-prefetch" href="//pic4.zhimg.com">
<link rel="dns-prefetch" href="//static.zhimg.com">
```

發現使用picx為域名的圖片可以訪問，其他就不可以。其他域名的圖片也可以換成picx進行訪問。那麼，是否有一個方法可以當打開網頁時把pica,pic1,pic2,pic3,pic4換成picx以訪問圖片。

使用Header Editor推行重定向，規則如下:

```json
 "request" : [
        {
            "enable": true,
            "name" : "zhihu403",
            "ruleType": "redirect",
            "matchType": "regexp",
            "pattern": "^http(s?):\/\/(pica|pic1|pic2|pic3|pic4)\\.zhimg\\.com/(.*)",
            "exclude": "",
            "isFunction": false,
            "action": "redirect",
            "to": "https://picx.zhimg.com/$3",
            "group": "重定向"
        }
    ]
```
其實就是用了正則表達式

可以用這個網址來測試效果:
https://zhuanlan.zhihu.com/p/532806181



