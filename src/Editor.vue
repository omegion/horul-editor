<template>
  <div id="horul-editor">
    <div :id="holderId" />
    <button :id="`${holderId}-button`" @click="save" style="display: none;" />
  </div>
</template>

<script>
  import EditorJS from '@editorjs/editorjs'

  const PLUGINS = {
    link: {
      class: require('@editorjs/link'),
      inlineToolbar: true,
    },
    paragraph: {
      class: require('@editorjs/paragraph'),
      inlineToolbar: true,
    },
    header: {
      class: require('@editorjs/header'),
      inlineToolbar: true,
    },
    list: {
      class: require('@editorjs/list'),
      inlineToolbar: true,
    },
    inlineCode: {
      class: require('@editorjs/inline-code'),
      inlineToolbar: true,
    },
    embed: {
      class: require('@editorjs/embed'),
      inlineToolbar: true,
    },
    quote: {
      class: require('@editorjs/quote'),
      inlineToolbar: true,
    },
    marker: {
      class: require('@editorjs/marker'),
      inlineToolbar: true,
    },
    code: {
      class: require('@editorjs/code'),
      inlineToolbar: true,
    },
    delimiter: {
      class: require('@editorjs/delimiter'),
      inlineToolbar: true,
    },
    raw: {
      class: require('@editorjs/raw'),
      inlineToolbar: true,
    },
    table: {
      class: require('@editorjs/table'),
      inlineToolbar: true,
    },
    warning: {
      class: require('@editorjs/warning'),
      inlineToolbar: true,
    },
    image: {
      class: require('@editorjs/image'),
      inlineToolbar: true,
    },
    checklist: {
      class: require('@editorjs/checklist'),
      inlineToolbar: true,
    },
    personality: {
      class: require('@editorjs/personality'),
      inlineToolbar: true,
    },
  }

  const PLUGIN_PROPS_TYPE = {
    type: [Boolean, Object],
    default: () => false,
    required: false,
  }

  export default {
    name: 'horul-editor',
    props: {
      holderId: {
        type: String,
        default: () => 'codex-editor',
        required: false
      },
      autofocus: {
        type: Boolean,
        default: () => false,
        required: false
      },
      initData: {
        type: Object,
        default: () => {},
        required: false
      },
      customTools: {
        type: Object,
        default: () => {},
        required: false
      },
      /**
       * Plugins
       */
      header: PLUGIN_PROPS_TYPE,
      list: PLUGIN_PROPS_TYPE,
      code: PLUGIN_PROPS_TYPE,
      inlineCode: PLUGIN_PROPS_TYPE,
      embed: PLUGIN_PROPS_TYPE,
      link: PLUGIN_PROPS_TYPE,
      marker: PLUGIN_PROPS_TYPE,
      table: PLUGIN_PROPS_TYPE,
      raw: PLUGIN_PROPS_TYPE,
      delimiter: PLUGIN_PROPS_TYPE,
      quote: PLUGIN_PROPS_TYPE,
      image: PLUGIN_PROPS_TYPE,
      warning: PLUGIN_PROPS_TYPE,
      paragraph: PLUGIN_PROPS_TYPE,
      checklist: PLUGIN_PROPS_TYPE
    },
    data() {
      return {
        editor: null
      }
    },
    mounted() {
      this.initEditor();
    },
    methods: {
      initEditor() {
        if (this.editor) {
          this.editor.destroy();
        }
        this.editor = new EditorJS({
          holder: this.holderId,
          autofocus: this.autofocus,
          onReady: () => {
            this.$emit('ready')
          },
          onChange: () => {
            this.$emit('change')
          },
          data: this.initData,
          tools: this.getTools()
        })
      },
      async save() {
        const response = await this.editor.save()
        this.$emit('save', response)
      },
      getTools() {
        const pluginKeys = Object.keys(PLUGINS)
        const isFullyFeatured = pluginKeys.every(p => !this[p])
        const tools = {
          ...this.customTools
        }
        console.log(this.customTools);

        /**
         * When plugin props are empty, enable all plugins
         */
        if (isFullyFeatured) {
          pluginKeys.forEach(key => tools[key] = {
            class: PLUGINS[key].class,
            inlineToolbar: PLUGINS[key].inlineToolbar,
          })
          return tools
        }

        pluginKeys.forEach(key => {
          const props = this.$props[key]
          if (!props) {
            return
          }
          tools[key] = props
        })
        return tools
      }
    },
    watch: {
      initData: function () {
        this.initEditor();
      }
    }
  }
</script>

<style>
  @import './assets/style.scss';
</style>