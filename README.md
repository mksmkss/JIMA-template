# JIMA（日本経営工学会）論文テンプレート

## 概要
このテンプレートは日本経営工学会（JIMA: Japan Industrial Management Association）の論文投稿用として作成されたLaTeXテンプレートです。

## 作成者情報
- **作成者**: Masataka Suzuki
- **作成日**: 2025年9月6日
- **バージョン**: 1.0

## ファイル構成
```
jima-template/
├── jima-paper.sty      # スタイルファイル（書式定義）
├── jima-template.tex   # メインテンプレートファイル
└── README.md          # このファイル
```

## 使用方法

### 1. 基本的な使い方
1. `jima-paper.sty` と `jima-template.tex` を同じフォルダに配置
2. `jima-template.tex` を編集して論文を作成
3. LaTeXでコンパイル

### 2. 論文情報の設定
```latex
% タイトル設定
\title{あなたの論文タイトル}

% 著者情報（最大6名まで対応）
\authorone{第一著者}{早稲田大学}
\authortwo{第二著者}{早稲田大学}
\authorthree{第三著者}{他の研究機関}
% 使わない著者行はコメントアウト
```

### 3. 特徴
- **所属別の著者表示**: 早稲田大学所属者とその他の所属者を自動で分けて表示
- **2カラムレイアウト**: 学会論文に適した2段組み
- **図表・数式対応**: figure環境、equation環境を利用可能
- **日本語対応**: ltjsarticleクラスを使用

## 動作環境
- LaTeX（TeX Live、MiKTeX等）
- LuaLaTeX推奨（日本語処理のため）
- Visual Studio Code + LaTeX Workshop拡張機能（推奨）

### VS Code設定（推奨）

#### 1. 拡張機能のインストール
まず、以下の拡張機能をインストールしてください：
- **LaTeX Workshop** by James Yu（必須）
- **Japanese Language Pack for Visual Studio Code**（日本語化）

#### 2. settings.jsonの設定
`Ctrl/Cmd + Shift + P` → `Preferences: Open Settings (JSON)` を選択し、`settings.json`を開いて以下の設定をコピペしてください：

