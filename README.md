1. Pythonをインストール
```
$ brew search python@3
==> Formulae
python@3.10    python@3.11    python@3.12    python@3.13 ✔  python@3.8     python@3.9 ✔   ipython        bpython        jython         cython
$ brew install python@3.9
```

2. Poetryをインストール
```bash
$ brew install poetry
```

3. Pythonプロジェクトの作成
```bash
$ poetry init project-name
```
```
├── README.md
├── pyproject.toml ← 依存関係の管理（package.json的なもの）
├── src
│   └── python_starter ← pythonの実コードを格納するディレクトリ 
│       └── __init__.py
└── tests ← ユニットテスト
    └── __init__.py
```

4. Hello World
```src/python_starter/main.py
print("Hello World")
```

5. FastAPI導入
```bash
$ poetry add fastapi uvicorn
```

5. Ruff
```
poetry add --dev ruff
```
以下の拡張機能をインストール
https://marketplace.visualstudio.com/items/?itemName=charliermarsh.ruff

6. settings.json
.vscode/settings.json
```json
{
    "[python]": {
        "editor.defaultFormatter": "charliermarsh.ruff",
        "editor.formatOnSave": true,
        "editor.codeActionsOnSave": {
            "source.fixAll": "explicit",
            "source.organizeImports": "explicit"
        },
    },
} 
```