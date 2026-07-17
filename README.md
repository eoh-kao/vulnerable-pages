# ⚠️ Vulnerable Pages（意図的な脆弱性テストサイト）

> **これは脆弱性検知テストのために作成された、意図的に脆弱性を仕込んだGitLab Pages用の静的サイトです。**

## 目的

フロントエンドで起こりがちな脆弱性を、実際に手を動かして体験・観察できるデモサイトです。
各ページには

- 脆弱なコードとその実演（`VULNERABLE:` コメント付き）
- なぜ危険なのか（想定される攻撃シナリオ）
- 正しい実装方法（`FIX:` コメント付き）

を記載しています。

## 公開範囲・取り扱い上の注意

このリポジトリは GitLab Pages でホスティングされますが、**社内限定公開**として利用してください。

1. GitLab の `Settings > General > Visibility, project features, permissions` で
   **Pages access control を `Only project members`（もしくは Private）に設定**してください。
   コード側だけでは公開範囲を制限できないため、必ずこの設定を確認してください。
2. デモページの URL や脆弱性の内容を社外に共有しないでください。
3. 学習が終わったら Pages を無効化する、またはリポジトリをアーカイブすることを推奨します。

## 含まれる脆弱性テスト

| ページ                                              | 脆弱性                                                    | 分類 (CWE / OWASP、目安)                                  |
| --------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| [dom-xss.html](public/dom-xss.html)                 | DOM-based XSS（`innerHTML` への未サニタイズ挿入）         | CWE-79                                                    |
| [reflected-xss.html](public/reflected-xss.html)     | Reflected XSS（検索結果へのクエリパラメータ反映）         | CWE-79                                                    |
| [secret-exposure.html](public/secret-exposure.html) | クライアントサイドへの機密情報（APIキー等）のハードコード | CWE-798 / CWE-540                                         |
| [unsafe-links.html](public/unsafe-links.html)       | `target="_blank"` の Tabnabbing（evil-tab.html）          | CWE-1022                                                  |
| [unsafe-links.html](public/unsafe-links.html)       | 未検証オープンリダイレクト（redirect.html）               | CWE-601                                                   |
| [missing-csp.html](public/missing-csp.html)         | CSP・セキュリティヘッダー不備                             | CWE-693（近似）/ OWASP A05:2021 Security Misconfiguration |

> CWE 番号は代表的なものを目安として付記しています。特に「CSP・セキュリティヘッダー不備」は単一の CWE に一対一で対応しないため近似的な分類です。正確な分類が必要な場合は [cwe.mitre.org](https://cwe.mitre.org/) で個別に確認してください。

各ページの「攻撃してみる」リンクから、実際に脆弱性が発火する様子を確認できます。

## ローカルでの確認方法

```bash
cd public
python3 -m http.server 8080
# http://localhost:8080 を開く
```

## デプロイ

`master` / `main` ブランチへの push で GitLab CI/CD の `pages` ジョブが実行され、
`public/` ディレクトリの内容がそのまま Pages として公開されます（`.gitlab-ci.yml` 参照）。

## 参考

- OWASP Top 10: https://owasp.org/www-project-top-ten/
- OWASP Cheat Sheet Series (XSS Prevention): https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html
