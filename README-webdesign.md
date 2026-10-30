# 本任务资料总览：webdesign v1.2 × OCR 任务

从「新建 OCR 网页识别 PDF 图片文字」任务（`2026-10-30-21-12-03`）与 webdesign v1.2 技能中，
把**设计相关的规范、文档、上下文**搬到了本工作区，便于继续沿用或重做。

## 目录结构
```
2026-10-30-23-15-22/
├─ README-webdesign.md                  ← 本文件（总览）
├─ webdesign-v1.2/                      ← webdesign v1.2 规范完整副本
│  ├─ SKILL.md                          · 规范总说明（何时用、令牌、禁忌、复用口诀）
│  ├─ references/design-system.md       · 完整 CSS 令牌 + 主题切换（亮/暗/跟随系统）代码
│  └─ assets/
│     ├─ webdesign-v1.2.html            · 网页版活范本（可直接浏览器打开）
│     ├─ webdesign-v1.2-prompt.md       · 可复制粘贴的提示词
│     └─ effect-showcase.svg            · 配色色块示意图
└─ context/
   ├─ webdesign在OCR任务中的应用.md      · OCR 页面如何套用规范：令牌映射+偏离点（核心）
   └─ OCR任务-2026-10-30工作日志.md      · 原任务当天上下文（打包/ fnOS 上架记录）
```

## 一图速记（OCR 页面已落地的规范要点）
- 底色 `#FFF1E5` 三文鱼粉；强调色 `#990F3D` 酒红（暗色 `#C7365F`）。
- 正文 `#33302E`，16px / 行距 1.85。
- 小标题酒红竖线 `.sec-title`；48px 居中短分割线 `hr.divider`。
- 右上角三态主题切换（跟随系统/明亮/昏暗），`localStorage` 持久化（键 `ocr-theme`）。

## 已知偏离（详见 context 文档第三节）
1. 卡片底色用了纯白 `#FFFFFF`（规范建议暖白 `#FFFAF6`）。
2. 圆角 14px、阴影略放大（风格微调）。
3. 状态徽标引入绿/红、警告横幅用琥珀色 —— 语义状态/警告色，属有意例外，非装饰强调色。
4. `<head>` 未加 `<meta name="color-scheme">`（规范建议项，可补）。

## 原 OCR 任务未搬入本工作区的内容
- 页面源码 `index.html` / `ocr-v1.1.html`、离线依赖 `libs/`（43MB）、`test/`、`fnos-app/`、`OCR离线工具_可分享版.zip` 等运行文件
  未复制（按此前"取消复制"的约定，只搬设计相关资料）。如需运行版，源目录完好：`C:\Users\SDKJ-\WorkBuddy\2026-10-30-21-12-03\`。
