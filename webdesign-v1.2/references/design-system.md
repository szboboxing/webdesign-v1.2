# 设计系统完整 CSS — webdesign v1.2

复制以下 `:root` 令牌与基础样式到任意页面 `<style>` 即可套用本规范。

```css
:root {
  --bg: #FFF1E5;            /* 三文鱼粉页面底色 */
  --panel: #FFFAF6;         /* 卡片：暖白（非纯白） */
  --panel-deep: #FFFDFB;    /* 输入框/代码区：暖白 */
  --border: #F0DCCC;        /* 暖调描边 */
  --text: #33302E;          /* 正文文字（非纯黑） */
  --muted: #8C7F74;         /* 次要文字（同色系弱化） */
  --accent: #990F3D;        /* 全篇唯一强调色：酒红 */
  --accent-soft: #FBE2E9;   /* 酒红弱化底 */
}
* { box-sizing: border-box; margin: 0; padding: 0; }
body {
  font-family: -apple-system, "Segoe UI", "Microsoft YaHei", sans-serif;
  background: var(--bg); color: var(--text);
  font-size: 16px; line-height: 1.85;
}
.wrap { max-width: 1080px; margin: 0 auto; padding: 28px 20px 64px; }
header { margin-bottom: 6px; }
header h1 { font-size: 26px; line-height: 1.45; display: flex; align-items: center; gap: 10px; }
header h1 .logo { background: var(--accent); color: #fff; border-radius: 8px; padding: 2px 10px; font-size: 18px; }
header p { color: var(--muted); font-size: 14px; margin-top: 4px; }

/* 短分割线：48px 宽、3px 粗、居中、酒红 */
hr.divider { border: none; width: 48px; height: 3px; background: var(--accent); border-radius: 2px; margin: 10px auto 24px; }

.card {
  background: var(--panel); border: 1px solid var(--border); border-radius: 12px;
  padding: 20px 22px; margin-bottom: 18px;
  box-shadow: 0 2px 10px rgba(153, 15, 61, .06);
}
/* 小标题：酒红竖线 */
.card-title {
  font-size: 17px; font-weight: 700; color: var(--text);
  border-left: 4px solid var(--accent); padding-left: 12px; margin-bottom: 14px; line-height: 1.5;
}
.card-title .sub { font-size: 13px; font-weight: 400; color: var(--muted); margin-left: 8px; }

.urlbar { display: flex; gap: 10px; margin-top: 14px; }
.urlbar input {
  flex: 1; padding: 9px 12px; border: 1px solid var(--border); border-radius: 8px;
  font-size: 14px; background: var(--panel-deep); color: var(--text);
}
.urlbar input::placeholder { color: var(--muted); }
button {
  padding: 9px 16px; border: 1px solid var(--border); border-radius: 8px;
  background: var(--panel-deep); color: var(--text); font-size: 14px; cursor: pointer;
}
button.primary { background: var(--accent); border-color: var(--accent); color: #fff; }

/* 卡片配色方案示例（暖色系非纯白） */
#uploadCard, #fmtCard { transition: background .2s, border-color .2s; }
.scheme-a #uploadCard { background: #FFE7D6; border-color: #E9C3AC; } /* 浅蜜桃 */
.scheme-a #fmtCard   { background: #FFE7D6; border-color: #E9C3AC; } /* 与上传框统一 */
.scheme-b #uploadCard { background: #FBE3E9; border-color: #E6B9C6; } /* 酒红淡底 */
.scheme-b #fmtCard   { background: #FFE7D6; border-color: #E9C3AC; } /* 浅蜜桃 */
```

## 预览区（Markdown 渲染）样式要点
```css
#preview { font-size: 16px; line-height: 1.85; color: var(--text); background: var(--panel-deep); }
#preview strong { color: var(--accent); font-weight: 700; }     /* 重点加粗 = 酒红 */
#preview h4, #preview h5, #preview h6 { color: var(--accent); }  /* 小标题 = 酒红 */
#preview a { color: var(--accent); }
#preview blockquote { border-left: 4px solid var(--accent); background: var(--accent-soft); color: var(--muted); }
#preview hr { border: none; width: 48px; height: 3px; background: var(--accent); border-radius: 2px; margin: 20px auto; }
#preview th { background: #FBEFE4; }
#preview code { background: #F7EADC; }  #preview pre { background: #F9EFE3; }
```

## 配色禁忌（务必遵守）
- 不要出现第二种鲜艳强调色（绿/蓝/橙等）。
- 不要用 `#ffffff`、冷灰 `#f6f7f9` 作底色。
- 不要用 `#000000`、冷黑 `#24292f` 作正文。
- 不要用通栏长分割线；重点分隔只用 48px 短横。

