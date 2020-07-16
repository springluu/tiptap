<template>
  <q-page class="page-quasar-tiptap-basic">
    <section class="row col-12 justify-center">
      <header class="row col-12 justify-center items-center bg-blue text-white banner">
        <span class="text-h3">Lưu Nguyyễn</span>
      </header>
      <section class="row col-10 q-pa-md">
        <quasar-tiptap v-bind="options" @update="onUpdate" />
      </section>
    </section>
  </q-page>
</template>

<script>
import Vue from 'vue'
import { QuasarTiptapPlugin, RecommendedExtensions } from 'quasar-tiptap'

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
      options: {
        content: 'hoho',
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
  },
  methods: {
    onUpdate ({ getJSON, getHTML }) {
      this.json = getJSON()
      this.html = getHTML()
      console.log('html', this.html)
    }
  },
  mounted () {
    console.log('mounted', this.$o)
    this.$o.lang.set('en-us')
  }
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