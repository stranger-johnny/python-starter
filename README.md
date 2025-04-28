
## 1. Pythonをインストールする
まずはPythonをインストールします。
今回はバージョンを固定して使うため、Homebrewで特定のバージョンをインストールします。

```bash
$ brew search python@3
# 利用可能なバージョン一覧が表示されます

$ brew install python@3.13
```

## 2. Poetryをインストールして設定する
Pythonプロジェクトの依存管理には、Poetry を使います。

```bash
$ brew install poetry
```

## 3. Pythonプロジェクトを作成する
Poetryで新しいPythonプロジェクトを作成します。

```bash
$ poetry init python-starter
```
プロジェクトごとに仮想環境を分けたいので、以下の設定もしておきましょう。

```bash
$ cd python-starer
$ poetry config --local virtualenvs.in-project true
```

これで、プロジェクト直下に .venv フォルダが作成されるようになります。

初期構成はこんな感じになります。

```
├── README.md
├── pyproject.toml  # 依存管理ファイル（package.json的なもの）
├── src
│   └── python_starter
│       └── __init__.py
└── tests
    └── __init__.py
```

## 4. Hello Worldしてみる
まずは動作確認のため、簡単なコードを書いてみましょう。`src/python-starter/main.py`を作成して、`Hello World`を出力するようにします。

```python
print("Hello World")
```

```bash
$ poetry run python src/python_starter/main.py
Hello World
```
## 5. FastAPIを導入する

```bash
$ poetry add fastapi uvicorn
```
`src/python-starter/main.py`を以下のように修正します。
```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
async def root():
    return {"message": "OK"}
```

## 6. コード整形ツール Ruff を導入する
Ruff（Linter/Formatter）も導入しておきます。
```bash
$ poetry add --dev ruff
```
VSCodeを使っている場合は、拡張機能もインストールしておくと便利です。

[Ruff VSCode Extension](https://marketplace.visualstudio.com/items/?itemName=charliermarsh.ruff)

## 7. VSCode用の設定
.vscode/settings.json を以下のように設定します。自動インポートがされたり、保存時にフォーマットが走ります。
```json
{
    "python.analysis.autoImportCompletions": true,
    "python.analysis.indexing": true,
    "[python]": {
        "editor.defaultFormatter": "charliermarsh.ruff",
        "editor.formatOnSave": true,
        "editor.codeActionsOnSave": {
            "source.fixAll": "explicit",
            "source.organizeImports": "explicit"
        }
    }
}
```

## 8. FastAPIアプリを起動してみる
```bash
$ poetry run uvicorn src.python_starter.main:app --port 8080 --reload
```