# webdesign v1.2 在「OCR 网页识别 PDF 图片文字」任务中的应用上下文

> 本文档整理 OCR 任务（`2026-10-30-21-12-03`，主程序 `index.html` / `ocr-v1.1.html`）如何套用 **webdesign v1.2 暖色系设计规范**，
> 以及它与规范默认令牌之间的对应关系、做出的取舍与偏离点。供本任务（当前工作区）继续沿用或重做时参考。
> 规范完整内容见 `../webdesign-v1.2/`（SKILL.md + references/design-system.md + assets/）。

---

## 一、核心结论

OCR 页面**已按 webdesign v1.2 落地**：三文鱼粉底色 `#FFF1E5` + 酒红强调色 `#990F3D`、正文 `#33302E`、16px / 行距 1.85、
酒红竖线小标题、48px 居中短分割线、暖白卡片、右上角三态主题切换（跟随系统/明亮/昏暗，localStorage 持久化）全部到位。

规范令牌与本页面变量**一一对应但有重命名**；少数组件做了合理偏离（圆角、阴影、状态色），见第三节。

---

## 二、令牌映射表（规范 → OCR 页面实际变量）

| 规范令牌 | 规范色值 | OCR 页面变量 | OCR 页面取值 | 说明 |
| --- | --- | --- | --- | --- |
| 页面底色 `--bg` | `#FFF1E5` | `--bg` | `#FFF1E5` | 完全一致 |
| 卡片底色 `--panel` | `#FFFAF6` | `--surface` | `#FFFFFF` | 偏离：用了纯白作卡片（见偏离 1） |
| 输入框/代码区 `--panel-deep` | `#FFFDFB` | `--surface-2` | `#FBE9DD` | 偏离：改用浅蜜桃作次级面，非暖白输入框 |
| 描边 `--border` | `#F0DCCC` | `--border` | `#EAD9CC` | 暖棕描边，色系一致 |
| 正文 `--text` | `#33302E` | `--text` | `#33302E` | 完全一致 |
| 次要文字 `--muted` | `#8C7F74` | `--text-muted` | `#7A726C` | 同色系弱化，略偏灰 |
| 唯一强调色 `--accent` | `#990F3D` | `--accent` | `#990F3D` | 完全一致 |
| 强调弱化底 `--accent-soft` | `#FBE2E9` | `--accent-soft` | `#C7365F` | 偏离：页面把 `--accent-soft` 当作"强调色 hover 态"（亮酒红），而非淡晕染底 |
| 阴影 | `0 2px 10px rgba(153,15,61,.06)` | `--shadow` | `0 6px 24px rgba(153,15,61,.08)` | 偏离：阴影更大更柔（见偏离 2） |

### 暗色令牌（一致）
- 亮：`--accent #990F3D`；暗：`--accent #C7365F`（规范要求的暗色微调，已采用）。
- 暗色面：`--bg #1A1715 / --surface #25211E / --surface-2 #2F2A26 / --text #EBE4DE / --text-muted #A89E96 / --border #3A342F`。
- 暗色实现用 `:root[data-theme="dark"]` + `@media (prefers-color-scheme: dark)` 跟随系统，**与规范完全一致**。

---

## 三、组件实现与偏离点

### 1. 卡片底色用了纯白 `--surface:#FFFFFF`
规范建议卡片用暖白 `#FFFAF6` 避免纯白。OCR 页面为突出内容区（拖放框、文件卡片），用了纯白卡片 + 暖描边 + 较大阴影，视觉上更接近"工具面板"。
**取舍**：工具型页面内容密度高，纯白可读性略好；若严格合规可改回 `#FFFAF6`。

### 2. 圆角 `--radius:14px`、阴影放大
规范卡片圆角 12px、阴影 `0 2px 10px`。OCR 页面统一用 14px 圆角、阴影 `0 6px 24px rgba(153,15,61,.08)`，更现代、浮起感更强。属风格微调，不违反配色禁忌。

### 3. 主题切换按钮：三态 + localStorage
- 取值：`auto` / `light` / `dark`（规范示例用 `system/light/dark`，功能等价，文案"跟随系统/明亮/昏暗"一致）。
- 存储键：`ocr-theme`（规范默认 `webdesign-theme`，因是独立小工具单独命名）。
- 控件样式 `.theme-switch`（胶囊 `.active` 实底酒红）与规范一致。

