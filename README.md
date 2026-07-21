# ⚠️ Vulnerable Pages（意図的な脆弱性テストサイト）

> **これは脆弱性検知テストのために作成された、意図的に脆弱性を仕込んだGitLab Pages用の静的サイトです。**

## 含まれる脆弱性テスト

| ページ                                              | 脆弱性                                                    | 分類 (CWE / OWASP、目安)                                  |
| --------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| [dom-xss.html](public/dom-xss.html)                 | DOM-based XSS（`innerHTML` への未サニタイズ挿入）         | CWE-79                                                    |
| [reflected-xss.html](public/reflected-xss.html)     | Reflected XSS（検索結果へのクエリパラメータ反映）         | CWE-79                                                    |
| [secret-exposure.html](public/secret-exposure.html) | クライアントサイドへの機密情報（APIキー等）のハードコード | CWE-798 / CWE-540                                         |
| [unsafe-links.html](public/unsafe-links.html)       | `target="_blank"` の Tabnabbing（evil-tab.html）          | CWE-1022                                                  |
| [unsafe-links.html](public/unsafe-links.html)       | 未検証オープンリダイレクト（redirect.html）               | CWE-601                                                   |
| [missing-csp.html](public/missing-csp.html)         | CSP・セキュリティヘッダー不備                             | CWE-693（近似）/ OWASP A05:2021 Security Misconfiguration |

## ローカルでの確認方法

```bash
cd public
python3 -m http.server 8080
# http://localhost:8080 を開く
```

## 参考

- OWASP Top 10: https://owasp.org/www-project-top-ten/
- OWASP Cheat Sheet Series (XSS Prevention): https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html
