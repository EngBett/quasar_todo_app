<template>
  <q-page padding>
    <div class="row">
      <q-input v-model="newTask" placeholder="Add new task" class="col" @keyup.enter="addTask" style="height: 18px"/>
      <q-btn color="primary" size="md" class="q-ml-lg" label="Add" @click.native="addTask"/>
    </div>

    <div class="q-mt-lg" v-if="tasks.length>0">
      <q-list bordered>
        <q-item-label header style="text-align: center;color:dodgerblue">Tasks</q-item-label>

        <q-item v-for="(task,index) in tasks" class="q-mb-sm" clickable v-ripple>

          <q-item-section>
            <q-item-label caption lines="1">{{ task }}</q-item-label>
          </q-item-section>

          <q-item-section side>
            <q-icon name="check" color="green"@click.native="moveTask(index)"/>
          </q-item-section>
        </q-item>
      </q-list>
    </div>

    <div class="q-mt-lg" v-if="tasksDone.length>0" style="background-color: #e6e6e6">
      <q-list bordered>
        <q-item-label header style="text-align: center;color: green;">Tasks Done</q-item-label>

        <q-item v-for="(task,index) in tasksDone" class="q-mb-sm" clickable v-ripple>

          <q-item-section>
            <q-item-label caption lines="1">{{ task }}</q-item-label>
          </q-item-section>

          <q-item-section side>
            <q-icon name="close" color="red" @click.native="deleteTask(index)" />
          </q-item-section>
        </q-item>
      </q-list>
    </div>

  </q-page>
</template>

<style>
</style>

<script>
export default {
  name: 'PageIndex',
  data(){
    return{
      tasks:[],
      newTask:'',
      tasksDone:[],
    }
  },
  methods:{
    addTask(){
      if(this.newTask!==""){
        this.tasks.push(this.newTask);
        this.newTask='';
      }else {
        this.$q.dialog({
          title: 'Alert',
          message: 'Please type in a task'
        }).onOk(() => {
          //
        }).onCancel(() => {
          //
        }).onDismiss(() => {
          //
        })
      }
    },
    moveTask(index){
      this.tasksDone.push(this.tasks[index]);
      this.tasks.splice(index,1);
    }
    ,
    deleteTask(index){
      this.$q.dialog({
        title: 'Confirm',
        message: 'Do you really wish to delete?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasksDone.splice(index,1);
      }).onOk(() => {
        //
      }).onCancel(() => {
        //
      }).onDismiss(() => {
        //
      });
    }
  }
}
</script>
