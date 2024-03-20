<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";

// import type { Ref } from "vue";
import { ref, computed } from "vue";

import type Entry from "@/types/Entry";
import type Emoji from "@/types/Emoji";

// const emoji: Ref<Emoji | null> = ref(null);
const emoji = ref<Emoji | null>(null);
const body = ref("");

const charCount = computed<number>(() => body.value.length);

const maxChars = 280;

const handleTextInput = (event: Event) => {
  const textarea = event.target as HTMLTextAreaElement;

  if (textarea.value.length <= maxChars) {
    body.value = textarea.value;
  } else {
    body.value = textarea.value = textarea.value.substring(0, maxChars);
  }
};

const emit = defineEmits<{
  (e: "create", entry: Entry): void;
}>();

const handleSubmit = () => {
  emit("create", {
    body: body.value,
    emoji: emoji.value,
    createdAt: new Date(),
    userId: 1,
    id: Math.random(),
  });

  body.value = "";
  emoji.value = null;
};
</script>

<template>
  <form class="entry-form" @submit.prevent="handleSubmit">
    <textarea
      :value="body"
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
