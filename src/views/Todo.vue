<template>
  <div class="home py-6">

    <v-text-field
      v-model="newTaskTitle"
      class="py-2 px-4"
      outlined
      label="Add new task..."
      append-icon="mdi-plus"
      hide-details
      clearable
      @click:append="addTask"
      @keyup.enter="addTask"
    ></v-text-field>

    <v-list
      class="pt-0"
      flat
    >
      <div
        v-for="task in tasks"
        :key="task.id"
      >
        <v-list-item
          @click="doneTask(task.id)"
          :class="{ 'blue lighten-5' : task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="primary"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through' : task.done }"
              >
                {{ task.title }}
              </v-list-item-title> 
            </v-list-item-content>

            <v-list-item-action>
              <v-btn 
                icon
                @click.stop="deleteTask(task.id)"
              >
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
        newTaskTitle: '',
        tasks: [
        /*   {
            id: 1,
            title: 'Wake up',
            done: false,
          },
          {
            id: 2,
            title: 'Make breakfast',
            done: false,
          },

          {
            id: 3,
            title: 'Login into email',
            done: false,
          },  */       
        ]
      }
    },
    methods: {
      addTask() {
        //console.log('addTask')
        let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          done: false
        }
        this.tasks.push(newTask)
        this.newTaskTitle = ''
      },
      doneTask(id) {
        //console.log('id: ', id)
        let task = this.tasks.filter(task => task.id === id)[0]
        task.done = !task.done
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id !== id)
      }
    }
  }
</script>
