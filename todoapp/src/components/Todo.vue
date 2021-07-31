<template>
  <!-- <h2>hello</h2> -->
  <div class="container">
    <h2 class="text-center mt-5">My Vue To-Do App</h2>

    <!-- input -->
    <div class="d-flex">
      <input
        type="text"
        name=""
        id=""
        class="form-control"
        placeholder="Enter task"
        v-model="task"
      />
      <button class="btn btn-warning" @click="addTask">Add</button>
    </div>

    <!-- table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td><span class="pointer"></span>{{ task.name }}</td>
          <td style="width: 150px" @click="changeStatus(index)">
            {{ firstCharUpper(task.status) }}
          </td>
          <td>
            <div class="text-center">
              <span class="fa fa-pen" @click="editTask(index)"></span>
            </div>
          </td>
          <td>
            <div class="text-center">
              <span class="fa fa-trash" @click="deleteTask(index)"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "Todo",

  methods: {
    addTask() {
      if (this.task.length === 0) return;

      if (this.editedTask === null) {
        this.tasks.push({
          name: this.task,
          status: "todo",
        });
      } else {
        this.tasks[this.editedTask].name = this.task;

        this.editedTask = null;
      }

      this.task = "";
    },

    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    editTask(index) {
      this.task = this.tasks[index].name;

      this.editedTask = index;
    },

    changeStatus(index) {
      let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);

      if (++newIndex > 2) newIndex = 0;

      this.tasks[index].status = this.availableStatuses[newIndex];
    },

    firstCharUpper(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },
  },

  data() {
    return {
      task: "",
      editedTask: null,
      availableStatuses: ["to-do", "in-progress", "finished"],
      tasks: [
        {
          name: "Steal bananas from the store",
          status: "to-do",
        },
      ],
    };
  },
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
</style>