# horul-editor

horul-editor is editorjs wrapper component.

Please see this first. https://editorjs.io/

## Supported Plugins

- [Header](https://github.com/editor-js/header)
- [List](https://github.com/editor-js/list)
- [Image](https://github.com/editor-js/image)
- [InlineCode](https://github.com/editor-js/inline-code)
- [Embed](https://github.com/editor-js/embed)
- [Quote](https://github.com/editor-js/quote)
- [Marker](https://github.com/editor-js/marker)
- [Code](https://github.com/editor-js/code)
- [Link](https://github.com/editor-js/link)
- [Delimiter](https://github.com/editor-js/delimiter)
- [Raw](https://github.com/editor-js/raw)
- [Table](https://github.com/editor-js/table)
- [Warning](https://github.com/editor-js/warning)
- [Paragraph](https://github.com/editor-js/paragraph)
- [Checklist](https://github.com/editor-js/checklist)
- [Personality](https://github.com/editor-js/personality)

## Installation

```bash
npm install --save horul-editor

# or Yarn
yarn add horul-editor
```

## Usage

```js
// In main.js
// ...
import Editor from 'horul-editor'

Vue.use(Editor)
// ...
```

```js
// In component
// ...
import { Editor } from 'horul-editor'

export default {
  components: {
    Editor,
  }
}
// ...
```

```Vue
  <editor
    autofocus
    holder-id="codex-editor"
    save-button-id="save-button"
    :init-data="initData"
    @save="save"
    @ready="onReady"
    @change="onChange"
  />
```

---

```js
// on Nuxt.js

// in nuxt.config.js
plugins: [
  {
    src: '~/plugins/vue-editor.js', ssr: false
  }
],

// in ~/plugins/vue-editor.js
import Vue from 'vue'
import Editor from 'horul-editor'

Vue.use(Editor)

// in your page
<editor />

```

### Other props:
- customTools - Object with name (key) and class of a custom tool (value)