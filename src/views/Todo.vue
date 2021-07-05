<template>
  <div class="home">
    <v-text-field
      v-model='newTaskTitle'
      class="pa-3"
      outlined
      label="Add Task"
      append-icon="mdi-plus"
      hide-details
      clearable
      @click:append='addTask'
      @keyup.enter="addTask"
    >
    </v-text-field>
    <v-list
    class="pt-0"
      flat
    >
      <div v-for='task in tasks' :key='task.id' >
        <v-list-item @click='doneTask(task.id)' :class="{'blue lighten-5': task.done }">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="primary"
              ></v-checkbox>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title :class="{'text-decoration-line-through': task.done}">
                {{task.title}}
              </v-list-item-title>
            </v-list-item-content>
            <v-list-item-action @click="deleteTask(task.id)">
              <v-btn icon>
                <v-icon color="grey lighten-1">mdi-delete</v-icon>
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
    data(){
      return{
        newTaskTitle: '',
        tasks: [
        ]
      }
    },
    methods: {
      addTask(){
        this.tasks.push({id: Date.now(), title: this.newTaskTitle, done: false})
        this.newTaskTitle = ''
      },
      doneTask(id){
        let task = this.tasks.filter(t => t.id === id)[0]
        task.done = !task.done
      },
      deleteTask(id){
        this.tasks = this.tasks.filter(t => t.id !== id)
      }
    } 
  }
</script>
