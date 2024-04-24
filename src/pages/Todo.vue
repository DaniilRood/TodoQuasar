<template>
  <q-page class="bg-grey-3 column">
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
  </q-page>
</template>

<script>
    export default {
      data() {
        return {
          tasks: [
            {
              title: "rew",
              done: true,
            },
            {
              title: "rew",
              done: false,
            },
            {
              title: "rew",
              done: false,
            },
          ]
        }
      },
      methods: {
        deleteTask(index) {
          this.tasks.splice(index, 1);
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
</style>
