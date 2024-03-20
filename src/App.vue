<script setup lang="ts">
import TheHeader from "@/components/TheHeader.vue";
import EntryEditor from "./components/EntryEditor.vue";
import EntryCard from "@/components/EntryCard.vue";
import type User from "./types/User";

import { reactive } from "vue";
import Entry from "./types/Entry";

const user: User = reactive({
  id: 1,
  username: "alex-bulanov_io",
  setting: [],
});

console.log("user", user.id);

const handleCreateEntry = (entry: Entry) => {
  console.log("entry", entry);
};
</script>

<template>
  <main class="container m-auto p-10">
    <TheHeader />
    <EntryEditor @create="handleCreateEntry" />
    <ul>
      <li>
        <EntryCard />
      </li>
    </ul>
  </main>
</template>
