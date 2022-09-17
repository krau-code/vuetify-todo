<template>
  <div>
    <!-- text field -->
    <v-text-field
      class="pa-3"
      v-model="newTaskTitle"
      @click:append="addTask"
      @keyup.enter="addTask"
      outlined
      label="Add To-Do"
      append-icon="mdi-plus"
      hide-details
      clearable
    ></v-text-field>

    <!-- List -->
    <div v-if="tasks.length > 0">
      <v-list flat class="pt-0">

        <div v-for="task in tasks" :key="task.id">

          <v-list-item @click="doneTask(task.id)" :class="{ 'blue lighten-5': task.done,}">

            <template v-slot:default>
              <v-list-item-action>
                <v-checkbox :input-value="task.done"></v-checkbox>
              </v-list-item-action>

              <v-list-item-content>
                <v-list-item-title :class="{ 'text-decoration-line-through': task.done }">{{ task.title }}</v-list-item-title>
              </v-list-item-content>

              <v-list-item-action>
                <v-btn icon @click.stop="deleteTask(task.id)">
                  <v-icon color="blue lighten-1">mdi-delete</v-icon>
                </v-btn>
              </v-list-item-action>
            </template>
            
          </v-list-item>
          <v-divider></v-divider>
        </div>
      </v-list>
    </div>

    <div v-else>
      <div class="d-flex flex-column justify-center align-center pa-6">
        <v-icon class="text-h1" color="blue lighten-4">mdi-check</v-icon>
        <p class="text-h5 blue--text text--lighten-4">No Tasks</p>
      </div>
    </div>
    
  </div>
</template>

<script>
  export default {
    name: 'Todo',
    data() {
      return {
        newTaskTitle: '',
        tasks: [
          // {
          //   id: 1,
          //   title: 'Wake up',
          //   done: false
          // },
          // {
          //   id: 2,
          //   title: 'Get bananas',
          //   done: false
          // },
          // {
          //   id: 3,
          //   title: 'Eat bananas',
          //   done: false
          // }
        ]
      }
    },
    methods: {
      addTask() {
        if (this.newTaskTitle) {
          let newTask = {
            id: Date.now(),
            title: this.newTaskTitle,
            done: false
          }

          this.tasks.push(newTask);
          this.newTaskTitle = '';
        } else {
          alert('Add a task first');
        }
        
      },
      doneTask(id) {
        let task = this.tasks.filter(task => task.id === id)[0];
        task.done = !task.done;
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id != id);
      }
    }
  }
</script>
