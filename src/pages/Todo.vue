<template>
  <q-page class="bg-grey-3 column">
   <div class="row q-pa-sm bg-primary">
     <q-input
        v-model="newTask"
        @keyup.enter="addTask"
        class="col"
        square 
        filled
        bg-color="white"   
        placeholder="Add Todo"  
        dense>
        <template v-slot:append>
          <q-btn 
            @click="addTask"
            round  
            dense 
            flat 
            icon="add" />
        </template>
      </q-input>
   </div>
    <q-list 
      class="bg-white"
      separator
      bordered>
      <q-item 
        v-for="(task, index) in task"
        :key="task.title"
        @click="task.done = !task.done"
        :class="{ 'done bg-blue-1': task.done }"
        clickable
        v-ripple>

        <q-item-section avatar>
          <q-checkbox
           v-model="task.done"
           class="no-pointer-event"  
           color="primary" />
        </q-item-section>

        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
         <q-item-section
            v-if="task.done"
            side>
            <q-btn
              @click.stop="deleteTask(index)" 
              flat 
              round
              dense 
              color="primary" 
              icon="delete" />
        </q-item-section>
      </q-item>
    </q-list>
    <div 
      v-if="!task.length"
      class="no-task absolute-center">
      <q-icon
        name="check"
        size="100px"
        color="primary" />
      <div class="text-h6 text-primary text-center">
        No Task
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  data (){
    return {
      newTask: '',
      task: []
    }
  },
  methods: {
    deleteTask (index) {
       this.$q.dialog({
        title: 'Confirm',
        message: 'REALLY DELETE?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.task.splice(index, 1)
        this.$q.notify('Task Deleted')
      })
    },
    addTask() {
      this.task.push({
        title: this.newTask,
        done: false
      })
      this.newTask = ''
    }
  }
}
  
</script>

<style lang="scss">
  .done { 
    .q-item__label {
      text-decoration: line-through;
      color: #bbb;
    }
  }
  .no-task {
    opacity: 0.5;
  }
</style>