```json
{
  // ========================================
  // LaTeX Workshop 基本設定
  // ========================================
  
  // LaTeX formatter（latexindent）のパス設定
  "latex-workshop.formatting.latexindent.path": "/usr/local/bin/latexindent.pl",
  
  // ビルドツールの定義
  "latex-workshop.latex.tools": [
    {
      "name": "Latexmk (LuaLaTeX)",
      "command": "latexmk",
      "args": [
        "-f",
        "-gg",
        "-lualatex",
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "%DOC%",
        "-outdir=%OUTDIR%"
      ]
    },
    {
      "name": "Latexmk (XeLaTeX)",
      "command": "latexmk",
      "args": [
        "-f",
        "-gg",
        "-xelatex",
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "%DOC%",
        "-outdir=%OUTDIR%"
      ]
    },
    {
      "name": "Latexmk (upLaTeX)",
      "command": "latexmk",
      "args": [
        "-f",
        "-gg",
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "%DOC%",
        "-outdir=%OUTDIR%"
      ]
    },
    {
      "name": "Latexmk (pLaTeX)",
      "command": "latexmk",
      "args": [
        "-f",
        "-gg",
        "-latex='platex'",
        "-latexoption='-kanji=utf8 -no-guess-input-enc'",
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "%DOC%",
        "-outdir=%OUTDIR%"
      ]
    }
  ],
  
  // ビルドレシピの定義（このテンプレートはLuaLaTeXを推奨）
  "latex-workshop.latex.recipes": [
    {
      "name": "LuaLaTeX",
      "tools": ["Latexmk (LuaLaTeX)"]
    },
    {
      "name": "XeLaTeX",
      "tools": ["Latexmk (XeLaTeX)"]
    },
    {
      "name": "upLaTeX",
      "tools": ["Latexmk (upLaTeX)"]
    },
    {
      "name": "pLaTeX",
      "tools": ["Latexmk (pLaTeX)"]
    }
  ],
  
  // ========================================
  // PDF表示・同期設定
  // ========================================
  
  // PDF表示方法（tabでVS Code内に表示）
  "latex-workshop.view.pdf.viewer": "tab",
  
  // SyncTeX（PDFとソースの相互ジャンプ）を有効化
  "latex-workshop.synctex.afterBuild.enabled": true,
  
  // ========================================
  // 自動ビルド設定
  // ========================================
  
  // 保存時に自動ビルド
  "latex-workshop.latex.autoBuild.run": "onSave",
  
  // ========================================
  // 出力・クリーンアップ設定
  // ========================================
  
  // 生成ファイルをoutディレクトリに出力
  "latex-workshop.latex.outDir": "./out",
  
  // クリーンアップ方法
  "latex-workshop.latex.clean.method": "glob",
  
  // ビルド後に自動クリーンアップ
  "latex-workshop.latex.autoClean.run": "onBuilt",
  
  // クリーンアップ対象ファイル
  "latex-workshop.latex.clean.fileTypes": [
    "*.aux",
    "%DOCFILE%.bbl",
    "%DOCFILE%.blg",
    "%DOCFILE%.idx",
    "%DOCFILE%.ind",
    "%DOCFILE%.lof",
    "%DOCFILE%.lot",
    "%DOCFILE%.out",
    "%DOCFILE%.toc",
    "%DOCFILE%.acn",
    "%DOCFILE%.acr",
    "%DOCFILE%.alg",
    "%DOCFILE%.glg",
    "%DOCFILE%.glo",
    "%DOCFILE%.gls",
    "%DOCFILE%.ist",
    "%DOCFILE%.fls",
    "%DOCFILE%.fdb_latexmk",
    "_minted*",
    "%DOCFILE%.nav",
    "%DOCFILE%.snm",
    "%DOCFILE%.vrb"
  ],
  
  // マジックコメント対応
  "latex-workshop.latex.magic.args": [
    "-f",
    "-gg",
    "-pv",
    "-synctex=1",
    "-interaction=nonstopmode",
    "-file-line-error",
    "%DOC%"
  ],
  
  // ========================================
  // パッケージ補完・IntelliSense設定
  // ========================================
  
  // 使用パッケージのコマンドや環境の補完を有効化
  "latex-workshop.intellisense.package.enabled": true,
  
  // ========================================
  // LaTeX用エディタ設定
  // ========================================
  
  // .texファイルの設定
  "[tex]": {
    "editor.suggest.snippetsPreventQuickSuggestions": false,
    "editor.tabSize": 2
  },
  
  // .latexファイルの設定
  "[latex]": {
    "editor.suggest.snippetsPreventQuickSuggestions": false,
    "editor.tabSize": 2,
    "editor.defaultFormatter": "mathematic.vscode-latex"
  },
  
  // .bibファイルの設定
  "[bibtex]": {
    "editor.tabSize": 2
  },
  
  // ========================================
  // 日本語文書用設定
  // ========================================
  
  // 日本語文書で単語移動を使うため、助詞や読点、括弧を区切り文字として指定
  "editor.wordSeparators": "./\\()\"'-:,.;<>~!@#$%^&*|+=[]{}`~?　、。「」【】『』（）！？てにをはがのともへでや",
  
  // Unicode文字のハイライト設定（日本語文字を許可）
  "editor.unicodeHighlight.allowedCharacters": {
    "，": true,
    "．": true,
    "！": true,
    "？": true,
    "［": true,
    "］": true,
    "｛": true,
    "｝": true,
    "＜": true,
    "＞": true,
    "（": true,
    "）": true,
    "：": true
  }
}
```

#### 3. 設定の確認方法
設定が正しく適用されているかは以下で確認できます：
1. `.tex`ファイルを開く
2. `Ctrl/Cmd + Shift + P` → `LaTeX Workshop: Build LaTeX project` でビルド
3. エラーがなければPDFが表示される
4. `Ctrl/Cmd + S`で保存すると自動ビルドされる

#### 4. トラブルシューティング
- **ビルドエラー**: `out`フォルダを削除してから再ビルド
- **PDF表示されない**: `latex-workshop.view.pdf.viewer`設定を確認
- **日本語が表示されない**: LuaLaTeXでビルドされているか確認

## 免責事項
⚠️ **重要**: このテンプレートは個人的な利用を目的として作成されたものです。

- 使用に際して生じるいかなる問題についても作成者は責任を負いません
- 公式な投稿規定については必ずJIMAの最新ガイドラインをご確認ください
- テンプレートの書式が投稿規定と異なる場合は、公式規定を優先してください

## ライセンス
このテンプレートは自由に使用・改変していただけますが、使用による結果について作成者は一切の責任を負いません。

## 更新履歴
- **v1.0** (2025/09/06): 初回リリース
  - 基本的な論文レイアウト機能
  - 最大6名の著者対応
  - 所属別著者表示機能

## サポート・バグ報告
このテンプレートに関する質問、バグ報告、改善要望がございましたら、以下のGitHubリポジトリのIssueページからお気軽にお報告ください：

**🔗 GitHub Repository**: https://github.com/mksmkss/JIMA-template

### Issueを作成する際のお願い
- **バグ報告**: 発生した問題の詳細、環境情報（OS、LaTeXディストリビューション等）を記載
- **機能要望**: 具体的な機能の説明と使用場面を記載
- **質問**: できるだけ具体的な状況を記載

回答を保証するものではありませんが、可能な限りサポートいたします。