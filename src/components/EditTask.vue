<template>
   <div class="text-center">
      <v-dialog
        v-model="dialog"
      >
        <template v-slot:activator="{ props }">
          <v-btn
            color="white lighten-5"
            v-bind="props"
            icon
          >
          <v-icon color="blue lighten-1">mdi-pen</v-icon>
          </v-btn>
        </template>
  
  <v-card>
            <v-toolbar
  elevation="4"
  color="blue"
  shaped
>  <v-icon color="white lighten-1">mdi-pen</v-icon>  Update Task</v-toolbar>
Description:
            <v-text-field
            v-model="newTaskDescription"
            :label="id.Description"
            filled
            clearable	

          ></v-text-field>
          Date:
          <Datepicker v-model="date" :format="format"  modelType="dd.MM.yyyy"></Datepicker>
          Priority:
        <v-radio-group v-model="Priority">
             <v-radio label="High" value="High" ></v-radio>
             <v-radio label="Medium" value="Medium" ></v-radio>
             <v-radio label="low" value="low" ></v-radio>
        </v-radio-group>
          <v-card-actions>
            <v-btn color="blue" block @click="validate" > <v-icon color="blue lighten-1">mdi-pen</v-icon> Update</v-btn>
          </v-card-actions>
          <v-card-actions>
            <v-btn color="red" block @click=" cancel()"> <v-icon color="red lighten-1">mdi-close</v-icon> Cancel</v-btn>
        </v-card-actions>
        </v-card>
      </v-dialog>

    </div>
    <v-snackbar
        v-model="snackbar1"
      color="blue"
                  >
        {{ text1 }}
  
        <template v-slot:action="{ attrs }">
          <v-btn
            color="white"
            text
            v-bind="attrs"
            @click="snackbar1 = false"
          >
            Close
          </v-btn>
        </template>
      </v-snackbar>
  </template>
  <script>
 import Datepicker from '@vuepic/vue-datepicker';
    import '@vuepic/vue-datepicker/dist/main.css'
    
            
    export default {
         
        components:{Datepicker },
        name:'EditTask',
        props:[
            'id'
    ],
        data () {
        

        return {
            text1: 'Task updated Successfully ',
            snackbar1:false,
            newTaskTitle: '',
            newTaskDescription:'',
            date: null,
            format:'MM/dd/yyyy',
            dialog: false,
            Priority:null,  
            
        }
      },
      methods:{
        editTask(id){
        if(this.newTaskDescription!=='')
        id.Description=this.newTaskDescription

        if(this.date!==null)
        id.Deadline=this.date
        if(this.Priority!==null)
        id.Priority=this.Priority
        this.dialog = false,
        this.newTaskDescription='',
        console.log(id.update),
        this.snackbar1=true
        },
        cancel(){
    this.dialog = false
    }
  }
    }
  </script>