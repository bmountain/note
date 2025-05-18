必要物のインストール

```bash
sudo apt install graphviz doxygen
```

Doxyfileのテンプレート取得
```bash
doxygen -g Doxyfile
```

Doxyfileを編集し以下設定
```
PROJECT_NAME         = <適当に>
INPUT                = <ソースディレクトリ>
OUTPUT_DIRECTORY     = <htmlディレクトリが指定パス配下にできる>
EXTRACT_ALL          = YES
EXTRACT_PRIVATE      = YES
EXTRACT_STATIC       = YES
RECURSIVE            = YES
GENERATE_LATEX       = NO
HAVE_DOT             = YES
UML_LOOK             = YES
CALL_GRAPH           = YES
CALLER_GRAPH         = YES
DOT_PATH             = <which dotの出力>
MAX_DOT_GRAPH_DEPTH  = <適当に> # 0なら無制限
```
上記にない項目はそのままでOK

参考
https://ottfoekst.com/generate-class-diagram-and-call-graph-automatically/1738/#toc10