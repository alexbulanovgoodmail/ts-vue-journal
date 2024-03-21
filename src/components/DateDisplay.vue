<script lang="ts">
// @ts-ignore this works fine
import { formatRelative } from "date-fns";
import { defineComponent } from "vue";
// import { PropType, defineComponent } from "vue";

// import type Entry from "@/types/Entry";

export default defineComponent({
  props: {
    date: { type: Date, required: true },
  },

  // emits: {
  //   doSomething(payload: Entry) {
  //     return payload.body && payload.createdAt;
  //   },
  // },

  computed: {
    formatted(): string {
      // @ts-ignore this works fine
      return formatRelative(this.date, Date.now());
    },
  },

  mounted() {
    this.$http("https://myendpoint.com");
  },
});
</script>

<template>
  <div>{{ formatted }}</div>
</template>
