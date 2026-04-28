---
name: microsoft-docs
description: Azure、.NET、Agent Framework、Aspire、VS Code、GitHub など Microsoft 技術エコシステムの公式ドキュメント、チュートリアル、コード例を調べるためのスキル。Microsoft Learn MCP を優先し、利用できない場合は公式ページを直接確認する。
---

# Microsoft Docs

Microsoft 技術エコシステムの調査スキルです。`learn.microsoft.com` を中心に、Azure、.NET、M365、Power Platform、Agent Framework、Semantic Kernel、Windows などを扱います。

---

## 1. 優先する情報源

Microsoft Learn が第一候補です。利用可能な場合は、以下の MCP ツールを優先します。

| Tool | Purpose |
|------|---------|
| `microsoft_docs_search` | learn.microsoft.com の概念、ガイド、チュートリアル、構成を検索 |
| `microsoft_code_sample_search` | Learn docs のコード例を検索。言語指定があるとよい |
| `microsoft_docs_fetch` | 特定 URL の本文を取得 |

MCP ツールが使えない場合は、公式ページを直接取得して本文を確認します。

---

## 2. Microsoft Learn 以外を使うケース

| 対象 | 推奨情報源 |
|------|------------|
| .NET Aspire | `aspire.dev` 公式 docs、`github.com/dotnet/aspire` |
| VS Code | `code.visualstudio.com`、VS Code API docs |
| GitHub | `docs.github.com`、`cli.github.com` |
| Agent Framework | Microsoft Learn と `github.com/microsoft/agent-framework` |

---

## 3. クエリの作り方

具体的に検索します。

```text
Azure Functions Python v2 programming model
Cosmos DB partition key design best practices
GitHub Actions workflow_dispatch inputs matrix strategy
Aspire AddUvicornApp Python FastAPI integration
Agent Framework workflow conditional edges branching handoff
```

含めるとよい情報:

- バージョン（例: .NET 8、Aspire 13）
- 目的（quickstart、tutorial、overview、limits、API reference）
- 言語（Python、TypeScript、C#）

---

## 4. note 記事での引用ルール

- 公式ドキュメント本文を確認してからリンクする。
- Microsoft Learn / Docs / DevBlogs / TechCommunity へのリンクには `WT.mc_id=DT-MVP-5004827` を付与する。
- 既にクエリ文字列がある場合は `&WT.mc_id=DT-MVP-5004827` を追加する。
- フラグメントがある場合はクエリをフラグメントより前に置く。
- Microsoft 以外の公式サイトには付けない。

---

## 5. やってはいけないこと

- 検索スニペットだけで事実確認を終える
- 存在を確認していない URL を作る
- 個人ブログや Q&A サイトを根拠にする
- 古いバージョンの情報を現行仕様として断定する
