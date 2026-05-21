<script setup lang="ts">
import cv from '@/assets/cv.json'
import { ref, onMounted, type Ref } from 'vue'

const fullText = 'cat cv.json'
const typedText = ref('')
const isIdle = ref(true)
const isTypingDone = ref(false)
const visibleLines = ref(0)
const scrollRef = ref<HTMLElement | null>(null)

const sleep = (ms: number) => new Promise<void>((resolve) => setTimeout(resolve, ms))

const typeText = ({
  text,
  output,
  onDone,
  speed = 110,
  initialDelay = 800,
}: {
  text: string
  output: Ref<string>
  onDone?: () => void
  speed?: number
  initialDelay?: number
}) =>
  new Promise<void>((resolve) => {
    setTimeout(() => {
      let i = 0
      const interval = setInterval(() => {
        output.value = text.slice(0, ++i)
        if (i >= text.length) {
          clearInterval(interval)
          onDone?.()
          resolve()
        }
      }, speed)
    }, initialDelay)
  })

const revealLines = ({
  total,
  output,
  onLine,
  speed = 30,
  initialDelay = 200,
}: {
  total: number
  output: Ref<number>
  onLine?: () => void
  speed?: number
  initialDelay?: number
}) =>
  new Promise<void>((resolve) => {
    setTimeout(() => {
      const interval = setInterval(() => {
        output.value++
        onLine?.()

        if (output.value >= total) {
          clearInterval(interval)
          resolve()
        }
      }, speed)
    }, initialDelay)
  })

const highlightedLines = highlight(JSON.stringify(cv, null, 2)).split('\n')

onMounted(async () => {
  await sleep(1200)

  isIdle.value = false
  await typeText({
    text: fullText,
    output: typedText,
    onDone: () => (isTypingDone.value = true),
  })

  await sleep(300)

  await revealLines({
    total: highlightedLines.length,
    output: visibleLines,
    onLine: () => {
      if (scrollRef.value) scrollRef.value.scrollTop = scrollRef.value.scrollHeight
    },
  })
})

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
</script>

<template>
  <main class="p-8 font-sf-mono flex-1 min-h-0 overflow-hidden flex flex-col">
    <div class="p-6 border-4 rounded-2xl border-white flex-1 min-h-0 flex flex-col">
      <div class="flex w-full items-center gap-4 shrink-0">
        <div class="flex items-center">
          <div class="bg-dracula-purple px-6 py-1.5 text-xl tracking-wide text-black leading-none">
            ~/jamarciniak
          </div>
          <div
            class="w-0 h-0 border-t-16 border-t-transparent border-b-16 border-b-transparent border-l-16 border-l-dracula-purple self-stretch"
          />
        </div>
        <div class="text-white text-xl flex items-center">
          <span>{{ typedText }}</span>
          <span :class="['ml-0.5', isIdle || isTypingDone ? 'animate-blink' : '']">▋</span>
        </div>
      </div>

      <div
        ref="scrollRef"
        class="pt-4 text-white text-xl font-sf-mono mt-4 overflow-y-auto flex-1 min-h-0"
      >
        <pre class="whitespace-pre-wrap"><span
            v-for="(line, i) in highlightedLines"
            v-show="i < visibleLines"
            :key="i"
            v-html="line + '\n'"
          /></pre>
      </div>
    </div>
  </main>
</template>
<style>
@keyframes blink {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0;
  }
}
.animate-blink {
  animation: blink 1s step-start infinite;
}
</style>
