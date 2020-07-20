<template>
  <q-page class="page-quasar-tiptap-basic">
    <section class="row col-12 justify-center">
      <header class="row col-12 justify-center items-center bg-blue text-white banner">
        <span class="text-h3">Lưu Nguyyễn</span>
      </header>
      <section class="row col-10 q-pa-md">
        <quasar-tiptap v-bind="options" @update="onUpdate" />
      </section>

      <div v-html="html"></div>

      <h2>________________________________________________</h2><br/>
      <div>
        <textarea v-model="formula" cols="30" rows="10"></textarea>
        <vue-mathjax :formula="formula"></vue-mathjax>
      </div>
    </section>
  </q-page>
</template>

<script>
import Vue from 'vue'
import { QuasarTiptapPlugin, RecommendedExtensions } from 'quasar-tiptap'
import { VueMathjax } from 'vue-mathjax'

Vue.use(QuasarTiptapPlugin, {
  language: 'zh-hans',
  spellcheck: true
})

// import { QuasarTiptap, RecommendedExtensions } from 'quasar-tiptap'
import 'quasar-tiptap/lib/index.css'

import {
  Placeholder,
} from 'tiptap-extensions'

export default {
  name: 'page-quasar-tiptap-basic',
  data () {
    return {
      formula: '$$x = {-b \\pm \\sqrt{b^2-4ac} \\over 2a}.$$',
      msg: 'Welcome to Your Vue.js App',
      options: {
        title: 'xxx',
        content: 'Hello',
        editable: true,
        extensions: [
          ...RecommendedExtensions,
          new Placeholder({
            showOnlyCurrent: false,
            emptyNodeText: node => {
              if (node.type.name === 'title') {
                return 'Title'
              }
              return 'Content'
            }
          }),
        ],
        toolbar: [
          'add-more',
          'separator',
          'bold',
          'italic',
          'underline',
          'strike',
          'code',
          'separator',
          'heading',
          'font-family',
          'fore-color',
          'back-color',
          'format_clear',
          'separator',
          'align-dropdown',
          'indent',
          'outdent',
          'line-height',
          'separator',
          'horizontal',
          'bullet_list',
          'ordered_list',
          'todo_list',
          'separator',
          'blockquote',
          'code_block',
          'photo',
          'table',
          'separator',
          'undo',
          'redo',
        ]
      },
      json: '',
      html: ''
    }
  },
  components: {
    // QuasarTiptap
    'vue-mathjax': VueMathjax
  },
  methods: {
    onUpdate ({ getJSON, getHTML }) {
      this.json = getJSON()
      this.html = getHTML()
      console.log('json', this.json)
    }
  },
  mounted () {
    console.log('mounted', this.$o)
    this.$o.lang.set('en-us')
  },

  watch: {
    formula (newValue, oldValue) {
      this.options.content = {type: 'text', text: newValue};
    }
  },
}
</script>

<style lang="stylus">
  .page-quasar-tiptap-basic {
    .banner {
      height 100px
    }

    .tiptap {
      border solid 1px #eeeeee
      border-radius 6px
    }

    .editor-scroll-area {
      position absolute
      top 40px
      left 0
      right 0
      bottom 0
      background #f7f8fa
    }
  }
</style>