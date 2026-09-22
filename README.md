# Amazon Image Saver

A static web page that gets all images from an Amazon product listing and saves them as `.jpg` files.

## Use

1. Open the site.
2. Paste an Amazon product link or an ASIN.
3. Click **Get images**.
4. Click an image to save it as a `.jpg` file. Or clear the check boxes of the images you do not want, and click **Download .zip**.

## If the listing does not load

The public proxies are not reliable. They can fail in some regions, and some browsers block them. Use the bookmarklet instead. It needs no proxy.

1. Drag the **Save Amazon images** button to your bookmarks bar.
2. Open a product page on Amazon.
3. Click the bookmark. The images open in the saver.

You can also open the listing in your browser, copy the page source, and paste it into **Did not work? Paste the page source.**

## How it works

- A static page cannot read amazon.com directly (CORS). The page gets the listing HTML through a public CORS proxy (`cors.eu.org`, then `allorigins.win`, then `corsproxy.io`).
- The page reads the gallery data (`colorImages.initial`) and uses the ID of each image to get the original, full-size file from `m.media-amazon.com`.
- The page converts each image that is not a JPEG to JPEG with a canvas. It uses [JSZip](https://stuk.github.io/jszip/) to make the `.zip` file.

## Run locally

```bash
python3 -m http.server 8765
```

## Deploy

Push to GitHub. In **Settings → Pages**, set the source to the `main` branch, folder `/`.
