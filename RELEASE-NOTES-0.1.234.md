# SindriCAD 中文版 v0.1.234-cn

## 「跟随系统」改为向 Tauri 索取系统主题

上一版用 `matchMedia("(prefers-color-scheme: light)")` 判断，在 Tauri 窗口里它**不跟随 Windows 的应用模式**
（webview 有自己的主题，这个查询只回答它自己那个值），所以「跟随系统」看起来失效。

现在读取 **Tauri 窗口主题**（`getCurrentWindow().theme()`）并订阅**系统主题变更事件**（`onThemeChanged`）：
这是操作系统真正的深浅色，运行中切换 Windows 主题会**立即**跟着变。媒体查询只作为浏览器开发/测试的后备。

## 引擎文案接进语言文件

新增 `src/geometry/engineText.ts`：把 Python 侧车自带的用户可见文案映射到语言文件，
**未知文案原样透传**（新引擎消息不能因为缺键而消失）。

- 导入阶段：`正在读取文件 / 正在简化面 / 正在打包`
- 看门狗报错（按句式匹配，因为秒数每次都不同）：
  `某个操作停顿超过 {seconds} 秒 —— 几何内核已重启；最后一个检查点之前的进度已保留`

## 下载

| 文件 | 说明 |
| --- | --- |
| `SindriCAD_0.1.234-cn_x64-setup.exe` | Windows 安装包（NSIS），推荐 |
| `SindriCAD_0.1.234-cn_x64.msi` | Windows 安装包（MSI） |

未签名，SmartScreen 可能拦截：选择「更多信息 → 仍要运行」。

## 许可

上游 AGPL-3.0（见 `LICENSE`）。本次修改的对应源码＝`汉化素材/`。与上游作者无隶属关系，未获背书。