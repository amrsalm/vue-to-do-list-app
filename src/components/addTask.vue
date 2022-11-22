
<template>
   
    <div class="text-center">
      <v-dialog
        v-model="dialog"
      >
        <template v-slot:activator="{ props }">
          <v-btn
            color="white lighten-5"
            v-bind="props"
            @click="this.$root.add1()"
          >
          <v-icon color="white lighten-1">mdi-plus</v-icon> Add
          </v-btn>
        </template>
  
<v-card v-if="this.$root.add" pa-4 text-center>
            <v-toolbar
  elevation="4"
  color="blue"
  shaped
 
>    <v-icon color="white lighten-1">mdi-plus</v-icon> <text>Add a Task</text></v-toolbar>
<v-form ref="form"  v-model="valid"
      lazy-validation >
        <text>Task title:</text>
            <v-text-field
            v-model="newTaskTitle"
            label=""
            :rules="[empty,check]"
            required
            filled
            clearable	

          ></v-text-field>
          <text>Task Description:</text>
          <v-text-field
            v-model="Description"
            :rules="desRules"
            required
            label=""
            filled
            clearable	

          ></v-text-field>
          <text>Task Deadline:</text>
          <Datepicker v-model="date" :format="format"  modelType="MM.dd.yyyy"></Datepicker>
          <text>Task Priority:</text>
        <v-radio-group v-model="Priority">
             <v-radio label="High" value="High" ></v-radio>
             <v-radio label="Medium" value="Medium" ></v-radio>
             <v-radio label="low" value="low" ></v-radio>
        </v-radio-group>
    </v-form>
        <v-card-actions>
           <v-btn color="blue" block @click="validate" > <v-icon color="blue lighten-1">mdi-plus</v-icon> Add</v-btn>
        </v-card-actions>
        <v-card-actions>
           <v-btn color="red" block @click=" cancel()"> <v-icon color="red lighten-1">mdi-close</v-icon> Cancel</v-btn>
        </v-card-actions>
        </v-card>



      </v-dialog>
    </div>
  </template>
  
  <script>
    import Datepicker from '@vuepic/vue-datepicker';
    import '@vuepic/vue-datepicker/dist/main.css'       
    export default {
         
        components:{Datepicker },
        
        data () {
        

        return {
            valid: true,
            
    desRules: [
      v => !!v || 'Description is required',

    ],
            date: null,
            format:'MM/dd/yyyy',
            newTaskTitle:'',
            Priority:null,
            Description:null,
            
          dialog: false,
        }
      },
       
      methods:{
        async validate () {
            let newTask={
            id:Date.now(),
            update:true,
            title: this.newTaskTitle,
            Priority:this.Priority,
            Description:this.Description,
            done:false,
            Deadline:this.date
        }
      const { valid } = await this.$refs.form.validate()

      if (valid) {
        this.$root.tasks.push(newTask),
        this.dialog = false,
        this.newTaskTitle='',
        this.Priority=null,
        this.Description='',
        this.$root.snackbar = true
        
      }
    },
    empty(name){
    if (name==='')
      return 'Title is required'
    else
    return true
    },
    check(name){
        let i = 0;

        while (i < this.$root.tasks.length) {
    if(this.$root.tasks[i].title === name)
    return 'The Title already exist, please make sure the title is unique'
    i++;
    }
    return true;
       
       
        
    },
    
    cancel(){
    this.dialog = false
    }
  },
  
    }
  </script>