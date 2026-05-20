<script setup lang="ts"></script>
<template>
  <nav class="w-full h-10 flex justify-between px-10 py-8 text-xl font-sf-mono items-center">
    <div class="flex items-center gap-10">
      <div id="buttons" class="flex gap-3 h-full items-center group">
        <!-- Close -->
        <div
          class="relative h-5 aspect-square bg-[#FF605C] rounded-full flex items-center justify-center cursor-pointer hover:brightness-90 transition-all"
        >
          <svg
            class="absolute opacity-0 group-hover:opacity-100 transition-opacity w-3 h-3"
            viewBox="0 0 10 10"
          >
            <line
              x1="2"
              y1="2"
              x2="8"
              y2="8"
              stroke="#8B0000"
              stroke-width="3"
              stroke-linecap="round"
            />
            <line
              x1="8"
              y1="2"
              x2="2"
              y2="8"
              stroke="#8B0000"
              stroke-width="3"
              stroke-linecap="round"
            />
          </svg>
        </div>

        <!-- Minimize -->
        <div
          class="relative h-5 aspect-square bg-[#FFBD44] rounded-full flex items-center justify-center cursor-pointer hover:brightness-90 transition-all"
        >
          <svg
            class="absolute opacity-0 group-hover:opacity-100 transition-opacity w-3 h-3"
            viewBox="0 0 10 10"
          >
            <line
              x1="2"
              y1="5"
              x2="8"
              y2="5"
              stroke="#7A5800"
              stroke-width="3"
              stroke-linecap="round"
            />
          </svg>
        </div>

        <!-- Maximize -->
        <div
          class="relative h-5 aspect-square bg-[#00CA4E] rounded-full flex items-center justify-center cursor-pointer hover:brightness-90 transition-all"
        >
          <svg
            class="absolute opacity-0 group-hover:opacity-100 transition-opacity w-3 h-3"
            viewBox="0 0 10 10"
          >
            <polygon points="0,0 0,7 7,0" fill="#006622" />
            <polygon points="10,10 3,10 10,3" fill="#006622" />
          </svg>
        </div>
      </div>
      <div
        id="name"
        class="tracking-wider hover:drop-shadow-md hover:drop-shadow-dracula-purple cursor-pointer text-center"
      >
        @jamarciniak
      </div>
    </div>
    <!-- <div class="flex w-full text-black">
      <div class="bg-dracula-purple w-fit h-fit px-6 py-1">~/jamarciniak</div>
      <div
        class="w-0 h-0 border-t-[18.5px] border-t-transparent border-b-transparent border-b-[18.5px] border-l-[18.5px] border-l-dracula-purple"
      />
    </div> -->
    <div class="flex gap-15">
      <div>contact</div>
      <div>about me</div>
      <div>projects</div>
    </div>
  </nav>
</template>