**页面实际实现（index.html 第 224–238 行）**：
```html
<div class="theme-switch" id="themeSwitch" title="主题切换">
  <button data-theme="auto" class="active">跟随系统</button>
  <button data-theme="light">明亮</button>
  <button data-theme="dark">昏暗</button>
</div>
<script>
(function(){
  const root=document.documentElement, KEY='ocr-theme';
  const saved=localStorage.getItem(KEY)||'auto';
  applyTheme(saved);
  document.querySelectorAll('#themeSwitch button').forEach(b=>{
    b.classList.toggle('active', b.dataset.theme===saved);
    b.addEventListener('click',()=>{
      localStorage.setItem(KEY,t=b.dataset.theme);
      applyTheme(t);
      document.querySelectorAll('#themeSwitch button').forEach(x=>x.classList.toggle('active',x.dataset.theme===t));
    });
  });
  function applyTheme(t){ t==='auto'?root.removeAttribute('data-theme'):root.setAttribute('data-theme',t); }
})();
</script>
```
> 注：`<head>` 未加 `<meta name="color-scheme" content="light dark">`（规范建议项），可补。

### 4. 小标题 / 短分割线（一致）
- `.sec-title`：`border-left:4px solid var(--accent); padding-left:12px; font-size:18px`，与规范 `.card-title`（17px）几乎一致（仅字号 18 vs 17）。
- `hr.divider`：`width:48px; height:3px; background:var(--accent); border-radius:2px; margin:14px 0 22px` —— **与规范 48px 短横完全一致**。

### 5. 链接色（一致）
`a { color: var(--accent) }` —— 链接用酒红，符合规范。

### 6. 状态徽标：引入绿/红（有意偏离）
`.fc-status.done` 用绿 `#1f8a4d`、`.fc-status.err` 用红 `#c02828`，**违反了规范"全篇只酒红一种强调色"**。
**原因**：批量任务需要一眼区分"完成/失败"三态，仅靠酒红不够；这是语义状态色，属合理例外。若追求极致纯色，可改用酒红深浅区分（`done`=`--accent`，`err`=`--accent-deep #6E0B2C`）。

### 7. 警告横幅：琥珀色（有意偏离）
`.banner` 用琥珀 `#E0A100`（"file:// 打开受限"提示），同样属语义警告色，非装饰强调色。

### 8. 导出 HTML 内联样式
`exportHtml()` 生成的独立网页里硬编码了 `#990F3D` 标题与下划线 —— 直接复用强调色，符合规范。

---

## 四、若在本任务重做/沿用 OCR 页面，建议

1. **配色合规优先**：把 `--surface` 改回 `#FFFAF6`、补 `<meta name="color-scheme">`，让卡片完全暖色化。
2. **状态色取舍**：若要严格纯酒红，把 done/err 改为 `--accent` / `--accent-deep`。
3. **主题键统一**：新页面可沿用 `ocr-theme` 或回规范默认的 `webdesign-theme`（同一站点内用同一个键即可）。
4. **规范零成本复用**：`webdesign-v1.2/assets/webdesign-v1.2.html` 是活范本，`assets/webdesign-v1.2-prompt.md` 是可粘贴提示词，直接拿来美化新页面。

---

## 五、关键文件位置（本工作区）

- `../webdesign-v1.2/SKILL.md` —— 规范总说明
- `../webdesign-v1.2/references/design-system.md` —— 完整 CSS 令牌 + 主题切换代码
- `../webdesign-v1.2/assets/webdesign-v1.2.html` —— 网页版活范本
- `../webdesign-v1.2/assets/webdesign-v1.2-prompt.md` —— 可复用提示词
- `../webdesign-v1.2/assets/effect-showcase.svg` —— 配色色块示意图
- `OCR任务-2026-10-30工作日志.md` —— 原 OCR 任务当天打包/fnos 上架记录（设计相关上下文）
- 原 OCR 页面源码：`C:/Users/SDKJ-/WorkBuddy/2026-10-30-21-12-03/index.html`（未复制到本工作区，仅引用）
