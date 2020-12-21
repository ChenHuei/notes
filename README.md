# note

### Nginx

About Ngnix:

1. web server (回覆 web client 發送的請求)

web client (Chrome、Safari...) 造訪透過 web server 啟動的 port 取得 response 並進行 render

![client-server 架構](https://miro.medium.com/max/700/1*mRC9m1M4lKc9kq8s2yyWNg.png)

2. web server vs. application server

web server：Nginx、Apache，負責處理靜態資源，負載平衡、代理

application server：Node、Go 啟的 web server，可處理靜態及動態資源

> 如果 application server 已經包含 web server 了，那還需要 web server 做什麼？

Nginx

1. 負載平衡：負責分發高流量的 request 到不同 application server 分擔請求
2. 反向代理：client 只會得知反向代理的 IP address，而不會知道背後是哪台 application server 在處理 (保護真實 server)

更進一步還可設定：靜態資源 cache、URL Rewrite、Https 憑證和安全設定 (黑名單...)

\*\* 正向代理：server 只會知道代理 client 的 IP address 而不知道是哪個 client

3. 加上 web server 在處理靜態資源的能力是遠高於 application serve

> 因此在現在前後端分離須處理大量靜態資源的情況下，就非常適合使用 web server 這類服務。而 Nginx 又比 Apache 更有效能。

#### 2020/12/07

###### 參考來源

- https://medium.com/starbugs/web-server-nginx-1-cf5188459108
- https://ithelp.ithome.com.tw/articles/10221704
- https://zh.wikipedia.org/wiki/Nginx
- https://zh.wikipedia.org/wiki/%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86

### VScode snippet

Code snippets are templates that make it easier to enter repeating code patterns, such as loops or conditional-statements.

select `User Snippets` under `File` > `Preferences` (`Code` > `Preferences` on macOS), and then select the language for which the snippets should appear, or the New Global Snippets file option if they should appear for all languages.

```javascript=
// in file 'Code/User/snippets/javascript.json'
{
  "For Loop": {
    "prefix": ["for", "for-const"],
    "body": ["for (const ${2:element} of ${1:array}) {", "\t$0", "}"],
    "description": "A for loop."
  }
}
```

In the example above:

1. `For Loop` is the snippet name. It is displayed via IntelliSense if no description is provided.
2. `prefix` defines one or more trigger words that display the snippet in IntelliSense. Substring matching is performed on prefixes, so in this case, "fc" could match "for-const".
3. `body` is one or more lines of content, which will be joined as multiple lines upon insertion. Newlines and embedded tabs will be formatted according to the context in which the snippet is inserted.
4. `description` is an optional description of the snippet displayed by IntelliSense.

Personal case:

```javascript=
{
  "Vue Typescript Class": {
    "scope": "vue",
    "prefix": "vtc",
    "body": [
      "<template>",
      "  <div>",
      "    ",
      "  </div>",
      "</template>",
      "",
      "<script lang=\"ts\">",
      "/**",
      "  *  @author leo.chen ${CURRENT_YEAR}-${CURRENT_MONTH}-${CURRENT_DATE}",
      "  *  @description description",
      "  *",
      "  *  @summary summary",
      "  */",
      "",
      "import { Component, Vue } from 'vue-property-decorator';",
      "",
      "@Component",
      "",
      "export default class ${1} extends Vue {",
      "  ",
      "}",
      "</script>",
      "",
      "<style lang=\"scss\" scoped>",
      "  ",
      "</style>"
      ],
    "description": "vue typescript class"
  }
}
```

#### 2020/12/14

###### 參考來源

- https://code.visualstudio.com/docs/editor/userdefinedsnippets

### SVG sprite

 通常在專案中使用 svg 會有以下兩種方式

1. Using SVG as an `img`

利用 `img` 標籤來引入，此時 SVG 被視為一個圖檔載入

```HTML
<img src="icon.svg" />
```

優點：易讀

缺點：當相同 icon 有其他顏色的需求時，就會需要不同顏色的 SVG !!

2. Inline SVG

直接將 `svg` 標籤放進 Html 結構中

```HTML
<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 16 16">
  <g fill-rule="evenodd" stroke="#EA475B" stroke-linecap="round">
    <path d="M8 3.5v9M4.5 9.5l3.5 4 3.5-4"/>
  </g>
</svg>
```

優點：解決相同 SVG 改變顏色的問題

缺點：難讀

>  而這時候，SVG sprite 將可以綜合以下兩種方式的優點，成為我們的救星！

根據[官方文件](https://github.com/JetBrains/svg-sprite-loader)的說明，配置 webpack 之後，將可把各個 icon 打包成同一個檔案 (`解決多個網路請求`)，並可透過父層給予 icon name and style 進行 svg 的圖片切換和改變顏色

> 須將各個 SVG 檔裡的 fill 或 stroke 改成 currentColor (類似 inherit 的功用) 


#### 2020/12/21

##### 參考文件
- https://medium.com/@f820602h/%E5%9C%A8-vue-%E8%81%B0%E6%98%8E%E4%BD%BF%E7%94%A8-svg-icon-87a172a1b47b
- https://github.com/JetBrains/svg-sprite-loader
