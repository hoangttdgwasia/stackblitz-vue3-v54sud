<script>
export default {
  data() {
    return {
      newtodoEntrie: '',
      editedTodo: null,
      todoEntries: []
    }
  },
  methods: {
    addtodoEntrie() {
      if (this.newtodoEntrie.trim() !== '') {
        this.todoEntries.push({
          id: Date.now(),
          title: this.newtodoEntrie,
          status: 'In progress',
          createday: new Date().toLocaleString(),
          lastModify: new Date().toLocaleString(),
          completed: false,
          buttonCompleted: 'Complete',
        })
        this.newtodoEntrie = ''
      }
    },
    removetodoEntrie(todoEntrie) {
      const index = this.todoEntries.indexOf(todoEntrie)
      if (index > -1) {
        this.todoEntries.splice(index, 1)
      }
    },
    toggleCompletion(todoEntrie) {
      if ((todoEntrie.completed = !todoEntrie.completed)) {
        todoEntrie.status = 'Completed'
        todoEntrie.buttonCompleted = 'In progress'
      } else {
        todoEntrie.status = 'In progress'
        todoEntrie.buttonCompleted = 'Complete'
      }
    },
    editTaskName(todoEntrie) {
      this.editedTodo = todoEntrie
    },
    doneEditTaskName(todoEntrie) {
      if (!this.editedTodo) {
        return
      }
      this.editedTodo = null
      todoEntrie.title = todoEntrie.title.trim()
      todoEntrie.lastModify = new Date().toLocaleString()
      if (!todoEntrie.title) {
        this.removetodoEntrie(todoEntrie)
      }
    }
  }
}
</script>
<template>
  <div
    id="todoEntrie"
    class="max-w-screen-lg mx-auto bg-white shadow-lg rounded-lg overflow-hidden mt-16"
  >
    <div class="px-4 py-2">
      <h1 class="text-gray-800 font-bold text-2xl uppercase">To-Do List</h1>
    </div>
    <form class="w-full max-w-sm mx-auto px-4 py-2">
      <div class="flex items-center border-b-2 border-teal-500 py-2">
        <input
          v-model="newtodoEntrie"
          class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
          type="text"
          placeholder="Add a task"
        />
        <button
          @click="addtodoEntrie"
          class="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
          type="button"
        >
          Add
        </button>
      </div>
    </form>

    <div class="flex flex-col">
      <div class="overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 sm:px-6 lg:px-8">
          <div class="overflow-hidden">
            <table class="min-w-full text-left text-sm font-light text-surface dark:text-white">
              <thead class="border-b border-neutral-200 font-medium dark:border-white/10">
                <tr>
                  <th scope="col" class="px-6 py-4">Rank</th>
                  <th scope="col" class="px-6 py-4">TASK</th>
                  <th scope="col" class="px-6 py-4">STATUS</th>
                  <th scope="col" class="px-6 py-4">CREATE DAY</th>
                  <th scope="col" class="px-6 py-4">LAST MODIFY DAY</th>
                  <th scope="col" class="px-6 py-4">ACTION</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  class="border-b border-neutral-200 dark:border-white/10"
                  v-for="(todoEntrie, index) in todoEntries"
                  :key="todoEntrie.id"
                >
                  <td class="whitespace-nowrap px-6 py-4 font-medium">{{ index + 1 }}</td>
                  <td class="whitespace-nowrap px-6 py-4 relative cursor-pointer" @dblclick="editTaskName(todoEntrie)">
                    {{ todoEntrie.title }}
                    <input
                      v-model="todoEntrie.title"
                      :class="{ showTyping: todoEntrie === editedTodo}"
                      type="text"
                      class="peer top-1/2 hidden -translate-y-2/4 top-1 w-96 left-0 absolute h-14 bg-white rounded-[7px] border border-blue-gray-200 px-3 font-sans text-sm font-normal text-blue-gray-700"
                      placeholder=" "
                    />
                  </td>
                  <td
                    class="whitespace-nowrap px-6 py-4 font-bold"
                    :class="{
                      'text-blue-500': todoEntrie.completed,
                      'text-green-900': !todoEntrie.completed
                    }"
                  >
                    {{ todoEntrie.status }}
                  </td>
                  <td class="whitespace-nowrap px-6 py-4">{{ todoEntrie.createday }}</td>
                  <td class="whitespace-nowrap px-6 py-4">{{ todoEntrie.lastModify }}</td>
                  <td class="whitespace-nowrap px-6 py-4">
                    <div class="flex flex-1 gap-2">
                      <button
                        @click="toggleCompletion(todoEntrie)"
                        class="flex-shrink-0 bg-green-500 hover:bg-teal-700 border-green-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
                        type="button"
                      >
                        {{ todoEntrie.buttonCompleted }}
                      </button>
                      <button
                      @click="doneEditTaskName(todoEntrie)"
                        class="flex-shrink-0 bg-yellow-500 hover:bg-teal-700 border-yellow-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
                        type="button"
                      >
                        Update
                      </button>
                      <button
                        @click="removetodoEntrie(todoEntrie)"
                        class="flex-shrink-0 bg-red-500 hover:bg-teal-700 border-red-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
                        type="button"
                      >
                        Remove
                      </button>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.showTyping {
  display:  block !important;
}
</style>