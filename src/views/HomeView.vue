<script setup lang="ts">
import cv from '@/assets/cv.json'

function highlight(json: string): string {
  return json
    .replace(/&/g, '&amp;')
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;')
    .replace(
      /("(\\u[a-zA-Z0-9]{4}|\\[^u]|[^\\"])*"(\s*:)?|\b(true|false|null)\b|-?\d+(?:\.\d*)?(?:[eE][+-]?\d+)?|[{}[\],:])/g,
      (match) => {
        if (match.startsWith('"')) {
          if (match.endsWith(':')) {
            return `<span class="text-lonely-key">${match}</span>`
          }
          return `<span class="text-lonely-string">${match}</span>`
        }
        if (/true|false/.test(match)) {
          return `<span class="text-lonely-boolean">${match}</span>`
        }
        if (/null/.test(match)) {
          return `<span class="text-lonely-null">${match}</span>`
        }
        if (/[{}[\]]/.test(match)) {
          return `<span class="text-lonely-punctuation">${match}</span>`
        }
        if (/[:,]/.test(match)) {
          return `<span class="text-lonely-punctuation">${match}</span>`
        }
        return `<span class="text-lonely-number">${match}</span>`
      },
    )
}

const highlighted = highlight(JSON.stringify(cv, null, 2))
</script>

<template>
  <main class="p-8 font-sf-mono">
    <div class="p-6 border-4 rounded-2xl border-white">
      <div class="flex w-full text-black items-center gap-4">
        <div class="flex">
          <div class="bg-dracula-purple w-fit h-fit px-6 py-1.5 font text-xl tracking-wide">
            ~/jamarciniak
          </div>
          <div
            class="w-0 h-0 border-t-20 border-t-transparent border-b-transparent border-b-20 border-l-20 border-l-dracula-purple"
          />
        </div>
        <div class="text-white text-xl h-full">cat cv.json</div>
      </div>

      <div class="pt-4 text-white text-xl font-sf-mono mt-4">
        <pre class="whitespace-pre-wrap" v-html="highlighted" />
      </div>
    </div>
  </main>
</template>
