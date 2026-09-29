# SindriCAD 中文版

> 上游项目：**[MakerViking/sindricad](https://github.com/MakerViking/sindricad)**（SindriCAD，AGPL-3.0）
> 本仓库只做一件事：**给 SindriCAD 补上简体中文界面**，并提供带中文的 Windows 安装包。

SindriCAD 是面向 3D 打印的参数化 CAD（Tauri + Rust + Python 几何侧车 / build123d + OpenCASCADE）：
约束草图、拉伸 / 旋转 / 放样 / 圆角 / 倒角、表面纹理与文字、导出 STEP / STL / 3MF，或直接发送到打印机。

---
![中文界面](<界面截图-中文版.png>)


## 下载

| 文件 | 说明 |
| --- | --- |
| `SindriCAD_*_x64-setup.exe` | **Windows 安装包（NSIS）**，安装后在「设置 → 语言」里可看到 **简体中文** |
| `SindriCAD_*_x64_en-US.msi` | Windows 安装包（MSI 格式，内容相同） |
| `SindriCAD-CN-locale-pack.zip` | **只含汉化文件**（几百 KB），适合已有官方版本、想自己编译或提 PR 的人 |

首次启动会由安装程序自带 WebView2 检测；安装包未签名，SmartScreen 可能提示「Windows 已保护你的电脑」，选择「更多信息 → 仍要运行」即可。

## 汉化了什么

`locales/en.json` 共 **1307 条**界面字符串，**全部译为简体中文**（占位符 `{...}` 与复数形式保持一致）：

- 菜单 / 功能区 / 命令面板、模型树与时间轴
- 草图工具与全部约束（重合 / 共线 / 同心 / 相等 / 固定 / 水平 / 竖直 / 平行 / 垂直 / 中点 / 对称 / 相切）
- 特征：拉伸 / 旋转 / 放样 / 扫掠 / 抽壳 / 拔模 / 分割 / 剖切 / 镜像 / 阵列 / 组合 / 推拉 / 偏移面 / 加厚
- 面上文字与表面纹理、打印导出与耗材映射、测量 / 干涉 / 悬垂 / 属性
- 设置（含 3D 鼠标）、快捷键自定义、错误与状态提示

界面在「设置 → 语言 → 简体中文」处切换（切换后需重启）。

## 汉化是怎么做的（可复核）

只有两处改动，其余是上游代码：

1. 新增 `locales/zh-CN.json`（1307 条译文，键顺序与 `en.json` 一致，未改任何英文原文）
2. `src/i18n/registry.ts`：`import zhCN from "../../locales/zh-CN.json";` +
   `"zh-CN": { name: "简体中文", tag: "zh-CN", data: zhCN as Catalogue }`

另在 `locales/CREDITS.md` 里按上游约定署名。

已通过上游自带的校验：

```
npm run i18n:check   → zh-CN: 1307 entries, 0 missing, 0 extra, 0 placeholder mismatches
npm run i18n:lint    → no hardcoded UI strings found
npm run build        → tsc --noEmit + vite build 通过
npx vitest run       → 2116 passed（3 个失败在未修改的上游代码上同样失败，与本汉化无关）
```

素材都在 `汉化素材/`：`zh-CN.json`、`registry.patch`、`credits.patch`。

## 来源与许可

- SindriCAD 采用 **AGPL-3.0**（原文见 `LICENSE`），本仓库是它的**衍生作品**：仅新增中文翻译，未修改程序逻辑。
- 按 AGPL-3.0，本次修改的「对应源码」就是本仓库的 `汉化素材/`（`zh-CN.json` + 两个 patch），
  程序本体源码见上游仓库对应的提交。
- 本仓库与 SindriCAD 作者 **MakerViking 无隶属关系**，也未获其背书；商标与版权归各自所有者。
- 安装包按「原样」提供，不含任何担保。

上游：<https://github.com/MakerViking/sindricad> · 变更日志：<https://github.com/MakerViking/sindricad/blob/main/CHANGELOG.md>
