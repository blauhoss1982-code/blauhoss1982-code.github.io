# hermes-oauth-pages

Google OAuth 应用 **hermes-backup** 的公开页面（主页 / 隐私政策 / 服务条款）。
存在的原因只有一个：Google Cloud 的 Branding 页要求三个**可公开访问**的 URL，否则 `Publish app` 按钮是灰的，
应用会一直停在 Testing（refresh token 7 天过期，备份链每周断一次）。

## 在线地址（GitHub Pages）

| 用途 | URL |
|---|---|
| 主页 | https://blauhoss1982-code.github.io/ |
| 隐私政策 | https://blauhoss1982-code.github.io/privacy.html |
| 服务条款 | https://blauhoss1982-code.github.io/terms.html |

远端 = `github.com/blauhoss1982-code/blauhoss1982-code.github.io`（public，Pages 源 = `master` / `/`）。

## 填在控制台哪里

Google Cloud → Google Auth Platform → Branding（GCP 项目 `durable-timing-513713-14`／项目号 `963132096169`）：

- Application home page / privacy policy link / terms of service link = 上表三条
- Authorized domain 1 = `blauhoss1982-code.github.io`（只写 host，不带 `https://`）

## 改页面的流程

改 HTML → commit → push 到 `master` → Pages 自动重建（1–2 分钟），然后复查：

```bash
for u in https://blauhoss1982-code.github.io/ https://blauhoss1982-code.github.io/privacy.html https://blauhoss1982-code.github.io/terms.html; do
  printf '%s -> ' "$u"; curl -s -o /dev/null -m 15 -w '%{http_code}\n' -x http://127.0.0.1:7897 "$u"
done   # 三个都要 200
```

链接所属的备份线见 `D:/vault/02_Projects/Hermes灾难恢复/PLAN.md` §2。
