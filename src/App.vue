<script setup lang="ts">
import TheHeader from "@/components/TheHeader.vue";
import EntryEditor from "./components/EntryEditor.vue";
import EntryCard from "@/components/EntryCard.vue";
import type User from "./types/User";
import type Entry from "./types/Entry";

import { provide, reactive } from "vue";
import { userInjectionKey } from "./injectionKeys";

const user: User = reactive({
  id: 1,
  username: "alex-bulanov_io",
  setting: [],
});

provide(userInjectionKey, user);

const entries = reactive<Entry[]>([]);

const handleCreateEntry = (entry: Entry) => {
  entries.unshift(entry);
};
</script>

<template>
  <main class="container m-auto p-10">
    <TheHeader />
    <EntryEditor @create="handleCreateEntry" />
    <ul>
      <li v-for="entry in entries" :key="entry.id">
        <EntryCard :entry="entry" />
      </li>
    </ul>
  </main>
</template>
