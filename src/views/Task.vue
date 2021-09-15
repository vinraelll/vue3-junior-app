<template>
  <section class="task-details">
    <div v-if="task">
      <h1>{{task.title}}</h1>
    
      <div class="chips" ref="chips"></div>
    
      <div class="input-field">
        <textarea 
          id="description" 
          v-model="description" 
          class="materialize-textarea" 
          ref="desc" 
          style="min-height: 150px;"
        >
        </textarea>
        <label for="description">Description of your task</label>
        <span class="character-counter" style="float: right; font-size: 12px;">{{ description.length }}/2048</span>
      </div>
    
      <input type="text" class="datepicker" ref="datepicker">
    
      <div v-if="task.status !== 'completed'">
        <button 
          @click="updateTask"
          class="btn waves-effect waves-light"
          style="margin-right: 10px;" 
          type="submit" 
          name="action"
        >
          Update task
          <i class="material-icons right">send</i>
        </button>
        <button
          class="btn red waves-effect waves-light"
          type="button"
          @click="completeTask"
        >
          Complete task
        </button>
      </div>
    </div>
    
    <div v-else>
      <h1>Task not found</h1>
    </div>
  </section>
</template>

<script>
export default {
  computed: {
    task() {
      return this.$store.getters.taskById(Number(this.$route.params.id))
    }
  },
  data: () => ({
    description: '',
    tags: null,
    date: null,
  }),
  mounted() {
    this.description = this.task.description

    this.tags = M.Chips.init(this.$refs.chips, {
      placeholder: "Tags",
      data: this.task.tags,
    })

    this.date = M.Datepicker.init(this.$refs.datepicker, {
      setDefaultDate: true,
      defaultDate: new Date(this.task.date),
      format: 'dd.mm.yyyy',
    })

    setTimeout(() => {
      M.updateTextFields()
    }, 0)
  },
  methods: {
    updateTask() {
      this.$store.dispatch('updateTask', {
        id: this.task.id,
        description: this.description,
        date: this.date.date
      })
      this.$router.push('/list')
    },
    completeTask() {
      this.$store.dispatch('completeTask', this.task.id)
      this.$router.push('/list')
    }
  },
  destroyed() {
    if (this.date && this.date.destroy) {
      this.date.destroy()
    }
    
    if (this.tags && this.tags.destroy) {
      this.tags.destroy()
    }
  }
}
</script>

<style scoped>
.task-details {
  max-width: 600px;
  margin: 0 auto;
}
</style>