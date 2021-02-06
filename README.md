<h1 align="center">Adobe Animate React component</h1>

[![npm](https://badgen.net/npm/v/react-adobe-animate)](https://www.npmjs.com/package/react-adobe-animate)
[![npm](https://badgen.net/npm/dt/react-adobe-animate)](https://www.npmjs.com/package/react-adobe-animate)
[![npm](https://badgen.net/npm/dm/react-adobe-animate)](https://www.npmjs.com/package/react-adobe-animate)
[![Snyk Vulnerabilities for GitHub Repo](https://img.shields.io/snyk/vulnerabilities/github/bibixx/react-adobe-animate)](https://snyk.io/test/github/bibixx/react-adobe-animate)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)
[![Commitizen friendly](https://badgen.net/badge/commitizen/friendly/green)](http://commitizen.github.io/cz-cli/)

> The component for embedding animations from Adobe Animate.

## Installation

`npm install -S react-adobe-animate`

## Examples

* [Simple implementation (codesandbox.io)](https://githubbox.com/bibixx/react-adobe-animate/tree/master/example)

## Dependencies

* React
* CreateJS – add this to your page `<script src="https://code.createjs.com/1.0.0/createjs.min.js"></script>`
* Your animation – add .js file exported from Adobe Animate to page with `<script>` tag

## How to use
### Example
#### index.html
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>React Adobe Animate exmaple</title>
  </head>
  <body>
    <div id="root"></div>
    <script src="https://code.createjs.com/1.0.0/createjs.min.js" type="text/javascript"></script>
    <script src="./lishtml5-with-background.js" type="text/javascript"></script>
    <script src="./lishtml5.js" type="text/javascript"></script>
  </body>
</html>

```

#### App.tsx
```tsx
import { useState } from "react";
import AnimateCC, { GetAnimationObjectParameter } from "react-adobe-animate";

const App = () => {
  const [paused, setPaused] = useState(true);
  const [animationObject, getAnimationObject] = useState<GetAnimationObjectParameter|null>(null);
  const onClick = () => setPaused(!paused);

  console.log(animationObject);

  return (
    <div style={{ width: "400px" }}>
      <AnimateCC
        animationName="lishtml5"
        getAnimationObject={getAnimationObject}
        paused={paused}
      />

      <AnimateCC
        animationName="lishtml5"
        composition="C1475B64B160904BB90B34246A5FF54B"
        paused={paused}
      />

      <button onClick={onClick}>{paused ? "Unpause" : "Pause"}</button><br />
    </div>
  );
};
```

### Next.js
To use the component with [Next.js](https://github.com/vercel/next.js/) you have to include CreateJS and Animate files (you have to put those into `public` folder first) in `Head` component.

#### pages/index.tsx
```tsx
import { useState } from "react";
import Head from 'next/head';
import AnimateCC, { GetAnimationObjectParameter } from "react-adobe-animate";

export default function Home() {
  const [paused, setPaused] = useState(true);
  const [animationObject, getAnimationObject] = useState<GetAnimationObjectParameter|null>(null);
  const onClick = () => setPaused(!paused);

  console.log(animationObject);

  return (
    <div style={{ width: "400px" }}>
      <Head>
        <script src="https://code.createjs.com/1.0.0/createjs.min.js" type="text/javascript"></script>
        <script src="/lishtml5.js" type="text/javascript"></script>
        <script src="/lishtml5-with-background.js" type="text/javascript"></script>
      </Head>

      <AnimateCC
        animationName="lishtml5"
        getAnimationObject={getAnimationObject}
        paused={paused}
      />

      <AnimateCC
        animationName="lishtml5"
        composition="C1475B64B160904BB90B34246A5FF54B"
        paused={paused}
      />

      <button onClick={onClick}>{paused ? "Unpause" : "Pause"}</button><br />
    </div>
  );
}
```

### Props

| Prop name | Type | Required | Description  |
| --------- | ---- | -------- | ------------ |
| animationName | string | true | Name of animation (`exportRoot = new lib.animationName();` in js file. There the name is `(lib.animationName = function`. Also usually name of published file) |
composition | string | false | If you have two animations with same name you can specify an id of that animation. You can get it from .html file generate by Adobe Animate (`var comp=AdobeAn.getComposition("C1475B64B160904BB90B34246A5FF54B");`) |
| getAnimationObject | function | false | It is fired after component was mounted. It takes 1 argument – animation object that enables you to fire functions created in Adobe Animate
paused | boolean | false | Whether an animation should be paused

All other props will be passed to div surrounding canvas

### FAQ

#### How do I insert animations published from the same file?

Unfortunately it isn't possible to export from Adobe Animate two unique animations. However you can make one! Simply replace all occurrences of composition id inside your .js file of an animation to one created by you. Composition id is this long string in `var comp=AdobeAn.getComposition("C1475B64B160904BB90B34246A5FF54B");` found in .html file published by Adobe Animate.

## 🤝 Contributing

Contributions, issues and feature requests are welcome!\
Feel free to check [issues page](https://github.com/bibixx/react-adobe-animate/issues).

For development purposes you can use the `example` folder. \
You'll find instructions on how to use it in [`example/README.md`](https://github.com/bibixx/react-adobe-animate/blob/master/example/README.md)

## Show your support

Give a ⭐️ if this project helped you!

## 📝 License

Copyright © 2019-2020 [bibixx](https://github.com/bibixx) <bartosz+a.github@legiec.io>.<br />
This project is [MIT](https://github.com/bibixx/react-adobe-animate/blob/master/LICENSE.md) licensed.
