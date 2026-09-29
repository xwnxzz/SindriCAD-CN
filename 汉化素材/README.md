# 汉化素材（SindriCAD 简体中文）

| 文件 | 用途 |
| --- | --- |
| `zh-CN.json` | 1307 条中文译文，复制到上游仓库 `locales/zh-CN.json` |
| `registry.patch` | 在 `src/i18n/registry.ts` 里注册该语言（import + LOCALES 一行） |
| `credits.patch` | `locales/CREDITS.md` 的署名改动 |

## 自己编译带中文的版本

```bash
git clone https://github.com/MakerViking/sindricad.git && cd sindricad
git apply /path/to/registry.patch /path/to/credits.patch
cp /path/to/zh-CN.json locales/zh-CN.json
npm ci
npm run i18n:check          # 应输出 0 missing / 0 extra
./scripts/build-sidecar-runtime.ps1     # Windows；Linux/macOS 用 .sh
node scripts/collect-licenses.mjs
npm run tauri build -- --config src-tauri/tauri.bundle.conf.json \
  --config '{"bundle":{"createUpdaterArtifacts":false}}'
```

构建需要 Rust（stable-msvc）、VS Build Tools（C++ 工作负载）、Node 20+、uv。
`createUpdaterArtifacts:false` 是因为本地没有上游的更新签名私钥。