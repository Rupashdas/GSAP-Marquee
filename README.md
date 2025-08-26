# GSAP Marquee

Lightweight marquee utility built on GSAP. This repository includes a vanilla JS implementation (`src/gsap-marquee.js`) with a jQuery plugin wrapper, plus a demo (`demo/index.html`).

Demo: https://rupashdas.github.io/GSAP-Marquee/

Features

- Smooth, ticker-driven animation using `gsap.ticker`.
- Accurate spacing using DOM geometry (getBoundingClientRect) — handles margins and gaps correctly.
- Supports multiple marquees on a page.
- Options: direction (`ltr`/`rtl`), pause modes, variable speed on hover, responsive rebuild, looping or single-run, and callbacks.

Install / usage

Include GSAP (and optionally jQuery) then load the script from `src/` or your build output:

```html
<script src="https://cdn.jsdelivr.net/npm/gsap@3/dist/gsap.min.js"></script>
<!-- optional jQuery for the plugin wrapper -->
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<script src="src/gsap-marquee.js"></script>
```

HTML structure

```html
<div class="customMarquee" id="myMarquee">
  <div class="marqueeInner">
    <div class="marquee-item">Item A</div>
    <div class="marquee-item">Item B</div>
    <div class="marquee-item">Item C</div>
  </div>
</div>
```

Options

Pass an options object to `gsapMarquee(selector, options)` (or use the jQuery plugin):

| Option | Type | Default | Description |
|---|---:|---|---|
| speed | number | 100 | Pixels per second.
| direction | string | 'ltr' | 'ltr' or 'rtl'. Controls movement direction.
| pauseOnHover | boolean | true | Pause when mouse enters the marquee.
| pauseOnClick | boolean | false | Toggle pause when marquee is clicked (demo shows pattern).
| variableSpeed | boolean | false | On hover, slow down instead of pausing.
| startPaused | boolean | false | Start the marquee paused.
| responsive | boolean | true | Rebuild clones and widths on window resize.
| loop | boolean | true | Continuous looping (set false to run once).
| containerSelector | string | '.customMarquee' | Selector for the inner wrapper containing items.
| itemsSelector | string | '.marquee-item' | Selector for item nodes within the container.
| onComplete | function | null | Callback when a non-looping marquee completes a cycle. Receives cycle count.

Example (vanilla)

```js
var instance = gsapMarquee('#m1', {
  speed: 140,
  direction: 'ltr',
  pauseOnHover: true,
  variableSpeed: false,
  responsive: true,
  loop: true,
  containerSelector: '.marqueeInner',
  itemsSelector: '.marquee-item'
});
```

Example (images)

Always ensure images are loaded before initializing image marquees. Use `imagesLoaded` or wait for font loads, then call a short `setTimeout` and initialize.

```js
imagesLoaded('#m3', function(){
  setTimeout(function(){
    gsapMarquee('#m3', {
      speed: 80,
      containerSelector: '.marqueeInner',
      itemsSelector: '.marquee-img-item'
    });
  }, 0);
});
```

API / methods

Each initialized instance exposes:

- `pause()` — Pause animation.
- `resume()` — Resume animation.
- `isPaused()` — Returns `true` if paused.
- `rebuild()` — Recalculate widths and clones (call after DOM/content changes).
- `reverse()` — Toggle direction between `ltr` and `rtl`.
- `destroy()` — Cleanup event listeners and stop ticker for that instance.

Notes & accessibility

- Use `will-change: transform` on the inner container for smoother animation.
- Respect `prefers-reduced-motion`: consider starting paused or reducing speed for users who opt-in to reduced motion.
- Hover pause is not reliable on touch devices — provide explicit controls for mobile.
- Avoid placing interactive controls inside continuously moving marquees; if necessary, pause on `focus` for keyboard accessibility.
- If you change content dynamically, call `instance.rebuild()` after layout stabilizes.

License

MIT