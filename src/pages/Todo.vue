<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input 
        @keyup.enter="addTask"
        filled
        class="col"
        square
        bg-color="white" 
        v-model="newTask" 
        placeholder="Add task" 
        dense>

        <template v-slot:append>
          <q-btn
            @click="addTask"
            round
            dense
            flat
            icon="add"
            :disable="!newTask"
            />
        </template>
      </q-input>
    </div>
    <q-list separator bordered>
      <q-item
        @click="task.done = !task.done"
        clickable
        :class="{ 'done bg-green-2': task.done }"
        v-for="(task, index) in tasks" :key="task.title"
        v-ripple
        >
        <q-item-section avatar>
          <q-checkbox
          class="no-pointer-events"
          v-model="task.done"
          val="teal"
          color="teal"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section
        v-if="task.done"
        side
        >
        <q-btn 
        @click.stop="deleteTask(index)"
        class="glossy"
        dense
        round
        color="primary"
        icon="delete" />
        </q-item-section>
      </q-item>
    </q-list>
    <div
    v-if="!tasks.length" class="no-task absolute-center">
      <q-icon name="check" size="175px" color="primary"></q-icon>
      <div class="text-h4 text-primary text-center">No Tasks</div>
    </div>
  </q-page>
</template>

<script>
    export default {
      data() {
        return {
          newTask: '',
          tasks: [
            {
              title: "homework",
              done: false,
            },
            {
              title: "learn English",
              done: false,
            }
          ]
        }
      },
      methods: {
        deleteTask(index) {
          this.$q.
          dialog({
            title: 'Confirm',
            message: 'Do you want to delete it?',
            cancel: true,
            persistent: true
        })
        .onOk(() => {
          this.tasks.splice(index, 1);
          this.$q.notify('Deleted')
      })
        },
        addTask() {
          this.tasks.push({
            title: this.newTask,
            done: false,
          })
          this.newTask = ''
        } 
      }
    }
</script>

<style lang="scss">
  .done {
    .q-item__label{
      text-decoration: line-through;
      color: rgb(12, 57, 81);
    }
  }

  .no-task {
      opacity: 0.3;
    }
</style>
