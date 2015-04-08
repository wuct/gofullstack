# URL and SEO

## URL 架構

__TL;DR__ 針對國家在地化用 ccTLDs；針對語言在地化 Subdomain with gTLDs

- ccTLDs
    - eg: example.de, example.fr
    - 優點
        - Google 完全資源
        - 網址本身就是個在地化
        - 使用者喜歡，且容易辨認
        - 可在 DNS 指定至離使用者距離近的 server
    - 缺點
        - 貴，不容易買到所有網域
        - cookies, localStorage 不能共用，必須重新驗證 user
        - 如果網站是針對語言做區隔，而不是國家，這不是好選項。比如搜尋引擎可能會認為 .tw 的網站對美國使用者不重要，即使他是台灣人
-Subdomain with gTLDs
    - eg: de.site.com, fr.site.com
    - 優點
        - Google 完全資源
        - 同時適用針對國家或針對語言做在地化
        - 設定簡單
        - 可在 DNS 指定至離使用者距離近的 server
        - cookie 可共用
    - 缺點
        - 使用者可能比較不容易辨認
- Subdirectories with gTLDs
    - eg: site.com/de/, site.com/fr/, etc
    - 優點和缺點
        - 和 Subdomain with gTLDs 相同，除了無法在 DNS 指定 server
- URL parameters
    - eg: site.com?loc=de, ?country=france, etc.
    - 缺點
        - Google 不建議且不資源（Webmaster）
        - 切割網站不容易
        - 使用者難辨認

[Google gTLDs 列表](https://support.google.com/webmasters/answer/1347922?hl=en)

## 相關設定
可用 html header 或 sitemap （擇一）告訴搜尋引擎我們資源的 i18n 網站

### Html Header

```html
<link rel="alternate" hreflang="es" href="http://www.example.com/" />
<link rel="alternate" hreflang="es-ES" href="http://es-es.example.com/" />
<link rel="alternate" hreflang="es-MX" href="http://es-mx.example.com/" />
<link rel="alternate" hreflang="en" href="http://en.example.com/" />

```

[http://googlewebmastercentral.blogspot.tw/2011/12/new-markup-for-multilingual-content.html]()

### Sitemap
```
<url>
  <loc>http://www.example.com/en</loc>
  <xhtml:link
    rel="alternate"
    hreflang="de"
    href="http://www.example.com/de" />
  <xhtml:link
    rel="alternate"
    hreflang="en"
    href="http://www.example.com/en" />
</url>
<url>
  <loc>http://www.example.com/de</loc>
  <xhtml:link
    rel="alternate"
    hreflang="de"
    href="http://www.example.com/de" />
  <xhtml:link
    rel="alternate"
    hreflang="en"
    href="http://www.example.com/en" />
</url>
```
[http://googlewebmastercentral.blogspot.tw/2012/05/multilingual-and-multinational-site.html]()

## 判斷使用者語言的技術與使用時機
可利用以下兩種方式猜測使用者的語言
- Accept Language Header
- Geographic IP Address

__不要__猜測使用者的語言並產生不同的頁面給 user。應遵照 URL 產生對應的頁面。
原因：
1. 使用者可能使用別人的電腦（ex: 台灣人用美國朋友電腦）
2. 使用者可能不在自己的國家（ex: 台灣人去美國）
3. geo-ip 不一定 10% 正確
4. 使用者可能用 VPN
5. __Google 不建議__

正確的使用時機是在使用者進入網站後，假如使用者瀏覽的網站跟我們猜測他的語言不符合，跳出提告知使用者可以前往另外一個可能符合他語言的網站。

## 參考資料
 - [Google Webmaster: working with multilingual websites](http://googlewebmastercentral.blogspot.tw/2010/03/working-with-multilingual-websites.html)
 - [Google Webmaster: working with multi-regional websites](http://googlewebmastercentral.blogspot.tw/2010/03/working-with-multi-regional-websites.html)
 - [http://stackoverflow.com/questions/1828317/internationalization-and-search-engine-optimization]()
 - [http://webmasters.stackexchange.com/questions/403/how-should-i-structure-my-urls-for-both-seo-and-localization]()

