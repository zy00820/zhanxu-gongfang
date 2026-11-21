# 栈序云 Android 套壳（WebView 容器）

纯套壳：一个 WebView 加载线上单页应用 `https://zy00820.github.io/zhanxu-gongfang/admin.html`，
与浏览器同源，登录态、后端会话、本地存储全部共用同一套逻辑，不在原生侧另存一份数据。

## 原生侧补了什么

| 能力 | 说明 |
|---|---|
| 返回键 | 页面能后退就后退，回到首屏才退出 App |
| 顶部进度条 | 加载进度，页面加载完成自动隐藏 |
| 外链处理 | 站内域名（github.io / supabase / jsdelivr / 图床）留在 App 内，其他链接交给系统浏览器 |
| 文件选择 | 支持网页里的 `<input type=file>`（上传头像、附件等后续功能可用） |
| 手势 | 关闭缩放与双击放大，避免和页面自己的交互打架 |
| 明文流量 | 禁止（`usesCleartextTraffic=false`），只走 HTTPS |

## 编译

本地需要 Android SDK 与 JDK 17：

```bash
cd android
gradle assembleRelease   # 产物：app/build/outputs/apk/release/app-release.apk
```

仓库已配置 GitHub Actions（`.github/workflows/android.yml`），推送到 `main` 会自动编译，
并把安装包发布到 Releases 的 `app-latest` 标签，固定下载地址：

```
https://github.com/zy00820/zhanxu-gongfang/releases/latest/download/zhanxu-cloud.apk
```

## 版本

- `versionName` 与网页端保持一致（当前 1.1.9）
- `versionCode` 用 `119` 这种“主版本*100 + 次版本”的形式，便于后续升级判断
