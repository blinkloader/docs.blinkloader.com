<div style="font-size: 2rem; margin: 0 0 1rem;">Automatic Image Optimizer</div>

## React/Next.js

To achieve the best performance of your React/Next.js application, we'll be
using our open sourced react-blinkloader-components, hosted on Github.
This is a perfect solution, if you want to start loading images before
other bundles and then smoothly switch to React based rendering
without any conflicts.

### Quickstart

**Step 1. Create a project and copy the Project ID.**

Log into the dashboard using your Google account, then select a relevant project and go to the
<a href='/automatic-image-optimizer' target='_blank'>automatic image optimizer app</a>.

You should see a dashboard similar to this:

<img src='https://user-images.githubusercontent.com/1095400/47969500-7f60ca80-e02d-11e8-980b-508f14960c91.png'/>

Project ID can be taken from the right block.

<img src='https://cdn.staging-blinkloader.com/express/2gzemB8EavusbVtQ0btwyawka/image_optimizer_project_id.png'/>

In your own project the value is different, copy your Project ID value and use it in the SDK.

**Step 2. Add image sources to the whitelist.**

Resource whitelist allows Blinkloader to protect your account from other
people willing to do optimizations on your behalf.

For example, if all images are located in a folder named `xyz`, then you can
add `example.com/xyz` to the whitelist.

This lets optimization of images such as:
* `https://example.com/xyz/logo.png`
* `https://example.com/xyz/bg/foobar.png`

Other image sources would not be allowed. For example, an image like `https://bob.com/yo.png`
would be rejected and wouldn't be optimized.

**Step 3. Connect JavaScript SDK.**

Connect JavaScript SDK by adding these scripts to your website pages.

Add **blinkloader-2.0.5.min.js** to page head:

```html
<script src="https://cdn.blinkloader.com/blinkloader-2.0.5.min.js"></script>
```

Then add the following snippet to the bottom of page body, we need to
keep it outside of the React bundle and after the server
rendered application HTML.

Here is an example with a JSX template:

```html
<html>
  <head>
    <!-- blinkloader sdk -->
    <script src="https://cdn.blinkloader.com/blinkloader-2.0.5.min.js"></script>
  </head>
  <body>
    <!-- your server-side rendered application -->    
    <App/>

    <!-- blinkloader snippet -->
    <script
      dangerouslySetInnerHTML={{ __html: `Blinkloader.optimize({projectId: "YOUR_PROJECT_ID_GOES_HERE"});`}}
    ></script>

    <!-- your application bundle -->
    <script src="/app-bundle.js"></script>
  </body>
</html>
```

> Blinkloader works fine with pure client-side rendering. However, server side rendering (further SSR) is
highlhy recommended. With SSR images will start loading sooner, because the library
starts rendering images before the application bundle is done loading.

**Step 4. React components.**

Install `react-blinkloader-components`:
```
$ npm install --save @blinkloader/react-blinkloader-components
```

In the root component of your application:
```js
const blinkloader = require('@blinkloader/react-blinkloader-components');
const { BlinkloaderProvider } = blinkloader;

/// and then in the JSX, example:
const MySuperApp = ({children}) => (
  <BlinkloaderProvider projectId="YOUR_PROJECT_ID_GOES_HERE">
    <div>{children}</div>
  </BlinkloaderProvider>
)

export default MySuperApp;
```

**Step 5. Now we are ready to optimize the images!**

There are three ways to add optimized images to your website. It's up to you
to decide, which one you need according to your page layout.

Among the options are the following:
* Image Component
* Image Block Component
* Background Component

Each one is described further.

### Image Component

Use this component instead of the image tag. All props are applicable like it's
a traditional tag. The provided image is optimized automatically.

```js
const { Img } = require('@blinkloader/react-blinkloader-components');

<Img
  className={customClasses}
	src="https://example.com/hello.png"
	lazyload={true}
	progressive={true}
/>
```

### Image Block Component

Image block is used with a `div` tag. Have you seen smooth transitions on Medium? Making a smooth animated transition from blurry image into normal is tricky. That's why we have come up with this component. All other components support progressive image loading as well, but they don't support animation. Here is an example:

```js
const { ImgBlock } = require('@blinkloader/react-blinkloader-components');

const Photo = ({src, className}) => (
  <ImgBlock
    lazyload={true}
    progressive={true}
    className={className}
    src={src}
  />
)
```

### Background Component

Background image optimization:

```js
const { Background } = require('@blinkloader/react-blinkloader-components');

const Photo = ({src, className}) => (
  <Background
    className={className}
    lazyload={true}
    progressive={true}
    src={src}
  >
    <h1>Hello world!</h1>
    <p>More content goes here</p>
  </Background>
)
```

!> Keep in mind that `Background` and `ImgBlock` are divs. This is why they need to have some relative or absolute width and height parameters. So in case you switch from Img to these components keep this in mind. It's simple to do using CSS classes similar to other blocks in your layout.

### Defer Attribute

Add defer property to **Img** component, when you can't show images before the rest of the react bundle (ex: a slider on mobile devices). The layout may break if we render images without defer.

With defer you can start fetching optimized images before the bundle,
but they are rendered on a page only when the bundle is ready.

```js
const { Img } = require('@blinkloader/react-blinkloader-components');

const Photo = ({src, className}) => (
  <Img
    defer={true}
    lazyload={true}
    progressive={true}
    className={className}
    src={src}
  />
)
```

### Lazy Loading

Add `lazyload={true}` property to the react component in order to apply lazyloading on the element.

### Progressive Loading

Add `progressive={true}` property to the react component in order to use progressive loading.
Shows a blurry image before an original image is loaded.

### Prefetching

This is an advanced feature allowing to load an optimized image in advance and to keep it
in browser cache. It is useful when there are several website pages with images and you
know, that visitors will go through them.

With prefetching you can specify original images and then Blinkloader SDK prepares an
optimized version and preloads it for a visitor. This approach enables instant image
rendering, when new website pages are visited.

Usage example:

```js
Blinkloader.prefetch([
  'https://example.com/photo.png',
  'https://example.com/another-photo.png'
])
```

> In case of React it's recommended to put prefetching inside `componentDidMount`
of the initial view. Then new pages or new elements rendered further will have instant
images taken from browser cache.
