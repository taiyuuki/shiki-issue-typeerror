<script setup>
import { onMounted, ref } from 'vue'
import { initMonaco } from './monaco';
import { getHighlighter } from 'shiki'
import { shikiToMonaco } from '@shikijs/monaco'

const monaco_demo = ref(null)

onMounted(async () => {
    const monaco = initMonaco()
    monaco.editor.create(monaco_demo.value, {
        model: monaco.editor.createModel('Hello World!', 'javascript'),
    })

    const highlighter = await getHighlighter({
        themes: [
            // 'vitesse-dark', // works
            'github-dark-default', // error
            'github-dark-dimmed', // error
            'vesper' // error
        ],
    })

    shikiToMonaco(highlighter, monaco)

    monaco.editor.setTheme('github-dark-default')
})

</script>

<template>
  <div>
    <div style="height: 100vh;width: 100vw" ref="monaco_demo"></div>
  </div>
</template>
