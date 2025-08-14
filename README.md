# Notify-Native-js

**Notify Native.js** is a simple and lightweight library that allows you to display various notifications on the screen — from a new message to service notifications.

## Features

- 🎨 6 ready-made styles + custom
- 📌 4 screen positions
- 🔔 Built-in sounds + custom
- 🕒 Flexible notification closing system
- 🛠️ Action buttons with handlers
- 📱 Responsive design
- 🚀 No dependencies

## Installation

1. Download the library from the repository
2. Connect the library files:
```html
<link rel="stylesheet" href="notify-native.min.css">
<script src="notify-native.min.js"></script>
```

## Quick start

1. Create an instance of the `Notify()` object without parameters:

```javascript
const notify = new Notify(); // creates a notification display area in the default position (corner: `top_right`, maxElem: 5)
```

2. Call the `render()` method of the `Notify()` object without parameters:

```javascript
notify.render(); // creates a notification with default parameters (header: `Hi, I'm the Notify Native — JS library.`, style: 'dark', type: {closed: false})
```

## Main parameters

The `Notify()` object has 2 parameters: `corner` and `maxElem`. The table below describes them:

| Parameter | Default | Type | Description |
|:-----|:-----|:-----------|:-----| 
| corner | `top_right` | string | Sets the position of the notification display area: `top_right`, `top_left`, `bottom_right`, `bottom_left` |
| maxElem | 5 | number | Maximum number of simultaneously displayed notifications |

## Notification parameters (`render()` method)	

The `render()` method has several parameters listed below:

| Parameter | Default | Type | Description |
|:-----|:-----|:-----------|:-----| 
| header | Hi, I'm the Notify Native — JS library. | string | Notification header |
| content | false | object / false | Content object (see table below) |
| ctaBtn | false | object / false | Action button parameters object (see table below) |
| style | `dark` | string | Notification style: `dark`, `light`, `info`, `success`, `warning`, `danger`, `custom` |
| sound | false | boolean / string | Play sound: `true` - default sound, string - path to a custom sound file |
| type | `{closed: false}` | object | Closing parameters (see table below) |

## `content` parameter

The `content` parameter of the `render()` method is `false` by default, but you can also pass an object with the following properties:

| Parameter | Type | Description |
|:-----|:-----|:-----------|
| text | string | Notification text (long text is automatically truncated to 150 characters) |
| image	 | string | Image URL for the notification |

## `ctaBtn` parameter

The `ctaBtn` parameter of the `render()` method is `false` by default, but you can also pass an object with the following properties:

| Parameter | Type | Description |
|:-----|:-----|:-----------|
| title | string | Button text (required) |
| url | string | Redirect URL (optional) |
| target | string | `target` attribute (e.g. `_blank`) |
| onClick | `function(e, notification)` | Click handler function |

## `type` parameter

The `type` parameter of the `render()` method is `{closed: false}` by default, but you can also pass an object with the following properties:

| Parameter | Default | Type | Description |
|:-----|:-----|:-----------|:-----| 
| closed | false | boolean | Show close button |
| delay | undefined | number / undefined | Auto-close time (ms) |

## Appearance customization

Add the following classes and properties to your project's stylesheet:
```css
:root {
  --custom-bg-color: rgb(46, 66, 80);
  --custom-bg-btn-color: rgba(23, 40, 52, 0.85);
  --custom-text-color: rgb(175, 204, 224);
}

.alert-custom {
  background-color: var(--custom-bg-color);
  color:  var(--custom-text-color);
}
.alert-custom .closeBtn {
  background-color: var(--custom-bg-btn-color);
  color:  var(--custom-text-color);
}  
.alert-custom .closeBtn > svg > path {
  fill: var(--custom-text-color);
}
.alert-custom .ctaBtn {
  background-color: var(--custom-bg-btn-color);
  color:  var(--custom-text-color);
}
.alert-custom a {
  color: var(--custom-text-color);
}
```
To use the custom theme when calling the `render()` method, set the `style` parameter to `'custom'`.

## Usage examples
### Info notification with a header and text

```javascript
notify.render({
    header: 'ℹ️ Info',
    content: {
        text: 'A new user has registered'
        },
    style: 'info'
})
```

### Notification with header, text, image, and link using the `custom` theme

```javascript
notify.render({
    header: 'Mount Elbrus',
    type: {
        closed: true,
        delay: 10000
    },
    content: {
        text: 'Elbrus is the highest mountain peak in Russia and Europe if the boundary between Europe and Asia is drawn along or south of the Greater Caucasus Mountain Range (otherwise, the highest peak in Europe is considered Mont Blanc in the Alps).',
        image: `elbrus.jpg`
    },
    ctaBtn: {
        title: 'Go to Encyclopedia',
        url: `https://en.wikipedia.org/wiki/Mount_Elbrus`,
        target: '_blank'
    },
    style: 'custom'
})
```

### Error warning

```javascript
notify.render({
    header: 'Error',
    type: {
        closed: true
    },
    content: {
        text: 'Failed to save data, please try again later.'
    },
    style: 'danger'
})
```

### Notification with a button to hide the notification

```javascript
notify.render({
    header: 'Notification',
    content: {
        text: 'Action completed'
        },
    type: {
        closed: true,
        delay: 10000
    },
    ctaBtn: {
        title: 'Ok',
        onClick: function(e, notification) { notify.hideAndRemove(notification) }
    },
    style: 'success'
})
```

### Service notification with page reload function

```javascript
notify.render({
    header: 'Notification',
    content: {
        text: 'Data successfully entered into the database'
    },
    type: {
        closed: true,
        delay: 10000
    },
    ctaBtn: {
        title: 'Reload the page?', 
        onClick: function() { window.location.reload() }
    },
    style: 'light'
})
```
