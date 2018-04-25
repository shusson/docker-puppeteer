# puppeteer docker image for drone ci

docker image with [Google Puppeteer](https://github.com/GoogleChrome/puppeteer) installed and designed to run on drone ci.

[![nodesource/node](http://dockeri.co/image/shusson/puppeteer-drone-ci)](https://hub.docker.com/r/shusson/puppeteer-drone-ci)

## before usage

1. You should pass `--no-sandbox, --disable-setuid-sandbox` args when launch browser

In your tests:

```js
const puppeteer = require('puppeteer');

(async() => {

    const browser = await puppeteer.launch({
        args: [
            '--no-sandbox',
            '--disable-setuid-sandbox'
        ]
    });

    const page = await browser.newPage();

    await page.goto('https://www.google.com/', {waitUntil: 'networkidle2'});

    browser.close();

})();
```

or if you use [jest-puppeteer](https://github.com/smooth-code/jest-puppeteer) then in jest-puppeteer.config.js:

```js
module.exports = {
    launch: {
        args: ["--no-sandbox", "--disable-setuid-sandbox"]
    }
};
```

## usage

Add the image to your pipeline

```yml
  e2e-client:
    image: shusson/puppeteer-drone-ci:1.0.0
    commands:
      - cd app/client/src/test/e2e
      - yarn --no-lockfile
      - yarn run test
```
