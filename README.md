# Video Background Play Fix  ![logo](/icon.svg)

Android web browsers can continue playing video even if you switch to another tab or app.
However, sites can detect these user actions with the [Page Visibility API](https://developer.mozilla.org/en-US/docs/Web/API/Page_Visibility_API) and the [Fullscreen API](https://developer.mozilla.org/en-US/docs/Web/API/Fullscreen_API).
This userscript is designed to block events and properties exposed by the APIs.

## How to Install
1. Install a script manager such as [Violentmonkey](https://chrome.google.com/webstore/detail/violentmonkey/jinjaccalgkegednnccohejagnlnfdag).
2. [Click here](https://github.com/Delphox/video-bg-play-userscript/raw/master/video-bg-play.user.js) to install the userscript.

NOTE: installing to your Chromium browser natively via the Extensions page might work but isn't supported. Chromium built in userscript support is very barebones, using a script manager is preferable.

## License

Userscript code: MIT.

"[Glasses](https://thenounproject.com/term/glasses/1473422)" icon used in the logo by rahmatmasiv from [the Noun Project](https://thenounproject.com/)  under the [CC BY 3.0 US](https://creativecommons.org/licenses/by/3.0/us/).

## Technical detail

The userscript injects a content script to replace the properties exposed, and stops events from propagating when applicable.

### Page Visibility API

The userscript blocks `visibilitychange` event, and set `document.hidden` to be always `false` and `document.visibilityState` to be forever `visible`.

### Fullscreen API

The userscript doesn't generally override the Fullscreen API because at the moment this is not required and the original implementation caused some broken UI after existing fullscreen.
As a site-specific workaround, we do however block `fullscreenchange` events on Vimeo to prevent playback from stopping when exiting fullscreen.

### User activity tracking

Some pages stop playback if they don't detect any user activity for a certain amount of time. To avoid this, the add-on ensures that the time of the last user activity is regularly updated.

## Sites

As a demonstration, the content script currently injects itself to the following sites:

* youtube.com and youtube-nocookie.com
* vimeo.com
