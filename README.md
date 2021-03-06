<div align="center"><img src="https://raw.githubusercontent.com/retyui/react-native-stylex/master/docs/logo.png" width="456"/></div>

# react-native-stylex

Better styling for react-native

[![npm](https://img.shields.io/npm/v/react-native-stylex.svg)](https://www.npmjs.com/package/react-native-stylex)
[![npm downloads](https://img.shields.io/npm/dm/react-native-stylex.svg)](https://www.npmtrends.com/react-native-stylex)
[![CI](https://github.com/retyui/react-native-stylex/workflows/Node.js%20CI/badge.svg)](https://github.com/retyui/react-native-stylex/actions)

### Module features:

- 📦 Very light and simple;
- ⚡️ Hooks support;
- 🔋 Theming support;
- ⛱️ [Typescript support](docs/ts.md);
- 📝 [Easy integrated with jest](docs/testting.md);
- 💉 CSS Media Queries syntax.

### Links

- [Documentation](docs/api.md);
- [Live demo](https://snack.expo.io/@retyui/react-native-stylex);
- [Example app](example/AppStyleX).

## Install

`react-native-stylex` requires react-native 0.59.0 or later.

#### 1️⃣ Add module

```sh
yarn add react-native-stylex

# or npm install react-native-stylex
```

#### 2️⃣ Add theme `<ThemeProvider/>`

Stylex provides component, which makes the theme available to the rest of your app:

```js
import { ThemeProvider } from "react-native-stylex";

const theme = {
  palette: { textColor: "black" },
  utils: { fade: (color, value) => {} }
};

const Root = () => (
  <ThemeProvider value={theme}>
    <App />
  </ThemeProvider>
);

export default Root;
```

#### 3️⃣ Create styles `makeUseStyles(...)`

Stylex provides a helper function to inject styles to your component.

Normally, you’ll use it in this way:

```js
import { makeUseStyles, maxWidth } from "react-native-stylex";

const useStyles = makeUseStyles(({ palette, utils }) => ({
  root: {
    color: utils.fade(palette.text.textColor, 0.5),
    height: 100,
    // On screens that are 320 or less, set the height to 69
    ...maxWidth(320, { height: 69 })
  },
  // Another syntax, `.row` property would be `null` or passed object
  point: maxWidth(320, { height: 4, width: 4 })
}));

export default useStyles;
```

#### 4️⃣ Inject styles `useStyles(...)` & `withStyles(...)`

And finally just use in component:

```js
import React, { Component } from "react";
import useStyles from "./styles";

// Functional component (hooks variant)
const Root = () => {
  const styles = useStyles();

  return <View style={styles.root} />;
};

export default Root;

//--------------------------------

// Class component (HOC variant)
class Root extends Component {
  render() {
    const { styles } = this.props;

    return <View style={styles.row} />;
  }
}

export default withStyles(useStyles)(Root);
```
