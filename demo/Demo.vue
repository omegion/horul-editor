<template>
  <div class="demo">
    <button @click="save">Save & Log</button>
    <button @click="load">Load</button>
    <button @click="loadData">Load Example</button>
    <editor :autofocus="true" :init-data="initData" ref="editor" @save="onSave"
    @ready="onReady" @change="onChange"/>
  </div>
</template>

<script>
  import {
    Editor
  } from '../src' // import { Editor } from 'horul-editor'

  export default {
    components: {
      Editor,
    },
    data() {
      return {
        initData: {
          "time": 1567071477422,
          "blocks": [{
              "type": "header",
              "data": {
                "text": "Horul.js",
                "level": 2
              }
            },
            {
              "type": "paragraph",
              "data": {
                "text": "Classic WYSIWYG-editors produce raw HTML-markup with both content data and content appearance. On the contrary, Editor.js outputs JSON object with data of each Block. You can see an example below"
              }
            },
            {
              "type": "image",
              "data": {
                "file": {
                  "url": "https://codex.so/upload/redactor_images/o_e48549d1855c7fc1807308dd14990126.jpg"
                },
                "caption": "",
                "withBorder": true,
                "stretched": false,
                "withBackground": false
              }
            }
          ],
          "version": "2.15.0"
        },
        savedData: {},
        plugins: {
          image: {
            class: require('@editorjs/image'),
            inlineToolbar: false,
          },
          header: {
            class: require('@editorjs/header'),
            inlineToolbar: false,
          },
        },
      }
    },
    mounted() {
      this.loadData()
    },
    methods: {
      save() {
        this.$refs.editor.save();
      },
      load() {
        this.initData = this.savedData;
      },
      loadData() {},
      onSave(response) {
        console.log(JSON.stringify(response))
        this.savedData = response;
        console.log('saved')
      },
      onReady() {
        console.log('ready')
      },
      onChange() {
        console.log('changed')
      }
    }
  }
</script>

<style>

</style>