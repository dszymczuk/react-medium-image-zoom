# ⚠️  WARNING
The `master` branch currently represents the work-in-progress for version `4.0`.
It is completely unstable and should not be used by anyone except contributors.

The `v4.0` work is being tracked on the project board:
https://github.com/rpearce/react-medium-image-zoom/projects/1

The latest stable published version is located on the [v3.x
branch](https://github.com/rpearce/react-medium-image-zoom/tree/v3.x).

# react-medium-image-zoom

[![All Contributors](https://img.shields.io/badge/all_contributors-22-orange.svg?style=flat-square)](#contributors-)
[![npm version](https://img.shields.io/npm/v/react-medium-image-zoom.svg)](https://www.npmjs.com/package/react-medium-image-zoom) [![npm downloads](https://img.shields.io/npm/dm/react-medium-image-zoom.svg)](https://www.npmjs.com/package/react-medium-image-zoom) [![Build Status](https://travis-ci.org/rpearce/react-medium-image-zoom.svg?branch=master)](https://travis-ci.org/rpearce/react-medium-image-zoom) [![Coverage Status](https://coveralls.io/repos/github/rpearce/react-medium-image-zoom/badge.svg?branch=master)](https://coveralls.io/github/rpearce/react-medium-image-zoom?branch=master) [![Maintainability](https://api.codeclimate.com/v1/badges/8e4debef4b9f0e8acd6e/maintainability)](https://codeclimate.com/github/rpearce/react-medium-image-zoom/maintainability) [![Gitter](https://badges.gitter.im/react-medium-image-zoom/community.svg)](https://gitter.im/react-medium-image-zoom/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

This library is a [`React.js`](https://reactjs.org/) implementation of
[Medium.com's image
zoom](https://medium.com/design/image-zoom-on-medium-24d146fc0c20) that allows
for low-resolution and high-resolution images to work together for a “zooming”
effect and works regardless of parent elements that have `overflow: hidden` or
[parents with transform properties](https://codepen.io/rpearce/pen/MEyOmb).

As an added bonus, it will let you zoom _anything_ (see the [`Storybook
Examples`](https://rpearce.github.io/react-medium-image-zoom/) for more).

## Links
* [Installation](#installation)
* [Basic Usage](#basic-usage)
* [API](#api)
* [Contributors](#contributors)
* [Storybook Examples](https://rpearce.github.io/react-medium-image-zoom/)
* [Authors](./AUTHORS.md)
* [Changelog](./CHANGELOG.md)
* [Contributing](./CONTRIBUTING.md)
* [Code of Conduct](./CODE_OF_CONDUCT.md)

## Installation
```bash
$ npm i react-medium-image-zoom@alpha
```
or
```bash
$ yarn add react-medium-image-zoom@alpha
```

## Basic Usage

### Uncontrolled component (default)
Import the component and the CSS, wrap whatever you want to be "zoomable" with
this component and the component will handle it's own state:

```js
import React, { useState } from 'react'
import Zoom from 'react-medium-image-zoom'
import 'react-medium-image-zoom/dist/styles.css'

const MyComponent = () => (
  <Zoom>
    <img
      alt="that wanaka tree"
      src="/path/to/thatwanakatree.jpg"
      width="500"
    />
  </Zoom>
)

export default MyComponent
```

### Controlled component (`Controlled`)
Import the `Controlled` component and the CSS, wrap whatever you want to
be "zoomable" with this component and then dictate the zoomed/unzoomed state to
the component. Here, we will automatically zoom the component once the image has
loaded:

```js
import React, { useCallback, useState } from 'react'
import { Controlled as ControlledZoom } from 'react-medium-image-zoom'
import 'react-medium-image-zoom/dist/styles.css'

const MyComponent = () => {
  const [isZoomed, setIsZoomed] = useState(false)

  const handleImgLoad = useCallback(() => {
    setIsZoomed(true)
  }, [])

  const handleZoomChange = useCallback(shouldZoom => {
    setIsZoomed(shouldZoom)
  }, [])

  return (
    <ControlledZoom isZoomed={isZoomed} onZoomChange={handleZoomChange}>
      <img
        alt="that wanaka tree"
        onLoad={handleImgLoad}
        src="/path/to/thatwanakatree.jpg"
        width="500"
      />
    </ControlledZoom>
  )
)

export default MyComponent
```

## API

## Both uncontrolled & controlled components
You can pass these options to either the default or controlled components.

| Prop | Type | Required | Default  | Details |
| ---  | --- | ---  | --- | --- |
| `closeText` | `String` | no | `'Unzoom Image'` | Accessible label text for when you want to unzoom |
| `openText` | `String` | no | `'Zoom Image'` | Accessible label text for when you want to zoom |
| `overlayBgColorEnd` | `String` | no | `'rgba(255, 255, 255, 0.95)'` | Modal overlay background color at end of zoom |
| `overlayBgColorStart` | `String` | no | `'rgba(255, 255, 255, 0)'` | Modal overlay background color at start of zoom |
| `portalEl` | `Element` | no | `document.body` | [DOM Element](https://developer.mozilla.org/en-US/docs/Web/API/element) to which we will append the zoom modal |
| `scrollableEl` | `Window` | no | `window` | [DOM Element](https://developer.mozilla.org/en-US/docs/Web/API/element) to which we will listen for scroll events to determine if we should unzoom |
| `transitionDuration` | `Number` | no | `300` | Transition duration in milliseconds for the component to use on zoom and unzoom |
| `wrapStyle` | `Object` | no | `null` | Optional style object to pass to the wrapper `div`. Useful when you want the `<Zoom>` container to be `width: '100%'`, for example |
| `zoomMargin` | `Number` | no | `0` | Offset in pixels the zoomed image should be from the `window`' boundaries |
| `zoomZindex` | `Number` | no | `2147483647` | `z-index` value for the zoom overlay |

## Only the controlled component
You can pass these options to only the controlled component.

| Prop | Type | Required | Default  | Details |
| ---  | --- | ---  | --- | --- |
| `isZoomed` | `bool` | yes | `false` | Tell the component whether or not it should be zoomed |
| `onZoomChange` | `Function` | no | `Function.prototype` | Listen for hints from the component about when you should zoom (`true` value) or unzoom (`false` value) |

## Contributors

Thanks goes to these wonderful people ([emoji key](https://github.com/kentcdodds/all-contributors#emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/cbothner"><img src="https://avatars1.githubusercontent.com/u/4642599?v=4" width="100px;" alt=""/><br /><sub><b>Cameron Bothner</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=cbothner" title="Code">💻</a> <a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=cbothner" title="Documentation">📖</a> <a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Acbothner" title="Bug reports">🐛</a> <a href="#example-cbothner" title="Examples">💡</a> <a href="#ideas-cbothner" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/rpearce/react-medium-image-zoom/pulls?q=is%3Apr+reviewed-by%3Acbothner" title="Reviewed Pull Requests">👀</a> <a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=cbothner" title="Tests">⚠️</a></td>
    <td align="center"><a href="https://github.com/jeremybini"><img src="https://avatars2.githubusercontent.com/u/12982155?v=4" width="100px;" alt=""/><br /><sub><b>Jeremy Bini</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=jeremybini" title="Code">💻</a> <a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Ajeremybini" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://ismaywolff.nl"><img src="https://avatars1.githubusercontent.com/u/7355199?v=4" width="100px;" alt=""/><br /><sub><b>ismay</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Aismay" title="Bug reports">🐛</a> <a href="#ideas-ismay" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="https://www.qeek.co"><img src="https://avatars0.githubusercontent.com/u/220647?v=4" width="100px;" alt=""/><br /><sub><b>Rajit Singh</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Arajit" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/rsaccon"><img src="https://avatars1.githubusercontent.com/u/16122?v=4" width="100px;" alt=""/><br /><sub><b>Roberto Saccon</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Arsaccon" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/wtfdaemon"><img src="https://avatars0.githubusercontent.com/u/6598350?v=4" width="100px;" alt=""/><br /><sub><b>wtfdaemon</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Awtfdaemon" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://robertwpearce.com"><img src="https://avatars2.githubusercontent.com/u/592876?v=4" width="100px;" alt=""/><br /><sub><b>Robert Pearce</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=rpearce" title="Code">💻</a> <a href="#question-rpearce" title="Answering Questions">💬</a> <a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=rpearce" title="Tests">⚠️</a> <a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Arpearce" title="Bug reports">🐛</a> <a href="#example-rpearce" title="Examples">💡</a> <a href="#design-rpearce" title="Design">🎨</a> <a href="https://github.com/rpearce/react-medium-image-zoom/pulls?q=is%3Apr+reviewed-by%3Arpearce" title="Reviewed Pull Requests">👀</a> <a href="#ideas-rpearce" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=rpearce" title="Documentation">📖</a></td>
  </tr>
  <tr>
    <td align="center"><a href="http://www.joshsloat.com"><img src="https://avatars1.githubusercontent.com/u/606159?v=4" width="100px;" alt=""/><br /><sub><b>Josh Sloat</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Ajoshsloat" title="Bug reports">🐛</a> <a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=joshsloat" title="Code">💻</a> <a href="#example-joshsloat" title="Examples">💡</a> <a href="https://github.com/rpearce/react-medium-image-zoom/pulls?q=is%3Apr+reviewed-by%3Ajoshsloat" title="Reviewed Pull Requests">👀</a> <a href="#ideas-joshsloat" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=joshsloat" title="Documentation">📖</a> <a href="#design-joshsloat" title="Design">🎨</a> <a href="#question-joshsloat" title="Answering Questions">💬</a></td>
    <td align="center"><a href="https://github.com/aswinckr"><img src="https://avatars1.githubusercontent.com/u/5960217?v=4" width="100px;" alt=""/><br /><sub><b>Aswin</b></sub></a><br /><a href="#question-aswinckr" title="Answering Questions">💬</a></td>
    <td align="center"><a href="https://github.com/alexshelkov"><img src="https://avatars3.githubusercontent.com/u/1233347?v=4" width="100px;" alt=""/><br /><sub><b>Alex Shelkovskiy</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Aalexshelkov" title="Bug reports">🐛</a></td>
    <td align="center"><a href="http://adrian-design.com"><img src="https://avatars1.githubusercontent.com/u/7365629?v=4" width="100px;" alt=""/><br /><sub><b>Adrian Bindiu</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3ASnowsoul" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/kendagriff"><img src="https://avatars3.githubusercontent.com/u/110935?v=4" width="100px;" alt=""/><br /><sub><b>Kendall Buchanan</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Akendagriff" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/HippoDippo"><img src="https://avatars2.githubusercontent.com/u/25674779?v=4" width="100px;" alt=""/><br /><sub><b>Kaycee</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=HippoDippo" title="Code">💻</a></td>
    <td align="center"><a href="http://shuffle.do"><img src="https://avatars2.githubusercontent.com/u/9633371?v=4" width="100px;" alt=""/><br /><sub><b>Anuj</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Aoyeanuj" title="Bug reports">🐛</a> <a href="#question-oyeanuj" title="Answering Questions">💬</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/ludwigfrank"><img src="https://avatars1.githubusercontent.com/u/10273946?v=4" width="100px;" alt=""/><br /><sub><b>Ludwig Frank</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Aludwigfrank" title="Bug reports">🐛</a> <a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=ludwigfrank" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/serfgy"><img src="https://avatars2.githubusercontent.com/u/20569525?v=4" width="100px;" alt=""/><br /><sub><b>LX</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Aserfgy" title="Bug reports">🐛</a> <a href="#ideas-serfgy" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="http://www.rosentomov.com"><img src="https://avatars3.githubusercontent.com/u/5452135?v=4" width="100px;" alt=""/><br /><sub><b>Rosen Tomov</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3AbabyPrince" title="Bug reports">🐛</a></td>
    <td align="center"><a href="http://tommoor.com"><img src="https://avatars2.githubusercontent.com/u/380914?v=4" width="100px;" alt=""/><br /><sub><b>Tom Moor</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=tommoor" title="Code">💻</a> <a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Atommoor" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/jpreynat"><img src="https://avatars2.githubusercontent.com/u/7927876?v=4" width="100px;" alt=""/><br /><sub><b>Johan Preynat</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=jpreynat" title="Code">💻</a> <a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Ajpreynat" title="Bug reports">🐛</a></td>
    <td align="center"><a href="http://rahulgaba.com"><img src="https://avatars3.githubusercontent.com/u/7898942?v=4" width="100px;" alt=""/><br /><sub><b>Rahul Gaba</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=rgabs" title="Code">💻</a> <a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Argabs" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/spencerfdavis"><img src="https://avatars3.githubusercontent.com/u/1526292?v=4" width="100px;" alt=""/><br /><sub><b>Spencer Davis</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=spencerfdavis" title="Code">💻</a> <a href="#ideas-spencerfdavis" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/rpearce/react-medium-image-zoom/pulls?q=is%3Apr+reviewed-by%3Aspencerfdavis" title="Reviewed Pull Requests">👀</a> <a href="#design-spencerfdavis" title="Design">🎨</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/dnlnvl"><img src="https://avatars2.githubusercontent.com/u/39607648?v=4" width="100px;" alt=""/><br /><sub><b>dnlnvl</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/commits?author=dnlnvl" title="Code">💻</a></td>
    <td align="center"><a href="http://tomorrowstudio.co"><img src="https://avatars3.githubusercontent.com/u/6374876?v=4" width="100px;" alt=""/><br /><sub><b>Sean King</b></sub></a><br /><a href="#ideas-seaneking" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="https://github.com/0x6e6562"><img src="https://avatars3.githubusercontent.com/u/14088?v=4" width="100px;" alt=""/><br /><sub><b>Ben Hood</b></sub></a><br /><a href="#ideas-0x6e6562" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3A0x6e6562" title="Bug reports">🐛</a> <a href="#example-0x6e6562" title="Examples">💡</a> <a href="https://github.com/rpearce/react-medium-image-zoom/pulls?q=is%3Apr+reviewed-by%3A0x6e6562" title="Reviewed Pull Requests">👀</a></td>
    <td align="center"><a href="http://puthir.in"><img src="https://avatars2.githubusercontent.com/u/45002?v=4" width="100px;" alt=""/><br /><sub><b>Navilan</b></sub></a><br /><a href="#ideas-navilan" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="https://github.com/13806"><img src="https://avatars1.githubusercontent.com/u/31736960?v=4" width="100px;" alt=""/><br /><sub><b>13806</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3A13806" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://www.twitter.com/deadcoder0904"><img src="https://avatars1.githubusercontent.com/u/16436270?v=4" width="100px;" alt=""/><br /><sub><b>Akshay Kadam (A2K)</b></sub></a><br /><a href="https://github.com/rpearce/react-medium-image-zoom/issues?q=author%3Adeadcoder0904" title="Bug reports">🐛</a> <a href="#ideas-deadcoder0904" title="Ideas, Planning, & Feedback">🤔</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/kentcdodds/all-contributors) specification. Contributions of any kind welcome!
