<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input class="col" square filled bg-color="white" v-model="newTask" label="Add Task" dense>
      <template>
        <q-btn round :dense="dense" fl at icon="add"/>
      </template>
      </q-input>
    </div>
    <q-list class="bg-white" separator bordered>
      <q-item
        v-for="(task, index) in tasks"
        :key="task.title"
        @click="task.done = !task.done"
        :class="{ done: task.done }"
        clickable
        v-ripple
      >
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            class="no-pointer-events"
            color="primary"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn
            @click.stop="deleteTask(index)"
            flat
            round
            dense
            color="primary"
            icon="delete"
          ></q-btn>
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>

export default {
  data () {
    return {
      tasks: [
        {
          title: 'Get a life',
          done: false
        },
        {
          title: 'Live that life',
          done: false
        },
        {
          title: 'Die',
          done: false
        }
      ]
    }
  },
  methods: {
    deleteTask(index) {
      console.log(index)
      this.$q.dialog({
          title: 'Confirm',
          message: 'Really delete?',
          cancel: true,
          persistent: true
        })
        .onOk(() => {
          this.tasks.splice(index, 1)
          this.$q.notify('Task deleted')
        })
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
</style>
