<template>
  <div class="filters">
    <div class="search">
      <input
          v-model="searchQueryLocal"
          type="text"
          placeholder="Поиск по названию или автору..."
      />
    </div>

    <div class="filter-buttons">
      <button
          v-for="option in filterOptions"
          :key="option.value"
          @click="updateFilter(option.value)"
          :class="['filter-btn', { active: filter === option.value }]"
      >
        {{ option.label }}
      </button>
    </div>

    <div class="stats">
      <p>Всего: {{ total }} | Прочитано: {{ completed }} | Осталось: {{ total - completed }} | ❤ Избранное: {{ favoriteCount }}</p>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  filter: {
    type: String,
    default: 'all'
  },
  books: {
    type: Array,
    required: true
  },
  searchQuery: {
    type: String,
    default: ''
  }
})

const emit = defineEmits(['update:filter', 'update:searchQuery'])

const filterOptions = [
  { value: 'all', label: 'Все' },
  { value: 'unread', label: 'Непрочитанные' },
  { value: 'read', label: 'Прочитанные' },
  { value: 'favorite', label: '❤ Избранные' }
]

const total = computed(() => props.books.length)
const completed = computed(() => props.books.filter(b => b.completed).length)
const favoriteCount = computed(() => props.books.filter(b => b.favorite).length)

const searchQueryLocal = computed({
  get: () => props.searchQuery,
  set: (value) => {
    emit('update:searchQuery', value)
  }
})

const updateFilter = (value) => {
  emit('update:filter', value)
}
</script>

<style scoped>
.filters {
  background: #f9f9f9;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  margin-bottom: 20px;
}

.search {
  margin-bottom: 15px;
}

.search input {
  width: 100%;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 1em;
  transition: border-color 0.3s;
}

.search input:focus {
  outline: none;
  border-color: #4CAF50;
}

.filter-buttons {
  display: flex;
  gap: 10px;
  margin-bottom: 15px;
  flex-wrap: wrap;
}

.filter-btn {
  padding: 8px 16px;
  border: 1px solid #ddd;
  background: white;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s;
  font-size: 0.9em;
}

.filter-btn:hover {
  background: #f0f0f0;
  transform: translateY(-1px);
}

.filter-btn.active {
  background: #4CAF50;
  color: white;
  border-color: #4CAF50;
}

.stats {
  padding-top: 15px;
  border-top: 1px solid #eee;
  color: #666;
  font-size: 0.9em;
  text-align: center;
}
</style>