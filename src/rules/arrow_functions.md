## Anonymous Functions

Use arrow function notation for anonymous functions e.g. when passing an inline callback. It creates a version of the function that executes in the context of this which is usually the desired functionality, and is a more concise syntax.

When dealing with a fairly complicated function, it is recommended to move that logic out into its own named function expression.

> ESLint: [prefer-arrow-callback][eslint/prefer-arrow-callback] and [arrow-spacing][eslint/arrow-spacing]

###### Examples

⇣ **Incorrect** code for this rule:

```js
[1, 2, 3].map(function (number) {
  const nextNumber = number + 1;
  return number * nextNumber;
});
```

⇡ **Correct** code for this rule:

```js
[1, 2, 3].map(number => {
  const nextNumber = number + 1;
  return number * nextNumber;
});
```

## Implicit Return

If the function body consists of a single statement returning an [expression][mdn-expressions_and_operators] without side effects, omit the braces and use the implicit return. Otherwise use a `return` statement. This rule is syntactic sugar and significantly increases the readability when multiple functions are chained together.

> ESLint: [arrow-parens][eslint/arrow-parens] and [arrow-body-style][eslint/arrow-body-style]

###### Examples

⇣ **Incorrect** code for this rule:

```js
["snow", "frost"].map(element => {
  const nextElement = element;
  `The winter season has ${nextElement}.`;
});
```

```js
let isFalling = false;

snow(() => isFalling = true);
```

⇡ **Correct** code for this rule:

```js
["snow", "frost"].map(element => `The winter season has ${element}.`);
```

```js
["snow", "frost"].map(element => {
  const sparklingElement = `sparkling ${element}`;
  return `The winter season has ${sparklingElement}.`;
});
```

```js
["snow", "frost"].map((element, index) => ({
  [index]: element
}));
```

```js
// No implicit return with side effects.
function seasons(callback) {
  const season = callback();
  if (season === "snow") {
    // ...
  }
}
```

```js
let isFalling = false;

snow(() => {
  isFalling = true;
});
```

## Parentheses Wrap

In case the expression spans over multiple lines, wrap it in parentheses for better readability. This shows clearly where the function starts and ends.

###### Examples

⇣ **Incorrect** code for this rule:

```js
["snow", "frost", "ice"].map(element => Object.prototype.hasOwnProperty.call(
    elementObjectWithAVeryLongName,
    element
  )
);
```

⇡ **Correct** code for this rule:

```js
["snow", "frost", "ice"].map(element => (
  Object.prototype.hasOwnProperty.call(
    elementObjectWithAVeryLongName,
    element
  )
));
```

## Single Argument Parentheses

If a function takes a single argument and doesn't use braces, omit the parentheses. Otherwise, always include parentheses around arguments for clarity and consistency.

> ESLint: [arrow-parens][eslint/arrow-parens]

###### Examples

⇣ **Incorrect** code for this rule:

```js
["snow", "frost"].map((element) => `sparkling ${element}`);
```

```js
["snow", "frost"].map((element) => {
  const sparkling = "sparkling";
  return `${sparkling} ${element}`;
});
```

⇡ **Correct** code for this rule:

```js
["snow", "frost"].map(element => `sparkling ${element}`);
```

```js
["snow", "frost"].map(element => (
  `A long string about the winter season with sparkling ${element}. It's so long that we don't want it to take up space on the ".map()" line!`
));
```

## Comparison Operators Confusion

Avoid confusing arrow function syntax `=>` with comparison operators (`<=`, `>=`).

> ESLint: [no-confusing-arrow][eslint/no-confusing-arrow]

###### Examples

⇣ **Incorrect** code for this rule:

```js
const elementDensity = element => element.density > 256 ? element.highDensity : element.lowDensity;
```

```js
const elementDensity = (element) => element.density > 256 ? element.highDensity : element.lowDensity;
```

⇡ **Correct** code for this rule:

```js
const elementDensity = element => (element.density > 256 ? element.highDensity : element.lowDensity);
```

```js
const elementDensity = element => {
  const { density, highDensity, lowDensity } = element;
  return density > 256 ? highDensity : lowDensity;
};
```

[eslint/arrow-body-style]: https://eslint.org/docs/rules/arrow-body-style
[eslint/arrow-parens]: https://eslint.org/docs/rules/arrow-parens
[eslint/arrow-spacing]: https://eslint.org/docs/rules/arrow-spacing
[eslint/no-confusing-arrow]: https://eslint.org/docs/rules/no-confusing-arrow
[eslint/prefer-arrow-callback]: https://eslint.org/docs/rules/prefer-arrow-callback
[mdn-expressions_and_operators]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions