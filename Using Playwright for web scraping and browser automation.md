# What is Playwright?

<img src="https://playwright.dev/img/playwright-logo.svg" width="100">[Playwright](https://playwright.dev/)

Microsoft Playwright enables fast, reliable and capable automation across all modern browsers. It is an open-source, 
JavaScript-based, cross-browser automation library

* Support for all browsers
* Fast and reliable execution
* Powerful automation capabilities
* Integrates with your workflow

# Step 1: Install & Configure Playwright

## Step 1.1: Install Playwright

- Install Playwright at the project folder

```
$ npm i -D playwright

> playwright@1.11.1 install /Users/hanafiah/Documents/Development/SPLaSK/node_modules/playwright
> node install.js

Downloading chromium v878941 - 115.4 Mb [====================] 100% 0.0s 
chromium v878941 downloaded to /Users/hanafiah/Library/Caches/ms-playwright/chromium-878941
Downloading firefox v1250 - 75.3 Mb [====================] 100% 0.0s 
firefox v1250 downloaded to /Users/hanafiah/Library/Caches/ms-playwright/firefox-1250
Downloading webkit v1472 - 52.6 Mb [====================] 100% 0.0s 
webkit v1472 downloaded to /Users/hanafiah/Library/Caches/ms-playwright/webkit-1472
Downloading ffmpeg v1005 - 1.3 Mb [====================] 100% 0.0s 
ffmpeg v1005 downloaded to /Users/hanafiah/Library/Caches/ms-playwright/ffmpeg-1005
npm WARN splask@1.0.0 No description
npm WARN splask@1.0.0 No repository field.

+ playwright@1.11.1
added 38 packages from 80 contributors and audited 89 packages in 94.527s
```

- Verify from package.json file that Playwright is successfully installed
```
...
  "devDependencies": {
    "playwright": "^1.11.1"
  }
...
```

## Step 1.2: Playwright Inspector

Playwright Inspector is a GUI tool that helps authoring and debugging Playwright scripts. To use the inspector, run the following command:

```
$ npx playwright codegen cloud-connect.asia
```
You should get wthe following window

<img src="/uploads/b24419a2ec39a9b40c81f37ae5981201/image.png" width="400">

# Step 2: Using Playwright

## Step 2.1: First Script

From VS Code, click new file icon to create a file called **playwright.js**

copy the code from Playwright inspector and paste to the file:

```
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch({
    headless: false
  });
  const context = await browser.newContext();

  // Open new page
  const page = await context.newPage();

  // Go to http://www.cloud-connect.asia/
  await page.goto('http://www.cloud-connect.asia/');

  // ---------------------
  await context.close();
  await browser.close();
})();
```
Next, **Save playwright.js**

At the terminal, run the following command
```
$ node playwright.js
```

## Step 2.2: Screenshot website

This step will navigate to CloudConnect website for 3 seconds and get a website screenshot

From VS Code, click new file icon to create a file called **playwright-screenshot.js**

copy the following code snippets and paste to the file:

```
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch({
    headless: false,
    slowMo: 3000
  });
  const context = await browser.newContext();

  // Open new page
  const page = await context.newPage();

  // Go to http://www.cloud-connect.asia/
  await page.goto('http://www.cloud-connect.asia/');
  await page.screenshot({ path: `ujian.png` });

  // ---------------------
  await context.close();
  await browser.close();
})();
```
Next, **Save playwright-screenshot.js**

At the terminal, run the following command
```
$ node playwright-screenshot.js
```

## Step 2.3: Get website content

This step will get CloudConnect copyright text from the footer using element selector

<img src="/uploads/57efa9ef3f21d01f5c1758dd2d28441c/image.png" width="450">

- Tips: to get the element selector for copyright text: select the copyright content as per above image, **right-click -> select Inspect** then follow the steps as image below

<img src="/uploads/bf0b03cca75a1c5fdc842b3897c66316/image.png" width="600">

From VS Code, click new file icon to create a file called **playwright-copyright.js**

copy the following code snippets and paste to the file:

```
const { chromium } = require('playwright');


(async () => {
  const browser = await chromium.launch({
    headless: true
  });
  const context = await browser.newContext();

  // Open new page
  const page = await context.newPage();

  // Go to http://www.cloud-connect.asia/
  await page.goto('http://www.cloud-connect.asia/');

  // find the element selector for footer copyright content
  await page.waitForSelector('#custom_html-2 > h3');

  // get the element selector for footer copyright content
  const copyright = await page.$eval('#custom_html-2 > h3', el => el.textContent.trim())

  console.log('copyright :>> ', copyright);

  // ---------------------
  await context.close();
  await browser.close();
})();
```

Next, **Save playwright-copyright.js**

At the terminal, run the following command and get the result
```
$ node playwright-copyright.js
copyright :>>  ©2009-2021. Cloud Connect Sdn. Bhd. All Rights Reserved.
```

## Step 2.4: Get website tag

This step will check SPLaSK tag from KPLB website

From VS Code, click new file icon to create a file called **playwright-tag.js**

copy the following code snippets and paste to the file:

```
const { chromium } = require('playwright');


(async () => {
   const browser = await chromium.launch({
     headless: false
   });
  const context = await browser.newContext();

  // Open new page
  const page = await context.newPage();
  

  // Go to https://www.rurallink.gov.my/ website
  await page.goto('https://www.rurallink.gov.my/');
  
  
  // sample html
  // <form splwpk-search-function="splwpk-search-function" ....>
  // ...
  // </form>

  // find the <form> element and get splwpk-search-function value
  const tag = await page.getAttribute('form', 'splwpk-search-function')
  console.log('tag :>> ', tag);

  // ---------------------
  //await context.close();
  await browser.close();
})();
```

Next, **Save playwright-tag.js**

At the terminal, run the following command and get the result
```
$ node playwright-tag.js
tag :>>  splwpk-search-function
```
