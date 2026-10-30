# webdesign v1.2 · 暖色系单页设计系统 Skill

一套以「三文鱼粉 + 酒红」为核心的暖色系单页 Web 配色设计规范，封装为 WorkBuddy 用户级 Skill。
全篇**只使用一种强调色（酒红 `#990F3D`）**，自带三态主题切换（跟随系统 / 明亮 / 昏暗）。

> 生成 HTML 格式的页面前，请先询问用户是否应用本规范（见 `webdesign-v1.2/安装提示词.txt`）。

## 配色速览

| 用途 | 色值 |
| --- | --- |
| 页面底色 | `#FFF1E5` 三文鱼粉 |
| 卡片底色 | `#FFFAF6` 暖白（非纯白） |
| 描边 | `#F0DCCC` 暖棕调 |
| 正文文字 | `#33302E` 近黑非纯黑 |
| **唯一强调色** | `#990F3D` 酒红（暗色 `#C7365F`） |

正文 `16px` / 行距 `1.85`；小标题加酒红竖线；分割线只用 48px 短横。

## 目录结构

```
webdesign-v1.2/
├─ SKILL.md                      规范总说明（何时用、令牌、禁忌、复用口诀）
├─ 安装说明.md                   安装路径、触发方式、套用步骤
├─ 安装提示词.txt                “生成 HTML 前先询问是否应用”
├─ 应用速查卡.md                 一页纸速查（令牌 / 必做三件事 / 禁忌）
├─ references/
│  └─ design-system.md           完整 CSS 令牌 + 主题切换（亮/暗/跟随系统）代码
└─ assets/
   ├─ webdesign-v1.2.html        网页版活范本（浏览器直接打开）
   ├─ webdesign-v1.2-prompt.md   可复用提示词
   └─ effect-showcase.svg        配色色块示意图
```

> 说明：本仓库只含 webdesign v1.2 设计系统 Skill 本身。它曾被用于「OCR 网页识别」项目的页面美化，
> 但 OCR 是另一个独立项目，其代码与设计落地记录单独成库，不在此仓库内。

## 安装为 WorkBuddy Skill

1. 把 `webdesign-v1.2/` 整个目录复制到：
   - 用户级：`C:\Users\<用户名>\.workbuddy\skills\webdesign-v1.2\`
   - 或项目级：`<工作区>\.workbuddy\skills\webdesign-v1.2\`
2. 刷新 / 重启 WorkBuddy 对话。
3. 在对话中描述"按暖色系美化网页"即可触发。

## 主题切换（默认组件）

所有套用本规范的页面，默认在页头右上角加入三态切换按钮，状态写入 `localStorage`。
完整 CSS / HTML / JS 见 `webdesign-v1.2/references/design-system.md` 的「主题切换」一节。

## 配色禁忌

- 不出现第二种鲜艳强调色（绿 / 蓝 / 橙等）。
- 不用 `#ffffff`、冷灰 `#f6f7f9` 作底；不用 `#000000`、冷黑 `#24292f` 作正文。
- 不画通栏长分割线，重点分隔只用 48px 短横。

## License

[MIT](./LICENSE) © 2026 boboxing