## 主题切换（亮 / 暗 / 跟随系统）—— 默认组件

所有套用本规范的页面/文档，**默认在合适位置（页头右上角）加入三态主题切换按钮**：`跟随系统 / 明亮 / 昏暗`。

### CSS：完整令牌 + 暗色覆盖
```css
:root {
  --bg:#FFF1E5; --panel:#FFFAF6; --panel-deep:#FFFDFB; --border:#F0DCCC;
  --text:#33302E; --muted:#8C7F74; --accent:#990F3D; --accent-deep:#6E0B2C;
  --accent-soft:#FBE2E9; --tint-1:#F3E8DC; --tint-2:#FBEFE4; --tint-3:#F7EADC; --tint-4:#F9EFE3;
  --on-accent:#ffffff; --shadow:rgba(153,15,61,.06);
  --card-warm:#FFE7D6; --card-warm-border:#E9C3AC; --card-wine:#FBE3E9; --card-wine-border:#E6B9C6;
}
:root[data-theme="dark"] {
  --bg:#1E1A18; --panel:#2A2522; --panel-deep:#322C28; --border:#463E38;
  --text:#F2E9E2; --muted:#B8A99E; --accent:#C7365F; --accent-deep:#8C1E3D;
  --accent-soft:#3A2530; --tint-1:#3A312B; --tint-2:#382F29; --tint-3:#2E2620; --tint-4:#2A221C;
  --on-accent:#ffffff; --shadow:rgba(0,0,0,.35);
  --card-warm:#332A20; --card-warm-border:#4C3D2E; --card-wine:#3A2530; --card-wine-border:#5A2E3C;
}
/* 跟随系统：系统为暗色时自动变暗（明确选"明亮"则排除） */
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --bg:#1E1A18; --panel:#2A2522; --panel-deep:#322C28; --border:#463E38;
    --text:#F2E9E2; --muted:#B8A99E; --accent:#C7365F; --accent-deep:#8C1E3D;
    --accent-soft:#3A2530; --tint-1:#3A312B; --tint-2:#382F29; --tint-3:#2E2620; --tint-4:#2A221C;
    --on-accent:#ffffff; --shadow:rgba(0,0,0,.35);
    --card-warm:#332A20; --card-warm-border:#4C3D2E; --card-wine:#3A2530; --card-wine-border:#5A2E3C;
  }
}
/* 切换控件（页头右上角） */
.theme-switch { display:inline-flex; gap:2px; background:var(--panel-deep);
  border:1px solid var(--border); border-radius:999px; padding:3px; }
.theme-switch button { border:none; background:transparent; color:var(--muted);
  font-size:13px; padding:5px 12px; border-radius:999px; cursor:pointer; }
.theme-switch button.active { background:var(--accent); color:var(--on-accent); }
```
- 暗色下强调色由 `#990F3D` 微调为更可读的 `#C7365F`（同酒红色系，仍只此一色）。
- 所有白底/暖白/描边/正文均给出暗色对应值，切换时整体联动。
- `<head>` 加 `<meta name="color-scheme" content="light dark">`。

### 切换按钮 HTML
```html
<div class="theme-switch" id="themeSwitch" role="group" aria-label="主题切换">
  <button type="button" data-theme-val="system" class="active">跟随系统</button>
  <button type="button" data-theme-val="light">明亮</button>
  <button type="button" data-theme-val="dark">昏暗</button>
</div>
```

### JS：状态持久化（localStorage）
```html
<script>
(function () {
  "use strict";
  var THEME_KEY = 'webdesign-theme';
  function applyTheme(t) {
    if (t === 'system') document.documentElement.removeAttribute('data-theme');
    else document.documentElement.setAttribute('data-theme', t);
    document.querySelectorAll('#themeSwitch button').forEach(function (b) {
      b.classList.toggle('active', b.dataset.themeVal === t);
    });
  }
  var saved = null;
  try { saved = localStorage.getItem(THEME_KEY); } catch (e) {}
  applyTheme(saved === 'light' || saved === 'dark' ? saved : 'system');
  document.getElementById('themeSwitch').addEventListener('click', function (e) {
    var btn = e.target.closest('button[data-theme-val]');
    if (!btn) return;
    var t = btn.dataset.themeVal;
    try { localStorage.setItem(THEME_KEY, t); } catch (e) {}
    applyTheme(t);
  });
})();
</script>
```
