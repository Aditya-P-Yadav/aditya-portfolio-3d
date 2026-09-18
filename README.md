# adityapratapyadav.co.uk

**Live at https://adityapratapyadav.co.uk**

Portfolio site for **Aditya Pratap Yadav**, Graduate Business Analyst, Birmingham.

One `index.html` and one `assets/` folder. Plain HTML, CSS and vanilla JavaScript. No
framework, no build step, no bundler, no backend.

## What is going on in the hero

A real 3D scan of me, rendered live with three.js, that **turns to follow your cursor**. It
floats on a canvas starfield with my tools orbiting it, and the huge ghosted word behind
changes as you scroll.

## Things in here worth a look if you write code

**The model is a static mesh with no skeleton.** No bones, no head joint, no animations. So
there is no head to articulate independently. The whole bust rotates toward the pointer,
eased, clamped to a natural range, with an idle sway when the cursor stops. On a head and
shoulders scan that is indistinguishable from head tracking, and it is honest about what the
asset actually supports.

**The loading placeholder is a render of the model itself.** The obvious approach is a
photo, but then the page visibly jumps when the 3D takes over. Instead the placeholder was
rendered offline from the same GLB using the same camera and the same five lights, exported
transparent and compressed to 22 KB of WebP. Measured against the live render it differs by
1.65 of 255, so the swap is invisible. It doubles as the fallback when WebGL is unavailable.

**The model was decimated on purpose.** The source scan is 2 million triangles and 58 MB. A
portfolio that makes someone download 58 MB is not a portfolio. `gltf-transform simplify`
took it to 60k triangles and 1.7 MB, which is indistinguishable at the size it renders.

**three.js is vendored, not loaded from a CDN**, so the site has no runtime dependency on
anyone else staying up.

**`<canvas>` is a replaced element.** `position:fixed;inset:0` with `width:auto` resolves to
its intrinsic 300x150 rather than stretching, so a full screen canvas silently draws into a
small patch in the corner. Both canvases set explicit dimensions.

**Gradient text cannot inherit a text-shadow.** With `background-clip:text` and
`color:transparent`, the shadow paints a dark silhouette of the glyphs under the gradient and
the text reads almost black.

**The orbiting chips measure the headline's real bounding box** and fade out inside it. The
first version guessed a zone, which worked on desktop and failed completely on a phone where
the text runs full width.

**Everything that moves respects `prefers-reduced-motion`**, live and in both directions.

## Structure

```
index.html     the entire site
assets/        the 3D model, its render, dashboards, a CV
assets/lib/    three.js r128 and GLTFLoader, vendored
```

## Contact

apy270602@gmail.com / [LinkedIn](https://www.linkedin.com/in/aditya-pratap-yadav-6505742a5/)
