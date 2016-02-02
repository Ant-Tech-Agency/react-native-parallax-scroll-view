[![](https://img.shields.io/npm/dm/react-native-parallax-scroll-view.svg?style=flat-square)](https://www.npmjs.com/package/react-native-parallax-scroll-view)

# react-native-parallax-scroll-view

A `ScrollView`-like component that:

- Has a parallax header
- Has an optional sticky header
- Is composable with any component that expects a `ScrollView` (e.g. `ListView` or [`InfiniteScrollView`](https://github.com/exponentjs/react-native-infinite-scroll-view))
- Can be nested within other views
- Works on iOS and Android

(Tested with react-native 0.16.0 on Android and iOS.

## Installation

```
$ npm install react-native-parallax-scroll-view --save
```

## Demo


| iOS | Android |
| --- | ------- |
| ![](./demo.ios.gif) | ![](./demo.android.20160117.gif) |

## Basic Usage

```js
import ParallaxScrollView from 'react-native-parallax-scroll-view';

// Inside of a component's render() method:
render() {
  return (
    <ParallaxScrollView
      backgroundColor="blue"
      contentBackgroundColor="pink"
      parallaxHeaderHeight={300}
      renderParallaxHeader={() => (
       <View style={{ height: 300, flex: 1, alignItems: 'center', justifyContent: 'center' }}>
          <Text>Hello World!</Text>
        </View>
      )}>
      <View style={{ height: 500 }}>
        <Text>Scroll me</Text>
      </View>
    </ParallaxScrollView>
  );
}
```

## Examples

Please refer to the [ListView example](./examples/ListView/Talks.js) provided to see how `ParallaxScrollView` can be used in
combination with `ListView`.

The [Android ListView example](./examples/ListView/index.android.js) shows how you can use `PullToRefreshViewAndroid` with `ParallaxScrollView`.

There are more examples in the [examples](./examples) folder.

## Usage (API)

All of the properties of `ScrollView` are supported. Please refer to the
[`ScrollView` documentation](https://facebook.github.io/react-native/docs/scrollview.html) for more detail.

The `ParallaxScrollView` component adds a few additional properties, as described below.

| Property | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| `parallaxHeaderHeight` | `number` | **Yes** |This is the height of parallax header. |
| `renderBackground` | `func` | No | This renders the background of the parallax header. Can be used to display cover images for example. (Defaults to an opaque background using `backgroundColor`) |
| `backgroundSpeed` | `number` | No | The speed factor that the background moves at relative to the foreground. Defaults to 5. |
| `renderForeground` |  `func` | No |This renders the foreground header that moves at same speed as scroll content. |
| `renderStickyHeader` | `func` | No | This renders an optional sticky header that will stick to the top of view when parallax header scrolls up. |
| `stickyHeaderHeight` | `number` | If `renderStickyHeader` is used | If `renderStickyHeader` is set, then its height must be specified. |
| `renderFixedHeader` | `func` | No | This renders an optional fixed header that will always be visible and fixed to the top of the view (and sticky header). You must set its height and width appropriately. |
| `renderScrollComponent` | `func` | No | A function with input `props` and outputs a `ScrollView`-like component in which the content is rendered. This is useful if you want to provide your own scrollable component. (See: [https://github.com/exponentjs/react-native-scrollable-mixin](https://github.com/exponentjs/react-native-scrollable-mixin)) (By default, returns a `ScrollView` with the given props) |
| `contentBackgroundColor` | `string` | No | This is the background color of the content. (Defaults to `'#fff'`) |
| `onChangeHeaderVisibility` | `func` | No | A callback function that is invoked when the parallax header is hidden or shown (as the user is scrolling). Function is called with a `boolean` value to indicate whether header is visible or not. |

## Changelog

### 0.17.0

- Refactored parallax header calculations to keep their scroll speeds consistent with user scroll speed.
- Parallax effect is now calculated using the `backgroundSpeed` prop.
