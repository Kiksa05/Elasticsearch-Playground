<script setup lang="ts">
import { computed, ref } from 'vue'

type Todo = {
  id: number
  text: string
  completed: boolean
}

const items = ref<Todo>([])
const newItem = ref('')
const filter = ref<'all' | 'active' | 'completed'>('all')
let nextId = 1

function addItem() {
  if (newItem.value.trim()) {
    items.value.push({
      id: nextId++,
      text: newItem.value.trim(),
      completed: false
    })
    newItem.value = ''
  }
}

function toggleCompleted(item: Todo) {
  item.completed = !item.completed
}

const remaining = computed(() => {
  return items.value.filter(item => !item.completed).length
})

const filteredItems = computed(() => {
  if (filter.value === 'active') {
    return items.value.filter(item => !item.completed)
  }
  if (filter.value === 'completed') {
    return items.value.filter(item => item.completed)
  }
  return items.value
})


</script>

<template>
  <div>
    <h1>ToDo list</h1>

    <div>
      <ul>
        <li v-for="(item, i) in items" :key="i">{{ item }}
          <!-- <button>Mark as completed</button> -->
        </li>
      </ul>

      <input v-model="newItem" placeholder="Add item" />
      <button @click="addItem">Add</button>

    </div>

    <div>
      <button @click="filter = 'all'">All</button>
      <button @click="filter = 'active'">Active</button>
      <button @click="filter = 'completed'">Completed</button>
    </div>


    <!-- List -->
    <ul>
      <li v-for="item in filteredItems" :key="item.id" :class="{ completed: item.completed }">
        {{ item.text }}
        <button @click="toggleCompleted(item)">Done</button>
      </li>
    </ul>

    <p>{{ remaining }} tasks left</p>
  </div>
</template>

<style scoped>
input {
  margin: 0.5rem 0;
  padding: 0.3rem;
}

button {
  /* margin-left: 0.5rem; */
}

.completed {
  text-decoration: line-through;
  color: gray;
}
</style>
