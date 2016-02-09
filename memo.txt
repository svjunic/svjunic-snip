いつも忘れるメモ書き

### 書き方参考
いつも忘れるので調べたら参考になる物があったので参考にさせてもらっています。
https://github.com/yonchu/dotfiles/blob/master/.vim/snippets/snippet.snip

# 解説

## 基本形
```
snippet    [name]
abbr       [abbreviation]
alias      [aliases]
options    [options]
    snippet code...
    ${1}
    ${2:default word}
    ${3:#:default word}
```

### snippet
  スニペット名 (必須)
  この名前が補完候補になる)

### abbr
省略形 (オプション)
補完候補に表示する説明書きとして使用

### alias
エイリアス (オプション)
補完候補に別名をつける, スペース or カンマ"," 区切りで複数指定可能

### options
オプション (word|head|indent)
word   : 単語の境界でのみ補完候補の対象となる
head   : 行頭でのみ補完対象となる (先頭にスペースがあっても補完対象となる)
indent : スニペット展開後に上の行と同じレベルのインデントを行う

### snippet code
先頭に1つ以上スペース入れるとスニペットコードとして認識される
スニペットコードにプレースホルダを指定することによって
スニペット展開後に任意の場所にテキスト挿入することが出来る

### placeholder
${1}
  プレースホルダは番号によって入力する順番を指定する
${2:default word}
  デフォルトで入力されるテキストを指定することもできる
  何も入力せず飛ばした場合にはデフォルト値が挿入される
${3:#:description}
  デフォルト値の代わりに説明文を指定することもできる
  何も入力せず飛ばした場合には何も挿入されない
${4:TARGET}
  スニペット展開前に選択したテキストを挿入する
  <Plug>(neosnippet_expand_target) をマッピングする必要がある

末尾に空行を入れる場合
```
snippet if
  if ${1:#:condition}
    ${2:do}
  endif

    ${3}
```

複数のプレースホルダに同じテキストを入力する場合
```
  ${1}に入力すると$1にも同じテキストが入力される
  ${1} -> $1
```

最後にジャンプするプレースホルダ
```
$0
```

特殊文字のエスケープ
```
  `  { } $
  バックスラッシュ"\"を使用する (i.e. \{)
```
プレースホルダのには途中で改行を指定することはできない

vimの関数を実行することができる
```
  snippet     header
     File: ${1:`expand('%:t')`}
     ${2:Created at: `strftime("%B %d, %Y")`}
```

プレースホルダをネストすることも出来る
ただし特殊文字のエスケープ処理が必要
```
snippet div
   <div ${1:id="${2:someid\}"}>${3}</div>${4}

snippet  catch
options  head
    catch ${1:/${2:pattern: empty, E484, Vim(cmdname):{errmsg\\}\}/}
```

別のスニペットファイルを読み込む
```
  include c.snip
  include javascript/*
```

スニペット定義の削除
aliasを指定している場合はそれも削除する必要がある
```
  delete <snipeets_name>
```


### JSのよく忘れる縦横の取り方
よく忘れるやつ
```
// 画面幅
screen.width
// 画面高
screen.height
// 有効画面幅
screen.availWidth
// 有効画面高
screen.availHeight
// 表示領域幅
window.innerWidth
// 表示領域高
window.innerHeight
// ウィンドウ幅
window.outerWidth
// ウィンドウ高
window.outerHeight
// 表示領域幅
$(window).width()
// 表示領域高
$(window).height()
// 表示領域幅
document.documentElement.clientWidth
// 表示領域高
document.documentElement.clientHeight
// ドキュメント幅
$(document).width()
// ドキュメント高
$(document).height()
```
