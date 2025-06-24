<script setup lang="ts">
import { computed, ref } from 'vue'

const search = ref('')
const contacts = ref ([
  { id: 1, name: "Alice Anderson" },
  { id: 2, name: "Bob Builder" },
  { id: 3, name: "Charlie Chaplin" },
  { id: 4, name: "Diana Developer" }
])

const filteredContacts = computed(() => {
  return contacts.value.filter(contact =>
    contact.name.toLowerCase().includes(search.value.toLowerCase())
  )
})

function hightlightMatch(name:string): string {
  if(!search.value) return name

  const escaped = search.value.replace(/[.*+?^${}()|[\]\\]/g, '\\$&')
  const regex = new RegExp(`(${escaped})`, 'gi')
  return name.replace(regex, '<mark>$1</mark>')
}


</script>

<template>
  <div>
    <h1>Contact Search</h1>

    <div>
  

      <!-- Search  -->
      <input v-model="search" placeholder="Search contacts..." />

      <ul>
        <li v-for="contact in filteredContacts" :key="contact.id"
          v-html="hightlightMatch(contact.name)">
        </li>
      </ul>

      <p v-if="filteredContacts.length === 0">No contacts found</p>

    </div>

  </div>
</template>

<style scoped>
input {
  margin: 0.5rem 0;
  padding: 0.3rem;
}


.completed {
  text-decoration: line-through;
  color: gray;
}

</style>
