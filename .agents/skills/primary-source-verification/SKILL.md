---
name: primary-source-verification
description: 技術記事や文章中の主張・コード・API仕様・数値を「一次情報」で検証する手順とフォーマットを提供するスキル。ファクトチェック、出典確認、要出典タグ付けを依頼されたときに参照する。
---

# 一次情報ファクトチェック スキル

このスキルは、文章中の技術的主張を**一次情報（primary source）**で検証するための定義・手順・出力テンプレートを提供します。note 記事のレビューや、外部記事のファクトチェック依頼を受けたときに参照してください。

---

## 1. 一次情報の定義

検証時は、以下の一次情報を優先的に参照します。

| カテゴリ | 例 |
|----------|----|
| 公式ドキュメント | `learn.microsoft.com`、`docs.python.org`、`developer.mozilla.org`、`kubernetes.io/docs` |
| 公式リポジトリ | GitHub の公式 org（`github.com/dotnet`, `github.com/microsoft`, `github.com/openai` 等）の README / ソース / リリースノート |
| 公式ブログ・告知 | `devblogs.microsoft.com`、`openai.com/blog`、`aws.amazon.com/blogs/aws`、製品リリースノート、変更ログ |
| 標準仕様 | RFC（IETF）、W3C 勧告、ECMA、ISO、Unicode、JIS |
| 学術論文 | arXiv、ACM、IEEE、Nature 等の査読済み論文 |
| 実機・実コードでの再現 | 自分で動かして確認できるコマンド・スクリプト・出力 |

### 二次情報は依拠しない

以下は検証の根拠にしません。参考として見る場合も、必ず一次情報へ遡ります。

- 個人ブログ、Qiita、Zenn、Medium、note の他者記事
- Stack Overflow、Reddit、X（Twitter）の投稿
- LLM の出力そのもの
- Wikipedia
- 二次配信のニュース記事

---

## 2. 検証手順

1. 主張の抽出: 対象文章を読み、検証対象となる「事実主張」「コード」「API シグネチャ」「数値」「日付・バージョン」を箇条書きで列挙する。意見・所感は対象外。
2. 一次情報の特定: 各主張について、最も適切な一次情報の URL を特定する。
3. 該当箇所の引用: 一次情報のうち、主張を裏付ける最小限の一文を引用する。
4. 判定: 以下のいずれかを付ける。

| 判定 | 意味 |
|------|------|
| ✅ 確認済 | 一次情報と完全に一致 |
| ⚠️ 要修正 | 表現の揺れ・古い情報・言い過ぎ・不正確だが部分的に正しい |
| ❌ 誤り | 一次情報と矛盾、または存在しない API / 機能 |
| ❓ 出典不明 | 一次情報を発見できず検証不能。要出典タグを推奨 |

5. 修正案の提示: ⚠️ / ❌ には書き換え案を添える。

---

## 3. 出力フォーマット

```markdown
## ファクトチェック結果

| # | 判定 | 主張（記事中の表現） | 一次情報 | 引用 / 補足 | 修正案 |
|---|------|----------------------|----------|------------|--------|
| 1 | ✅ | .NET 8 は LTS である | [.NET release lifecycle](https://learn.microsoft.com/dotnet/core/releases-and-support?WT.mc_id=DT-MVP-5004827) | "8.0 ... LTS ... 3 years" | — |
| 2 | ⚠️ | `HttpClient` は毎回 new するのが推奨 | [HttpClient guidance](https://learn.microsoft.com/dotnet/fundamentals/networking/http/httpclient-guidelines?WT.mc_id=DT-MVP-5004827) | 実際は `IHttpClientFactory` 推奨 | `IHttpClientFactory` 経由で取得する旨に書き換え |

### サマリ
- 確認済: N 件 / 要修正: N 件 / 誤り: N 件 / 出典不明: N 件
- ブロッカー（公開前に必ず直すべき項目）: #2
```

### 注意事項

- 表が長くなる場合は、判定ごと（❌ → ⚠️ → ❓ → ✅）にセクションを分けてもよい。
- 引用 URL は必ず実際にアクセスして存在を確認する。
- Microsoft 系ドメイン（`learn.microsoft.com`, `docs.microsoft.com`, `devblogs.microsoft.com`, `techcommunity.microsoft.com`）には `WT.mc_id=DT-MVP-5004827` を付与する。
- バージョン依存の主張は「いつ時点の情報か」を併記する。

---

## 4. ツール優先順位

| 用途 | 第一選択 | フォールバック |
|------|----------|----------------|
| Microsoft / Azure / .NET 系 | [`microsoft-docs`](../microsoft-docs/SKILL.md) スキル | 公式ページを直接取得 |
| GitHub のコード / Issue / Release | GitHub の公式リポジトリ | raw / release / tag URL を直接取得 |
| 一般 Web の公式ドキュメント | 公式ドメインのページ | Web 検索から公式ドメインへ絞り込み |
| OSS の挙動再現 | ローカルでコマンド実行 | 最小再現コード |

---

## 5. やってはいけないこと

- 一次情報を確認せずに「✅ 確認済」を付ける
- LLM の事前知識のみで判定する
- 検索結果のスニペットだけで判定する
- 二次情報を一次情報として扱う
- 翻訳された一次情報のみで判定する（原文がある場合は原文も確認）
