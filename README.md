# GSAP Marquee (jQuery + GSAP)

A tiny marquee utility built on **GSAP** and **jQuery**. Supports multiple marquees on the same page, hover-to-pause, responsive rebuilds, and a small control API per instance.

## Install

Use via a `<script>` tag after loading **jQuery** and **GSAP** (from CDN or your bundler).

```html
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3/dist/gsap.min.js"></script>
<script src="dist/gsap-marquee.js"></script>
```

Or import in a bundler (UMD): 

```js
import gsapMarquee from "gsap-marquee";
gsapMarquee(".customMarquee", { speed: 120 });
```

You can also use it as a jQuery plugin:

```js
$(".customMarquee").gsapMarquee({ speed: 120 });
```

## Usage

Your HTML should look like this:

```html
<div class="customMarquee">
  <div class="marqueeInner">
    <div class="marquee-item">Item 1</div>
    <div class="marquee-item">Item 2</div>
    <div class="marquee-item">Item 3</div>
  </div>
</div>
```

Then initialize:

```js
gsapMarquee(".customMarquee", {
  gap: 40,           // px gap between items
  speed: 100,        // px per second
  pauseOnHover: true,
  startPaused: false,
  responsive: true
});
```

### API

The function returns an instance (or an array of instances) with:

- `pause()` — pauses the marquee
- `resume()` — resumes the marquee
- `isPaused()` — returns boolean
- `rebuild()` — rebuilds layout (useful if items change)
- `el` — reference to the root element

## License

MIT