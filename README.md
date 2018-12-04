# fast-level-equal

This is a fork of [fast-deep-equal](https://www.npmjs.com/package/fast-deep-equal)

I made this because React's `shouldComponentUpdate` implementation for `PureComponent` is too shallow. It's common for me to pass `style={{...styleDefs}}`, and this create a new object every time, thus `PureComponent` would still update because `this.props.style !== nextProps.style`.

Since `this.props.style` is usually an object that goes one level deep.
Now with this package, I can prevent update on when style didn't change without doing a deep search in case there is a large, deeply nested object.

### Usage

```
import levelEqual from 'fast-level-equal'

const depth = 2

shouldComponentUpdate(nextProps) {
  return !levelEqual(this.props, nextProps, depth)
}
```