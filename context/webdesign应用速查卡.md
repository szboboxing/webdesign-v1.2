# webdesign v1.2 · 应用速查卡

暖色系单页规范「三文鱼粉 + 酒红」，全篇只酒红一种强调色。生成 HTML 前**先问用户是否套用**。

## 亮色令牌（抄进 :root）
| 用途 | 变量 | 值 |
| --- | --- | --- |
| 底色 | `--bg` | `#FFF1E5` |
| 卡片 | `--panel` | `#FFFAF6`（暖白，非纯白） |
| 输入框/代码区 | `--panel-deep` | `#FFFDFB` |
| 描边 | `--border` | `#F0DCCC` |
| 正文 | `--text` | `#33302E`（非纯黑） |
| 次要文字 | `--muted` | `#8C7F74` |
| 强调色 | `--accent` | `#990F3D` |
| 强调弱化底 | `--accent-soft` | `#FBE2E9` |

## 暗色令牌（data-theme="dark" 或系统暗色时）
`--bg #1E1A18` · `--panel #2A2522` · `--panel-deep #322C28` · `--border #463E38`
`--text #F2E9E2` · `--muted #B8A99E` · `--accent #C7365F`（暗色微调，仍只此一色）

## 必做三件事
1. **主题切换**：页头右上角三态按钮 `跟随系统 / 明亮 / 昏暗`，状态写 `localStorage`（键 `webdesign-theme`）。代码见 `references/design-system.md` 第 81–156 行。
2. **小标题**：`border-left:4px solid var(--accent); padding-left:12px;` + 加粗。
3. **短分割线**：`width:48px; height:3px; background:var(--accent);` 居中，千万别画通栏长线。

## 组件范式
- 卡片：暖白底 + 暖描边 + 极淡酒红阴影 `0 2px 10px rgba(153,15,61,.06)`。
- 主按钮：酒红实底白字；次按钮：暖白底 + 暖描边。
- 链接 / 加粗 / 四级以下小标题：全部用酒红。

## ⛔ 禁忌（违反即不合格）
- 出现第二种鲜艳强调色（绿/蓝/橙）。
- 用 `#ffffff` 或冷灰 `#f6f7f9` 作底；用 `#000000` 或冷黑 `#24292f` 作正文。
- 画通栏长分割线。

## OCR 任务的实际偏离（属有意例外，非装饰强调色）
- 卡片底色用了纯白 `#FFFFFF`（规范建议暖白）。
- 状态徽标用绿/红、警告横幅用琥珀色（语义状态/警告色）。
- `<head>` 未加 `<meta name="color-scheme" content="light dark">`（建议补）。
- 主题键改名 `ocr-theme`、按钮值 `auto/light/dark`（功能等价）。

## 快速资源
- 活范本：`assets/webdesign-v1.2.html`｜提示词：`assets/webdesign-v1.2-prompt.md`｜色块图：`assets/effect-showcase.svg`
- 落地记录：`webdesign在OCR任务中的应用.md`
