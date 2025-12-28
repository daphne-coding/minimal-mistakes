---
title: "Skin Preview"
layout: single
permalink: /skin-preview/
classes: wide
---

想快速比較 Minimal Mistakes 提供的配色？在這個頁面可以即時切換不同的 skin，無需重啟伺服器或改 `_config.yml`。

<div class="notice--info">在本頁切換只會影響預覽，不會改變全站的預設 skin（目前為 <strong>Milk Tea</strong>）。</div>

<div class="skin-preview" data-skin-preview>
  <div class="skin-preview__controls">
    {% for skin in site.data.skin_previews %}
    <button class="btn btn--small skin-preview__button" type="button"
      data-skin-label="{{ skin.label }}"
      data-skin-href="{{ skin.stylesheet | relative_url }}"
      aria-pressed="false">
      {{ skin.label }}
    </button>
    {% endfor %}
  </div>
  <p class="skin-preview__status">目前預覽：<strong id="skin-preview-current">{{ site.data.skin_previews[0].label }}</strong></p>

  <div class="skin-preview__grid">
    <article class="archive__item">
      <h3 class="archive__item-title">文章卡片</h3>
      <p class="archive__item-excerpt">展示標題、文字和按鈕，便於觀察文字對比與背景色。</p>
      <p>
        <a class="btn btn--primary" href="#">主要按鈕</a>
        <a class="btn" href="#">次要按鈕</a>
      </p>
    </article>

    <div class="notice--info">
      <h4 class="no_toc">提醒區塊</h4>
      <p>使用 notice 樣式可以快速檢視邊框、背景與連結顏色。</p>
      <p><a href="#">更多細節</a></p>
    </div>

    <div class="skin-preview__blockquote">
      <blockquote>
        <p>「色彩配搭不僅是審美，也是閱讀體驗的關鍵。」</p>
      </blockquote>
      <p class="small">— 匿名設計師</p>
    </div>

    <div class="skin-preview__code">
      <p class="skin-preview__badge">程式碼片段</p>
      <pre><code class="language-js">function hello(name) {
  return `Hello, ${name}!`;
}</code></pre>
    </div>
  </div>
</div>

<style>
.skin-preview__controls {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 0.5rem;
}

.skin-preview__controls .btn {
  margin: 0;
}

.skin-preview__status {
  font-weight: 600;
  margin-bottom: 1rem;
}

.skin-preview__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1rem;
}

.skin-preview__blockquote blockquote {
  margin: 0 0 0.5rem;
}

.skin-preview__code {
  border: 1px solid var(--global-border-color, #e9ecef);
  border-radius: 4px;
  padding: 0.75rem;
}

.skin-preview__badge {
  display: inline-flex;
  align-items: center;
  padding: 0.15rem 0.5rem;
  margin: 0 0 0.35rem;
  font-size: 0.8rem;
  font-weight: 600;
  border-radius: 999px;
  border: 1px solid var(--global-border-color, #e9ecef);
  background: var(--global-bg-secondary, rgba(0, 0, 0, 0.04));
}

.skin-preview__button[aria-pressed="true"] {
  box-shadow: 0 0 0 2px var(--global-border-color, #e9ecef);
}
</style>

<script>
(function() {
  const previewRoot = document.querySelector('[data-skin-preview]');
  if (!previewRoot) return;

  const stylesheetLink = document.querySelector('link[href*="/assets/css/main.css"]');
  if (!stylesheetLink) return;

  const buttons = previewRoot.querySelectorAll('[data-skin-href]');
  const statusEl = document.getElementById('skin-preview-current');
  const defaultHref = stylesheetLink.getAttribute('href');

  const setActiveButton = (active) => {
    buttons.forEach((button) => {
      button.setAttribute('aria-pressed', button === active ? 'true' : 'false');
    });
  };

  const setSkin = (button) => {
    const href = button?.dataset.skinHref || defaultHref;
    const label = button?.dataset.skinLabel || 'Milk Tea';
    stylesheetLink.setAttribute('href', href);
    if (statusEl) statusEl.textContent = label;
    setActiveButton(button);
  };

  buttons.forEach((button) => {
    button.addEventListener('click', () => setSkin(button));
  });

  setSkin(buttons[0]);
})();
</script>
