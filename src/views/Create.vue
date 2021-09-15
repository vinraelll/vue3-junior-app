<template>
  <section class="create">
    <h1>Create task</h1>
    
    <form @submit.prevent>
      <div class="input-field col s6">
        <input v-model="title" id="task-name" type="text" class="validate" />
        <label for="task-name">Task title</label>
        <span
          class="helper-text"
          data-error="Title is required"
          data-success="Valid title"
        ></span>
      </div>
    </form>

    <div class="chips" ref="chips"></div>

    <div class="input-field">
      <textarea v-model="description" id="description" class="materialize-textarea"></textarea>
      <label for="description">Description of your task</label>
      <span class="character-counter" style="float: right; font-size: 12px;">{{ description.length }}/2048</span>
    </div>

    <input type="text" class="datepicker" ref="datepicker">

    <button 
      @click="submitHandler"
      class="btn waves-effect waves-light" 
      type="submit" 
      name="action">
      Create task
      <i class="material-icons right">send</i>
    </button>
  </section>
</template>

<script>
export default {
  name: "Home",
  data: () => ({
    description: '',
    title: '',
    tags: null,
    date: null,
  }),
  mounted() {
    this.tags = M.Chips.init(this.$refs.chips, {
      placeholder: "Tags",
    })

    this.date = M.Datepicker.init(this.$refs.datepicker, {
      setDefaultDate: true,
      defaultDate: new Date(),
      format: 'dd.mm.yyyy',
    })
  },
  methods: {
    submitHandler() {
      if (!this.title) {
        return false
      }

      const task = {
        title: this.title,
        description: this.description,
        status: 'active',
        tags: this.tags.chipsData,
        date: this.date.date,
        id: Date.now()
      }

      this.$store.dispatch('createTask', task)
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
};
</script>

<style scoped>
.create {
  max-width: 600px;
  margin: 0 auto;
}

.input-field label {
  left: 0;
}
</style>
