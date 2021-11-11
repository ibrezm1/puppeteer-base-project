# puppeteer-base-project

Simple base project showing puppeteer from [here](https://medium.com/@jaredpotter1/connecting-puppeteer-to-existing-chrome-window-8a10828149e0)

```
npm install

node index.js
```

Check the `puppeteer-us-keyboard-layout.ts` file for reference to all key definitions.

e.g.
`await page.keyboard.press("ArrowLeft");` where the string is a definition (the first column in the .ts file)


Connecting to the running instance 
1. Close all existing chrome
2. Open terminal and run
```
google-chrome --remote-debugging-port=9222
```
3. You should see an output below
```
DevTools listening on ws://127.0.0.1:9222/devtools/browser/df6d14b2-7d88-4077-ab11-c70fc08f3432
```
4. Connect to your session using 
```
const wsChromeEndpointurl = 'ws://localhost:9222/devtools/browser/41a0b5f0–6747–446a-91b6–5ba30c87e951';
const browser = await puppeteer.connect({
    browserWSEndpoint: wsChromeEndpointurl,
});
```
5. When navigating to a new page in Puppeteer and it happens to be a SPA utilizing the following syntax helps ensure the page fully loads before starting to interact with its elements.
```
await page.goto(pageUrl, {
    waitUntil: 'networkidle0'
});
```
