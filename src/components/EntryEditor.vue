<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";

// import type { Ref } from "vue";
import { ref, computed } from "vue";

import type Emoji from "@/types/Emoji";

// const emoji: Ref<Emoji | null> = ref(null);
const emoji = ref<Emoji | null>(null);
const text = ref("");

const charCount = computed<number>(() => text.value.length);

const maxChars = 280;

const handleTextInput = (event: Event) => {
  const textarea = event.target as HTMLTextAreaElement;

  if (textarea.value.length <= maxChars) {
    text.value = textarea.value;
  } else {
    text.value = textarea.value = textarea.value.substring(0, maxChars);
  }
};

defineEmits<{
  (e: "create", entry: { text: string; emoji: Emoji | null }): void;
}>();
</script>

<template>
  <form class="entry-form" @submit.prevent="$emit('create', { text, emoji })">
    <textarea
      :value="text"
      placeholder="New Journal Entry for danielkelly_io"
      @keyup="handleTextInput"
    ></textarea>
    <EmojiField v-model="emoji" />
    <div class="entry-form-footer">
      <span>{{ charCount }} / {{ maxChars }}</span>
      <button>Remember <ArrowCircleRight width="20" /></button>
    </div>
  </form>
</template>
