<template>
  <div class="book-card" :class="{ completed: book.completed }">
    <div class="book-info">
      <h3>{{ book.title }}</h3>
      <p class="author">{{ book.author }}</p>
      <span class="genre">{{ book.genre }}</span>
    </div>
    <div class="book-actions">
      <!-- Кнопка "Избранное" -->
      <button
          @click="$emit('favorite')"
          :class="['btn', book.favorite ? 'btn-favorite' : 'btn-favorite-outline']"
      >
        {{ book.favorite ? '❤' : '❤' }}
      </button>

      <button
          @click="$emit('toggle')"
          :class="['btn', book.completed ? 'btn-secondary' : 'btn-primary']"
      >
        {{ book.completed ? 'Прочитано' : 'Отметить' }}
      </button>

      <button @click="$emit('delete')" class="btn btn-danger">
        Удалить
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  book: {
    type: Object,
    required: true
  }
})

defineEmits(['toggle', 'delete', 'favorite'])
</script>

<style scoped>
.book-card {
  background: white;
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 12px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: all 0.3s;
}

.book-card:hover {
  box-shadow: 0 4px 8px rgba(0,0,0,0.15);
}

.book-card.completed {
  background: #f0f7f0;
  opacity: 0.8;
}

.book-info {
  flex: 1;
}

.book-info h3 {
  margin-bottom: 4px;
  color: #333;
  font-size: 1.1em;
}

.author {
  color: #666;
  font-size: 0.9em;
  margin-bottom: 4px;
}

.genre {
  background: #e0e0e0;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 0.8em;
  display: inline-block;
}

.book-actions {
  display: flex;
  gap: 8px;
  align-items: center;
  flex-wrap: wrap;
  justify-content: flex-end;
}

.btn {
  padding: 8px 12px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9em;
  transition: all 0.3s;
}

.btn-primary {
  background: #4CAF50;
  color: white;
}

.btn-primary:hover {
  background: #45a049;
  transform: translateY(-1px);
}

.btn-secondary {
  background: #2196F3;
  color: white;
}

.btn-secondary:hover {
  background: #1e87db;
  transform: translateY(-1px);
}

.btn-danger {
  background: #f44336;
  color: white;
  padding: 8px 12px;
}

.btn-danger:hover {
  background: #da190b;
  transform: translateY(-1px);
}

.btn-favorite {
  background: #ff4757;
  color: white;
  border: none;
}

.btn-favorite:hover {
  background: #ff6b81;
  transform: scale(1.05);
}

.btn-favorite-outline {
  background: white;
  border: 1px solid #ff4757;
  color: #ff4757;
}

.btn-favorite-outline:hover {
  background: #ff4757;
  color: white;
  transform: scale(1.05);
}
</style>