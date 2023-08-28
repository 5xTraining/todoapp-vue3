<script>
import { v4 as uuidv4 } from "uuid"
import TodoItem from "./components/TodoItem.vue"

export default {
  data() {
    return {
      todo: "",
      todos: [],
    }
  },
  methods: {
    addTask() {
      if (this.todo.trim() != "") {
        const item = { id: uuidv4(), title: this.todo, completed: false }
        this.todos.unshift(item)
        this.todo = ""
      }
    },
    removeTask(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id)
    },
    toggleComplete(id) {
      const todo = this.todos.find((todo) => {
        return todo.id == id
      })
      todo.completed = !todo.completed
    },
  },
  components: { TodoItem },
}
</script>

<template>
  <main class="container mx-auto">
    <header class="m-2">
      <h1 class="text-6xl font-thin select-none">TODO!</h1>
      <div class="font-semibold select-none text-neutral-600">simple and studid todo app</div>
    </header>
    <form class="px-10 py-12 bg-white shadow-sm">
      <section class="flex">
        <input type="text" v-model="todo" placeholder="做點重要的事吧..." class="w-full text-2xl focus:outline-none input-lg input input-bordered" />
        <button @click.prevent="addTask" class="text-xl btn-lg btn btn-neutral">新增</button>
      </section>
    </form>

    <section class="px-10 py-6 mt-4 bg-white">
      <ul>
        <TodoItem
          v-for="todo in todos"
          @removeItem="removeTask"
          @toggleComplete="toggleComplete"
          :id="todo.id"
          :title="todo.title"
          :completed="todo.completed"
        />
      </ul>
    </section>
  </main>
</template>

<style scoped></style>
