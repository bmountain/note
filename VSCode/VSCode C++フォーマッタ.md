VSCodeでclang-formatを使用する手順を説明します。
MS製のC/C++ Extension Packのフォーマッタは動作しませんでした。
サードパーティの拡張機能を使用します。

# 前提
- WSL2で開発する

# 使用するプラグイン
- clang-format （WSLにインストール）
- Clang-Format（VSCode拡張機能）

# 準備
開発環境にclang-formatをインストールする
```bash
sudo apt install clang-format
```

開発環境でVSCodeを開き下記拡張機能をインストールする
名前：Clang-Format
作者：Xaver Hellauer
識別子：xaver.clang-format

WSLの適当なディレクトリに.clang-format設定ファイルを配置する

# 拡張機能を設定する
準備でインストールした拡張機能を設定する
設定画面で`@ext:xaver.clang-format`と検索する
Remote \[WSL: Ubuntu\]タブを開き、以下設定する

Clang-format: Executable
clang-formatの実行可能ファイルのパスを書く

Clang-fomrat: Fallback Style
`none`と書く。.clang-formatファイル以外の形式でのフォーマットを防止するため。

Clang-format: Style （最下部にあるはず）
`file:`に続けて.clang-formatファイルのパスを記載：
```
file:/your/path/to/.clang-format
```

# フォーマッタを適用する
上記拡張機能をフォーマッタとするよう設定する
設定画面でformatと検索する
Remote \[WSL: Ubuntu\]タブを開き、以下の設定を行う

Editor: Default Formatter
`Clang-Format`を選択する

Format On Paste
オンにする

Format On Save
オンにする

Format On Save Mode
既存コードにも適用する場合`file`を選択する
既存コードに適用しない場合`modifications`を選択する

# 念のための設定
C/C++ Extension Packのフォーマッタが動作しないようにする

設定画面でclangと検索する
Remote \[WSL: Ubuntu\]タブを開き、以下の設定を行う

C_Cpp: Clang_format_fallback Stle
`none`と書く

C_Cpp: Clang_format_path
空欄

C_Cpp: Clang_format_sort Includes
`null`を選択する

C_Cpp: Clang_format_style
空欄