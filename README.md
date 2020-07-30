# `tinykeys`

> A tiny (~400 B) & modern library for keybindings.
> [See Demo](https://jamiebuilds.github.io/tinykeys/)

## Install

```sh
npm install --save tinykeys
```

## Usage

```js
import tinykeys from "tinykeys"

tinykeys(window, {
  "Shift+D": () => {
    alert("The 'Shift' and 'd' keys were pressed at the same time")
  },
  "y e e t": () => {
    alert("The keys 'y', 'e', 'e', and 't' were pressed in order")
  },
  "$mod+KeyD": () => {
    alert("Either 'Control+d' or 'Meta+d' were pressed")
  },
})
```

## Commonly used `key`'s and `code`'s

Keybindings will be matched against
[`KeyboardEvent.key`](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key)
and[`KeyboardEvent.code`](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/code/code_values)
which may have some names you don't expect.

| Windows       | macOS           | `key`         | `code`                         |
| ------------- | --------------- | ------------- | ------------------------------ |
| N/A           | `Command` / `⌘` | `Meta`        | `MetaLeft` / `MetaRight`       |
| `Alt`         | `Option` / `⌥`  | `Alt`         | `AltLeft` / `AltRight`         |
| `Control`     | `Control` / `^` | `Control`     | `ControlLeft` / `ControlRight` |
| `Space`       | `Space`         | N/A           | `Space`                        |
| `Shift`       | `Shift`         | `Shift`       | `ShiftLeft` / `ShiftRight`     |
| `1`, `2`, etc | `1`, `2`, etc   | `1`, `2`, etc | `Digit1`, `Digit2`, etc        |
| `a`, `b`, etc | `a`, `b`, etc   | `a`, `b`, etc | `KeyA`, `KeyB`, etc            |
| `Enter`       | `Return`        | `Enter`       | `Enter`                        |
| `Esc`         | `Esc`           | `Escape`      | `Escape`                       |
| `-`           | `-`             | `-`           | `Minus`                        |
| `=`           | `=`             | `=`           | `Equal`                        |
| `+`           | `+`             | `+`           | `Equal`\*                      |

Something missing? Check out the key logger on the
[demo website](https://jamiebuilds.github.io/tinykeys/)

> _\* Some keys will have the same code as others because they appear on the
> same key on the keyboard. Keep in mind how this is affected by international
> keyboards which may have different layouts._

## Keybinding Syntax

Keybindings are made up of a **_sequence_** of **_presses_**.

A **_press_** can be as simple as a single **_key_** which matches against
[`KeyboardEvent.code`](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/code/code_values)
and
[`KeyboardEvent.key`](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key)
(case-insensitive).

```js
// Matches `event.key`:
"d"
// Matches: `event.code`:
"KeyD"
```

Presses can optionally be prefixed with **_modifiers_** which match against any
valid value to
[`KeyboardEvent.getModifierState()`](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/getModifierState).

```js
"Control+d"
"Meta+d"
"Shift+D"
"Alt+KeyD"
"Meta+Shift+D"
```

There is also a special `$mod` modifier that makes it easy to support cross
platform keybindings:

- Mac: `$mod` = `Meta` (⌘)
- Windows/Linux: `$mod` = `Control`

```js
"$mod+D" // Meta/Control+D
"$mod+Shift+D" // Meta/Control+Shift+D
```

### Keybinding Sequences

Keybindings can also consist of several key presses in a row:

```js
"g i" // i.e. "Go to Inbox"
"g a" // i.e. "Go to Archive"
"ArrowUp ArrowUp ArrowDown ArrowDown ArrowLeft ArrowRight ArrowLeft ArrowRight B A"
```

Each press can optionally be prefixed with modifier keys:

```js
"$mod+K $mod+1" // i.e. "Toggle Level 1"
"$mod+K $mod+2" // i.e. "Toggle Level 2"
"$mod+K $mod+3" // i.e. "Toggle Level 3"
```

Each press in the sequence must be pressed within 1000ms of the last.
