# Pong Wars: The Great Wave off Kanagawa edition

🌊 [Play the demo](https://tsopeh.github.io/pong-wars-kanagawa/) 🌊

https://github.com/tsopeh/pong-wars-kanagawa/assets/37545996/7a3df98c-3d63-4459-a5e0-98c3c7c990e4

## The story 📜🪶

This is a [Pong Wars](https://github.com/vnglst/pong-wars) clone inspired by The Great Wave off Kanagawa.

I stumbled upon this [post](https://x.com/vnglst/status/1751278052154179770) and immediately wanted to create my own version. I was even more interested when I saw the [implementation](https://github.com/vnglst/pong-wars): it was a single HTML file with some vanilla JS in a _script_ tag; the OG way of building. As a long time Typescript user, I developed a habit of dismissing the idea of building something in vanilla JS, but I wanted to see for myself if I could implement my version with a similar setup, while preserving most of Typescript's ergonomics via [JSDoc](https://jsdoc.app/tags-param) comments.

## Key takeaways for Typescript developers 🚀

> [!NOTE]
> tldr; `// @ts-check` and JSDoc comments are _sometimes_ all you need.

By utilizing the following tips you can work in the plain JS projects and still get most of the usual Typescript benefits: code autocomplete, navigate to references, safely rename symbols, etc. 😌

### ✨ @ts-check ✨

Write the `// @ts-check` comment before anything else. Place it at the beginning of the HTML's script tag and at the beginning of all JS files. This _special comment_ will be interpreted by your editor, so it will automatically apply the type checking analysis, as if you're writing JS in a TS project. This analysis works out of the box in both VS Code and WebStorm (VS Code works better for script tags), no need to install anything extra; no editor plugins or `npm` packages. You don't even need the `package.json` for this to work. Find out more [here](https://www.typescriptlang.org/docs/handbook/intro-to-js-ts.html#ts-check).

### 🔥 @typedef 🔥

**You can define new types in JS!** This is the reason why I'm writing this whole thing; more people need to know about it. 📣

With JSDoc, you can define custom types and later annotate code with those types. Read more [here](https://jsdoc.app/tags-typedef).

```javascript
// Define type `State` (the name goes at the end of type declaration).
/**
 * @typedef {{
 *   player1: Player
 *   player2: Player
 *   board: Board
 * }} State
 */

// Use the `State` type to anotate variables, funcrion params and return types.
  
/** @type {State} */
const state = {...}

/**
 * @param state {State}
 */
function recalculateState(state) {...}

/** @returns {State} */
function getInitialState() {...}
```

You can now find all usages/references of the `State` type, and safely rename its props.

### Generic functions 🧩

You can even define generic functions.

```javascript
/**
 * @template T
 * @param arr {Array<T>}
 * @returns {T}
 */
function randomArrayItem (arr) {...}
```

### Function overrides 🎢

You can even have function signature overrides. E.g. a RNG function can accept a single argument: a `max`, for the range `[0, max]`; or it can accept two arguments: `min` and `max`, for the range `[min, max]`.

```javascript
/**
 * @overload
 * @param max {number}
 * @returns {number}
 */
/**
 * @overload
 * @param min {number}
 * @param max {number}
 * @returns {number}
 */
/**
 * @param min {number}
 * @param [max] {number}
 * @returns {number}
 */
function randomFloat (min, max) {...}
```

### What if my project grows a bit? 📈

At some point you will wish to split your code across multiple JS files. Writing `// @ts-check` everywhere and the lack of the control over type checking can get annoying. Luckily you can get many benefits of Typescript by simply creating a `tsconfig.josn` file in your project's root; you don't need to install anything — just create the config file, the editor will pick it up.

```json
// `tsconfig.json`
{
  "compilerOptions": {
    "target": "es2016",
    "module": "commonjs",
    "allowJs": true,
    "checkJs": true,
    "strict": true,
    "skipLibCheck": true,
    "noEmit": true
  }
}
```

### Serve the project 🚀

Any http server will do. E.g.

```bash
npx serve

# or

python3 -m http.server
```

## Happy hacking! 🎉

Feel free to share this with your hacker friends and colleagues. 🙌 🥳
