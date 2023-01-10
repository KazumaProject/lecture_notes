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
[http_request](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- `<label for="">`と`<input id="">`を揃えるとlabelをクリックするとinputにfocusされる

## CSS
- 優先順位
    1. インライン
    2. 内部参照
    3. 外部参照

<details>
    <summary>/summary>
</details>
- ボックスモデルを調整できるプロパティ

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

- 結合子を使ったセレクタの種類

| 種類                 | 結合子        | 記述例     | 適用石の要素                  |
| :--------------------| :-------------| :----------| :-----------------------------|
| ユニバーサルセレクタ | *             | *          | 全ての要素                    |
| 子孫セレクタ         | Space         | p strong   | p 階層化の全てのstrong        |
| 子セレクタ           | >             | p > strong | pの1つ下の階層のstrong        |
| 隣接セレクタ         | +             | h2 + p     | h2の直後の記述した同じ階層のp |
| 間接セレクタ         | ~             | h1 ~ p     | h1の後に記述した全ての階層のp |

- link
    1. `a:link` 未訪問のリンク
    2. `a:visited` 訪問済みのリンク
    3. `a:hover` ホバー状態のリンク
    4. `a:active` クリック状態のリンク

- font
    - `selector {
    font-family: <font_name> or <font_family>
    }`

## Flexbox
- `div.<_class_name>{item}`
- `display: flex;`
- `flex-direction: <direction>;`
    - row
    - row-reverse
    - column
    - column-reverse

- `flex-wrap`
    - nowrap
    - wrap
    - wrap-reverse

- `justify-content`
    - flex-start
    - flex-end
    - center
    - space-between
    - space-around
    - space-evenly

- `align-items`
    - stretch
    - flex-start
    - flex-end
    - center
    - baseline

- `align-content`
    - stretch
    - flex-start
    - flex-end
    - center
    - space-between
    - space-around

- `flex-flow`
    - `flex-flow: <flex_direction> <flex-wrap>`

## Grid
```css
display: grid;
grid-template-columns: 1fr 1fr 1fr
grid-template-columns: 200px 200px 200px;
```

## repeat関数
```css
grid-template-columns: 1fr 1fr 1fr;
```
```css
grid-template-columns: repeat(3, 1fr);
```

