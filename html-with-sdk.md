# Plain HTML + JavaScript SDK

### Quickstart

**Step 1. Create a project and copy the Project ID.**

Log into the dashboard using your Google account, then select a relevant project and go to the
<a href='/image-optimizer' target='_blank'>automatic image optimizer app</a>.

You should see a dashboard similar to this:

<img src='https://user-images.githubusercontent.com/1095400/47969500-7f60ca80-e02d-11e8-980b-508f14960c91.png'/>

Take Project ID from the block on the right.

<img src='https://cdn.staging-blinkloader.com/express/2gzemB8EavusbVtQ0btwyawka/image_optimizer_project_id.png'/>

In your project the value is different, copy your Project ID value and use it in the SDK.

**Step 2. Add image sources to the whitelist.**

Resource whitelist allows Blinkloader to protect your account from other
people willing to do optimizations on your behalf.

For example, if all images are in in the folder named `xyz`, then you can
add `example.com/xyz` to the whitelist.

This lets optimization of images such as:
* `https://example.com/xyz/logo.png`
* `https://example.com/xyz/bg/foobar.png`

Other image sources would not be allowed. For example, an image like `https://bob.com/yo.png`
would be rejected and wouldn't be optimized.

**Step 3. Connect JavaScript SDK.**

Connect JavaScript SDK by adding these scripts to your website pages.

Add **blinkloader-2.0.6.min.js** to page head:

```html
<script src="https://cdn.blinkloader.com/blinkloader-2.0.6.min.js"></script>
```

Then add the following snippet to the bottom of the page body. Here is an example:

```html
<html>
  <head>
    <!-- blinkloader sdk -->
    <script src="https://cdn.blinkloader.com/blinkloader-2.0.6.min.js"></script>
  </head>
  <body>
    <!-- your page content goes here -->    
    <h1>Hello world!!!</h1>

    <!-- blinkloader snippet at the bottom of page body -->
    <script>
      Blinkloader.optimize({projectId: "YOUR_PROJECT_ID_GOES_HERE"});
    </script>
  </body>
</html>
```

**Step 4. Now we are ready to optimize the images!**

There are three ways to add optimized images to your website. It's up to you
to decide, which one you need according to your page layout.

Among the options are the following:
* Image Component
* Image Block Component
* Background Component

Each one is described further.

### Image Component

**Image** is used with an **img** tag. Let's say that you have images in your HTML
layout specified with this tag, then to apply Blinkloader.js do the following:

```html
<!-- This is an original image -->
<img src="/photo.png"/>

<!--
  Same image with Blinkloader. We add a transparent pixel as a placeholder to avoid glitches.
-->
<img
  data-blink-src="/photo.png"
  data-blink-progressive
  data-blink-lazyload
  src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAIAAACQd1PeAAAABnRSTlMA/wD/AP83WBt9AAAADElEQVQI12P4//8/AAX+Av7czFnnAAAAAElFTkSuQmCC"
/>
```

### Image Block Component

**Image block** is used with a **div** tag. Have you seen smooth transitions on Medium? Making a smooth animated transition from a blurry image into normal is tricky. That's why we have come up with this component. All other components support progressive image loading as well, but they don't support animation. Here is an example:

```html
<div
  data-blink-image-block
  data-blink-progressive
  data-blink-lazyload
  data-blink-src="/hello-world.jpg"
  class="some classes"
/>
```

### Background Component

**Background** is similar to **image block**. The difference is that **background** can be a wrapper for other content. Previously mentioned elements don't accept child elements.
Add **background** to your page in the following way:

```html
<div
  data-blink-background
  data-blink-progressive
  data-blink-lazyload
  data-blink-src="awesome_bg.png"
  class="some classes"
>
  <h1>Hello world!</h1>
</div>
```

> Since you might want to copy some of the snippets above, progressive images and lazy loading are in the examples by default. Remove respective data attributes, If you don't need those features.

### Lazy Loading

Add `data-blink-lazyload` property to the HTML tag to apply lazy loading on the element.

### Progressive Loading

Add `data-blink-progressive` property to the HTML tag to use progressive loading.
Shows a blurry image before an original image is loaded.

### Prefetching

Prefetching is an advanced feature allowing to load an optimized image in advance and to keep it
in the browser cache. It is useful when there are several website pages with images and you
know, that visitors will go through them.

With prefetching, you can specify original images, and then Blinkloader SDK prepares an
optimized version and preloads it for a visitor. This approach enables instant image
rendering when new website pages are visited.

Usage example:

```js
Blinkloader.prefetch([
  'https://example.com/photo.png',
  'https://example.com/another-photo.png'
])
```
