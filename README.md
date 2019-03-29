# use-visibility-change

A custom React Hook that provides easy access to the visibilitychange event.
Know how long it's been since a user has "seen" your app.

[![npm version](https://badge.fury.io/js/%40use-it%2Fevent-listener.svg)](https://badge.fury.io/js/%40use-it%2Fevent-listener) [![All Contributors](https://img.shields.io/badge/all_contributors-3-orange.svg?style=flat-square)](#contributors)

## Features

🕐 Know how long the user has been away from your page.

🕑 `saveCallback` called when the user changes tabs, closes the current tab, or minimizes the browser.

🕒 `restoreCallback` when the page is once again visible to the user (passing the `lastSeenDate`).

🕓 Persists `lastSeenDate` to `localStorage`.

This hook was inspired by this article on [Web Platorm News](https://webplatform.news/issues/2019-03-27#web-pages-can-now-detect-when-chrome-s-window-is-covered-by-another-window).


## Installation

```bash
$ npm i use-visibility-change
```

or

```bash
$ yarn add use-visibility-change
```

## Usage

Here is a basic setup.

```js
const data = useVisibilityChange(saveCallback, restoreCallback);
```

### Parameters

Here are the parameters that you can use. (\* = optional)

| Parameter   | Description                                                                                     |
| :---------- | :---------------------------------------------------------------------------------------------- |
| `saveCallback` | An optional callback function that is called upon closing or navigation away from the current tab, or minimizing the browser. You could use this callback to save the application state. |
| `restoreCallback` | An optional callback function that is called with `data` when the view is restored. You could use this callback to restore the application state, or reset the user's experience if they have been gone for some time. |

### Return

This hook returns a data object with the following keys.

| Property   | Description                                                                                     |
| :---------- | :---------------------------------------------------------------------------------------------- |
| `lastSeenDate` | A Date object representing the date that the user was last "seen". Returns `null` if this is the first time the user visited your site with this browser. |

## Example

Here we have a simple case where we render how long it's been since the user has "seen" your app.

```js
const App = () => {
  const { lastSeenDate } = useVisibilityChange();
  return (
    <div>
      <p>
        Obsure the complete browser window, change tabs, navigate away, or close
        the tab.
      </p>
      {lastSeenDate ? (
        <>
          <p className="hidden-for">
            This page was hidden for{' '}
            <em>{((new Date() - lastSeenDate) / 1000).toFixed(2)} secs</em>
          </p>
          <p>Last seen on: {lastSeenDate.toISOString()}</p>
        </>
      ) : (
        'Welcome new user!'
      )}
    </div>
  );
};
```

## Live demo

You can view/edit the sample code above on CodeSandbox.

[![Edit demo app on CodeSandbox](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/vm6l68k427)

## License

**[MIT](LICENSE)** Licensed
