<template>
  <div>
    <h4 class="text-3xl font-normal leading-normal mt-0 mb-2 text-amber-800">
      Vue ToDo App
    </h4>

    <input
      type="text"
      placeholder="Enter your todo task.."
      class="border py-2 px-3 text-grey-darkest md:ml-2"
      v-model="task"
    />

    <button
      class="py-2 px-8 bg-green-400 text-white font-bold"
      @click="submitTask"
    >
      Create
    </button>
  </div>
  <div>
    <div class="container flex justify-center mx-auto">
      <div class="flex flex-col">
        <div class="w-full">
          <table class="divide-y divide-gray-300">
            <tbody class="bg-white divide-y divide-gray-300">
              <tr v-for="(task, index) in tasks" :key="index">
                <td>
                  <span :class="{ 'line-through': task.status === 'finished' }">
                    {{ task.name }}
                  </span>
                </td>

                <td class="px-6 py-4">
                  <div @click="editTask(index)">
                    <a href="#">
                      <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-6 h-6 text-blue-400"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"
                        />
                      </svg>
                    </a>
                  </div>
                </td>
                <td class="px-6 py-4">
                  <div @click="deleteTask(index)">
                    <a href="#">
                      <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-6 h-6 text-red-400"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
                        />
                      </svg>
                    </a>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      task: "",
      editedTask: null,
      tasks: [],
    };
  },
  methods: {
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    submitTask() {
      if (this.task.length === 0) return;

      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      } else {
        this.tasks.push({
          name: this.task,
        });
      }
      this.task = "";
    },
  },
};
</script>