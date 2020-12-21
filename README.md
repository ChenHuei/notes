# note

### Nginx

About Ngnix:

1. web server (回覆 web client 端發送的請求)

web client (Chrome) 造訪透過 web server 啟動的 port 取得 response 並進行 render 

![client-server 架構](https://miro.medium.com/max/700/1*mRC9m1M4lKc9kq8s2yyWNg.png)


2. web server vs. application server

web server：Nginx、Apache，負責處理靜態資源，負載平衡、代理
application server：Node、Go 啟的 web server，可處理靜態及動態資源

> 如果 application server 已經包含 web server 了，那還需要 web server 做什麼？

1. 負載平衡：負責分發高流量的 request 到不同 application server 分擔請求
2. 反向代理：client 只會得知反向代理的 IP address，而不會知道背後是哪台 application server 在處理 (保護真實 server)

更進一步還可設定：靜態資源 cache、URL Rewrite、Https 憑證和安全設定 (黑名單...)

** 正向代理：server 只會知道代理 client 的 IP address 而不知道是哪個 client

3. 加上 web server 在處理靜態資源的能力是遠高於 application serve

> 因此在現在前後端分離須處理大量靜態資源的情況下，就非常適合使用 web server 這類服務。

#### 2020/12/07

###### 參考來源

- https://medium.com/starbugs/web-server-nginx-1-cf5188459108
- https://ithelp.ithome.com.tw/articles/10221704
- https://zh.wikipedia.org/wiki/Nginx
- https://zh.wikipedia.org/wiki/%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86

### VScode snippet

#### 2020/12/14

### SVG sprite

#### 2020/12/21
