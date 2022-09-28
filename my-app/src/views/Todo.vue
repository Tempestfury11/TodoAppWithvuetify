<template>
  <div class="home">

    <v-text-field
    v-model="newTaskTile"
    @click:append="addTask"
    @keyup.enter="addTask"
    class="pa-3" 
    outlined 
    label="Add Task" 
    append-icon="mdi-plus"
    hide-details
    clearable>

    </v-text-field>


    <v-list class="pt-0
    done: false" flat>
      <div v-for="task in tasks" :key="task.id">

        <v-list-item @click="doneTask(task.id)" :class="{ 'blue lighten-5' : task.done}">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary">
              </v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title :class="{ 'text-decoration-line-through' : task.done}">
                {{task.title}}
              </v-list-item-title>
            </v-list-item-content>

            <v-list-item-action>
              <v-btn @click.stop="deleteTask(task.id)" icon>
                <v-icon color="primary lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>

          </template>


        </v-list-item>
        <v-divider></v-divider>
      </div>

    </v-list>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      newTaskTitle:'',
      tasks: [
        {
          id: 1,
          title: 'Wake up',
          done: false
        },
        {
          id: 2,
          title: 'Make Breakfast',
          done: false
        },
        {
          id: 3,
          title: 'Eat Breakfast',
          done: false
        }
      ]
    }
  },
  methods: {
    addTask(){
      let newTask ={
        id:Date.new(),
        title: this.newTaskTitle,
        done: false
      }
      this.tasks.push(newTask)
      this.newTaskTitle = ''
    },
    doneTask(id) {
      let task = this.tasks.filter(task => task.id === id)[0]
      task.done = !task.done
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id)
    }
  }
}
</script>
