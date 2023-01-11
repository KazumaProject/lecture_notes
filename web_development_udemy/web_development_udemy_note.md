# HTML
- type `!` for html template in visual studio code
## comment out
- `command + slash` for comment out
## list
- `ol>li*3`
## MDN
- https://developer.mozilla.org/ja/
## 構文チェック
- https://validator.w3.org/
## 属性
- [属性のリファレンス](https://developer.mozilla.org/ja/docs/Web/HTML/Attributes)
## link
- `rel="noopener"`, `target="_blank"`

[説明文](https://developer.chrome.com/ja/docs/lighthouse/best-practices/external-anchors-use-rel-noopener/`)
## 文字実体参照
- 著作権 `&copy;`
[文字実体参照一覧](https://html.spec.whatwg.org/multipage/named-characters.html)
- `<p><small>&copy; 2023 Kazuma Naka</small></p>`
## 情報のグループ化
- div
- section
- header
- footer
- main
- article
- aside
- nav
## divとspan
- div: block要素で改行される
- span: inline要素で改行されない

## Form
- `<form action="<path_to_send_data_in_server>" method="<http_request> > </form>"`

[http request](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

- `<label for="">`と`<input id="">`を揃えるとlabelをクリックするとinputにfocusされる

## CSS
- 優先順位
    1. インライン
    2. 内部参照
    3. 外部参照

<details>
    <summary> ボックスモデルを調整できるプロパティ</summary>

| プロパティ    |               |
| :-----------  | :-------------|
| margin        | marginを調整  |
| padding       | paddingを調整 |
| border        | borderを調整  |
| width         | 横幅の調整    |
| min-width     | 横幅の最小値を調整 |
| max-width     | 横幅の最大値を調整 |
| height        | 高さの調整    |
| min-height    | 高さの最小値を調整 |
| max-height    | 高さの最大値を調整 |

</details>

<details>
    <summary>結合子を使ったセレクタの種類</summary>


| 種類                 | 結合子        | 記述例     | 適用石の要素                  |
| :--------------------| :-------------| :----------| :-----------------------------|
| ユニバーサルセレクタ | *             | *          | 全ての要素                    |
| 子孫セレクタ         | Space         | p strong   | p 階層化の全てのstrong        |
| 子セレクタ           | >             | p > strong | pの1つ下の階層のstrong        |
| 隣接セレクタ         | +             | h2 + p     | h2の直後の記述した同じ階層のp |
| 間接セレクタ         | ~             | h1 ~ p     | h1の後に記述した全ての階層のp |

</details>

- link
    1. `a:link` 未訪問のリンク
    2. `a:visited` 訪問済みのリンク
    3. `a:hover` ホバー状態のリンク
    4. `a:active` クリック状態のリンク

- font
```css
 selector {
    font-family: <font_name> or <font_family>;
    }
```

## Flexbox
- `div.<_class_name>{item}`

```css
display: flex;
```

```css
flex-direction: row;
flex-direction: row-reverse;
flex-direction: column;
flex-direction: column-reverse;
```

```css
flex-wrap: nowrap;
flex-wrap: wrap;
flex-wrap: wrap-reverse;
```

```css
justify-content: flex-start;
justify-content: flex-end;
justify-content: center;
justify-content: space-between;
justify-content: space-around;
justify-content: space-evenly;
```

```css
aligh-items: stretch;
aligh-items: flex-start;
aligh-items: flex-end;
aligh-items: center;
aligh-items: baseline;
```

```css
align-content: stretch;
align-content: flex-start;
align-content: flex-end;
align-content: center;
align-content: space-between;
align-content: space-around;
```

```css
flex-flow: <flex_direction> <flex-wrap>;
flex-flow: row wrap;
```


## Grid

```css
display: grid;
```

```css
grid-template-columns: 1fr 1fr 1fr;
grid-template-columns: 200px 200px 200px;
```

## repeat関数
```css
grid-template-columns: 1fr 1fr 1fr;
```
```css
grid-template-columns: repeat(3, 1fr);
```

## minmax関数
```css
grid-template-columns: repeat(3, minmax(240px, 1fr));
```

## Section 10
[css reset](http://html5doctor.com/html-5-reset-stylesheet/)

<details>
    <summary> html5 css reset</summary>

    ```css:html5reset-1.6.1.css

/*
html5doctor.com Reset Stylesheet
v1.6.1
Last Updated: 2010-09-17
Author: Richard Clark - http://richclarkdesign.com
Twitter: @rich_clark
*/

html, body, div, span, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
abbr, address, cite, code,
del, dfn, em, img, ins, kbd, q, samp,
small, strong, sub, sup, var,
b, i,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, figcaption, figure,
footer, header, hgroup, menu, nav, section, summary,
time, mark, audio, video {
    margin:0;
    padding:0;
    border:0;
    outline:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}

body {
    line-height:1;
}

article,aside,details,figcaption,figure,
footer,header,hgroup,menu,nav,section {
	display:block;
}

nav ul {
    list-style:none;
}

blockquote, q {
    quotes:none;
}

blockquote:before, blockquote:after,
q:before, q:after {
    content:'';
    content:none;
}

a {
    margin:0;
    padding:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}

/* change colours to suit your needs */
ins {
    background-color:#ff9;
    color:#000;
    text-decoration:none;
}

/* change colours to suit your needs */
mark {
    background-color:#ff9;
    color:#000;
    font-style:italic;
    font-weight:bold;
}

del {
    text-decoration: line-through;
}

abbr[title], dfn[title] {
    border-bottom:1px dotted;
    cursor:help;
}

table {
    border-collapse:collapse;
    border-spacing:0;
}

/* change border colour to suit your needs */
hr {
    display:block;
    height:1px;
    border:0;
    border-top:1px solid #cccccc;
    margin:1em 0;
    padding:0;
}

input, select {
    vertical-align:middle;
}

    ``` 

</details>
