<template>
<v-card>
    
    <v-container class="grey lighten-5"
    fixed ma-0 pa-0 fill-height
    >
    <v-row justify="center" no-gutters>
        <v-col col="4" order-xs="3" order-sm="1">
          <v-card  class="pa-4 text-center">
            Title
          </v-card>
        </v-col>
        <v-col col="4" order="2">
          <v-card class="pa-4 text-center">
            Description
          </v-card>
        </v-col>
        <v-col col="4" order-xs="1" order-sm="3">
          <v-card class="pa-4 text-center  " >
            Deadline
          </v-card>
        </v-col>
        <v-col col="4" order-xs="1" order-sm="4">
          <v-card class="pa-4 text-center">
            Priority
          </v-card>
        </v-col>
        <v-col col="4" order-xs="1" order-sm="5">
          <v-card class="pa-4 text-center">
            Is Complete
          </v-card>
        </v-col>
        <v-col col="4" order-xs="1" order-sm="6">
          <v-card class="pa-4 text-center">
           Actions
          </v-card>
        </v-col>
      </v-row>
      <v-divider></v-divider>
      <div v-for="task in tasks" :key="task.id" tasks_prop.sync="tasks">
        <v-list-item
        
        
        >      <v-row justify="center" no-gutters  class="pa-0  rounded-0">
        <v-col col="4" order-xs="3" order-sm="1"  class="pa-0  rounded-0">
          <v-card class="pa-0  rounded-0"
          flat solo
          >
            <v-list-item-title :class="{ ' text-decoration-line-through' : task.done}"> <text>{{ task.title }}</text></v-list-item-title>
          </v-card>
        </v-col>
        <v-col col="4" order="2">
          <v-card
          flat solo>
          <v-list-item-title :class="{ ' text-decoration-line-through' : task.done}"> <text>{{task.Description}}</text></v-list-item-title> 
          </v-card>
        </v-col>
        <v-col col="4" order-xs="1" order-sm="3">
          <v-card  class="pa-0  rounded-0"
          flat solo
          >
            <v-list-item-title :class="{ ' text-decoration-line-through' : task.done}"> <text>{{ task.Deadline }}</text></v-list-item-title>
          </v-card>
        </v-col>
        <v-col col="4" order-xs="1" order-sm="4">
          <v-card  class="pa-0  rounded-0"
          flat solo
          >
            {{task.Priority}}
          </v-card>
        </v-col>
        <v-col col="4" order-xs="1" order-sm="5">
          <v-card  class="pa-0  rounded-0"
          flat solo
          >
            <v-list-item-action start>
              <v-checkbox-btn color="green" :model-value="task.done" @click="doneTask(task.id)"></v-checkbox-btn>
            </v-list-item-action>
          </v-card>
        </v-col>
        <v-col col="4" order-xs="1" order-sm="6">
          <v-card  class="pa-0  rounded-0"
          flat solo
          >
          <v-row>
            <v-col col="1" order-xs="2" order-sm="1"> <v-list-item-action>
            <v-btn 
            @click.stop="deleteTask(task.id)"
            icon>
              <v-icon color="blue lighten-1">mdi-delete</v-icon>
            </v-btn>
          </v-list-item-action>
         
        </v-col>
          <v-col pa-0 v-col col="1" order-xs="2" order-sm="1"> <v-list-item-action>
            <EditTask :sandbox=task.update :id=task v-bind:tasks="tasks" v-if="!task.done"></EditTask>
          </v-list-item-action></v-col>
        </v-row>
          </v-card>
        
        </v-col>
        
      </v-row>
  
</v-list-item>
<v-divider></v-divider>
    </div>
    </v-container>

  </v-card>
 
      <v-snackbar
        v-model="snackbar2"
      color="red"
                  >
        Task deleted Successfully
  
        <template v-slot:action="{ attrs }">
          <v-btn
            color="white"
            text
            v-bind="attrs"
            @click="snackbar2= false"
          >
            Close
          </v-btn>
        </template>
      </v-snackbar>
</template>
<script>
import EditTask from './EditTask.vue';
export default {
    components:{EditTask},

name:"toDoList",
        props:['tasks'],
        data() {
            
    return {
        
        
        snackbar2:false,
        items: [
        {title: "title1", value: "value1", detail: "detail1"},
        {title: "title2", value: "value2", detail: "detail2"},
        {title: "title3", value: "value3", detail: "detail3"}
      ],
      id:15
    };
},


    methods:{

    doneTask(id) {
      let task = this.$root.tasks.filter(task => task.id===id )[0]
      task.done=!task.done
      
    },
    deleteTask(id){
        this.snackbar2 =true;
        this.$root.tasks = this.$root.tasks.filter(task => task.id!==id )
    }
  }

    }
        
</script>