# Google Font Picker
A simple method to use +1500 google fonts in your project, built with <code>HTML/CSS/JAVASCRIPT</code>!
# Feature this project
- Get more then +1500 fonts
- Filter Font by Popularity,new-added,trending,top-styled
- Font style live preview by sample text
- get each font ttf file based font variants `(truetype format)`
- Pagination Feature
> After Devide Pagination project gather more lightweight & faster
> 
## Why I should use it, instead of `Google Fonts`?
- You have to keep browsing to find a suitable font for your web project
> different fonts to see how it looks! testing your text for each single font,and style live preview by sample text

## Table of Contents
1. [Api](#api)

## api
> font api define as variable
```js
var api_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
var api = `https://www.googleapis.com/webfonts/v1/webfonts?key=${api_key}`;
```

> filter font by `popularity,trending,style,new-added-font and alfhabeticali`
```js
var popularity = "popularity", 
alfhabeticali = "alpha", 
NewItemFirst = "data", 
topStyle = "style",
trending ="trending";
var api = `https://www.googleapis.com/webfonts/v1/webfonts?key=${xxxxxx}&sort=${popularity}`
```
> fetch google font api
```js
const fetchfonts = async () => {
  const response = await fetch(api);
  const data = await response.json();
  return data; 
}
```
> then define display function
```js
fetchfonts().then(data => {
//item = number of font per page
//currPage = current page
  result = data.items.slice(item*currPage - item, item*currPage);/// for pagination method
  displayFont(result)
}) 
```
> Finaly display result
```js
const displayFont = (data) => {
data.forEach(font => {
      var plus = font.family.replace(/ /g, '+');
      var url = "https://fonts.googleapis.com/css?family="+plus+":"+font.variants;
      var card = document.createElement("div");
      card.classList = "card ";
      $(card).append(`<h3 class="card_title" style="font-family:${font.family}"><span>${font.family}</span><div class="ribbon-right">${font.variants.length} Style</div></h3>`);
      $(card).append(`<p class="card_sample" style="font-family:${font.family}" contenteditable="true">&#10075;&#10075;The best and most beautiful things in the world cannot be seen or even touched — they must be felt with the heart&#10076;&#10076;</p>`)
      $(card).append(`<h4>Add this code into the <i style='color: goldenrod;font-weight:300;'>&lt;head&gt;</i></h4>`);
      $(card).append(`<pre id="code-block" class="highlight"><code class="language-html" id="bb">&lt;link href="${url}" rel="stylesheet" type="text/css"&gt;</code></pre>`);
      $(card).append(`<h4>Add this code into the <i style='color: goldenrod;font-weight:300;'>&lt;style&gt;</i> <small style="font-size:8px;">or</small> <i style='color: goldenrod;font-weight:300;'>style.css</i></h4>`);
      $(card).append(`<pre id="code-block" class="highlight"><code class="language-css">@import url("${url}&display=swap");\nfont-family: "${font.family}", ${font.category};/* Family Name */</code></pre>`);
      $(card).append(`<h4 id="ttf"><span><i style='color: goldenrod;font-weight:300;'>@font-face</i> (ttf files)</span><a href="${font.truetype}" onclick="downloadedMsg()">Download <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 15 15" style="enable-background:new 0 0 585.918 585.918" xml:space="preserve"><path d="M13.75 1.254H9.209l-.06.003V0L.286 1.183v12.604l8.864 1.214v-1.295c.02.001.039.003.06.003h4.541a.964.964 0 0 0 .963-.963V2.217a.964.964 0 0 0-.963-.963zM2.933 6.663l-.84.017v2.641L1.42 9.29V6.695l-.766.016v-.596l2.279-.083v.632zm2.848-.059-.962.02v2.824l-.768-.036V6.64l-.873.018v-.636l2.603-.096v.678zm2.81-.076-1.52.032v.839l1.417-.003v.698l-1.417-.018v1.477l-.852-.039V5.91l2.372-.087v.705zm5.573 6.217a.413.413 0 0 1-.413.413H9.209c-.02 0-.04-.003-.06-.006V6.066l.007-.011c.072-.127.182-.171.639-.171h.341v2.708c0 .435-.044.49-.545.523v.154h1.58v-.154c-.523-.033-.567-.088-.567-.523V5.884h.391c.413 0 .506.038.595.171.054.072.097.178.144.358h-.442c-.154 0-.226-.011-.303-.137h-.11a21.67 21.67 0 0 1-.066.991h.159c.066-.243.11-.396.176-.49.072-.127.182-.171.639-.171h.341v2.709c0 .435-.044.49-.545.523v.154h1.58v-.154c-.523-.033-.567-.088-.567-.523V6.606h.391c.413 0 .507.039.594.171.066.088.116.226.176.49l.16-.017a13.62 13.62 0 0 1-.055-.974h-.116c-.088.105-.132.137-.281.137h-1.549a12.164 12.164 0 0 1-.045-.859h-.116c-.088.105-.132.137-.281.137H9.3a.649.649 0 0 1-.15-.012V1.811c.02-.003.039-.006.06-.006h4.541c.228 0 .413.185.413.413v10.527z" fill="#fff"/></svg></h4>`);
      var preUrls = document.createElement("pre");preUrls.classList = "highlight";
      preUrls.id = "code-block";preUrls.style.height = "100px";
      $(card).append(preUrls);
      var codeUrls = document.createElement("code");
      codeUrls.classList = "language-css";preUrls.append(codeUrls);
      // each files ttf urls base to each variants
     $.each(font.variants,function(index,value){
      codeUrls.insertAdjacentHTML("beforeend",'@font-face{\n    font-family: "'+ font.family +'", '+ font.category +';\n    font-variant: "'+ value +'";\n    src: url("'+ font.files[value] +'") format("truetype");\n}\n<br>');
    })
     $(card).append(`<div class="version" style="font-family:${font.family}"><span>${font.version}</span><small style="font-size:18px;font-weight:900;font-family: Consolas, Monaco, monospace;color:#fff">${font.lastModified}</small></div>`)
    $("#resultList").append(card);
    $('head').append('<link href="https://fonts.googleapis.com/css?family=' + plus + ":" + font.variants + '|" rel="stylesheet" type="text/css">');
})
}
```
# Contributing
If you want to make it better? That would be feel free even do it yourself and send a PR with the changes! 💻
