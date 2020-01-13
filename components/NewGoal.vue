<template>
  <article>
    <h2>Add a goal to the list:</h2>
    <form action="">
      <input
        id="goal-name"
        v-model="name"
        type="text"
        placeholder="What was the goal?"
      />

      <label for="goal-enjoyability">How enjoyable was this goal? </label>
      <select id="goal-enjoyability" v-model="enjoyability" name="enjoyability">
        <option value="0" disabled>Rate 1–10…</option>
        <option value="1">1 - I hated nothing more</option>
        <option value="2">2 - Awful</option>
        <option value="3">3 - Not enjoyable</option>
        <option value="4">4 - I didn't like it</option>
        <option value="5">5 - It was ok</option>
        <option value="6">6 - I didn't mind it</option>
        <option value="7">7 - Enjoyable</option>
        <option value="8">8 - I liked it</option>
        <option value="9">9 - I loved it</option>
        <option value="10">10 - I loved nothing more</option>
      </select>

      <label for="goal-flexibility">
        <span>How flexible was this goal? </span>
      </label>
      <select id="goal-flexibility" v-model="flexibility" name="flexibility">
        <option value="0" disabled>Rate 1–10…</option>
        <option value="1">1 - Absolutely mandatory; top priority</option>
        <option value="2">2 - Extremely important</option>
        <option value="3">3 - Very inflexible</option>
        <option value="4">4 - Pretty important</option>
        <option value="5">5 - Moderately important</option>
        <option value="6">6 - A little flexible</option>
        <option value="7">7 - Moderately flexible</option>
        <option value="8">8 - Very flexible</option>
        <option value="9">9 - Extremely flexible</option>
        <option value="10">10 - ¯\_(ツ)_/¯</option>
      </select>

      <fieldset>
        <legend>Was this goal a success?</legend>
        <div class="radio-group">
          <input
            id="yes-success"
            v-model="completed"
            type="radio"
            name="succeeded"
            value="true"
          />
          <label for="yes-success">Yes</label>
          <br />
          <input
            id="no-success"
            v-model="completed"
            type="radio"
            name="succeeded"
            value="false"
          />
          <label for="no-success">No</label>
        </div>
      </fieldset>

      <button @click.prevent="addGoal" :disabled="!readyToAdd" role="button">
        Add this goal to my list
      </button>
    </form>
  </article>
</template>

<script>
export default {
  name: 'NewGoal',
  props: {
    goals: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      name: '',
      flexibility: 0,
      enjoyability: 0,
      completed: null
    }
  },
  computed: {
    readyToAdd() {
      return (
        this.name && this.enjoyability && this.flexibility && this.completed
      )
    }
  },
  watch: {
    goals(prev, next) {
      prev !== next && prev.length > next.length && this.resetForm()
    }
  },
  methods: {
    addGoal() {
      this.$emit('addGoal', {
        name: this.name,
        flexibility: this.flexibility,
        enjoyability: this.enjoyability,
        completed: this.completed
      })
    },
    resetForm() {
      this.name = ''
      this.flexibility = 0
      this.enjoyability = 0
      this.completed = null
    }
  }
}
</script>

<style lang="scss" scoped>
form {
  width: 100%;
  max-width: 18rem;
}

label,
fieldset,
select,
input[type='text'] {
  font-weight: normal;
  display: block;
  margin-top: 2rem;
  font-family: inherit;
  font-size: inherit;
  width: 100%;
}

.radio-group {
  label {
    display: inline;
    font-weight: normal;
  }
}

label {
  font-size: 1.1rem;
  font-weight: bold;
}

fieldset {
  padding: 0;
  border: 0;

  legend {
    margin-bottom: 0.5em;
    font-weight: bold;
  }
}

input[type='text'] {
  border: 0;
  border-bottom: 1px solid;
  padding: 0.5em 0.25em;
  margin-top: 1rem;
  min-width: 16rem;
}

.subtext {
  font-weight: normal;
  font-size: 0.8em;
  line-height: 1;
}

.form-pair {
  flex-wrap: wrap;
  margin: 0 0 2rem;

  & > * {
    flex: 1 0 100%;
  }
}

select {
  font-size: inherit;
  padding: inherit;
  margin-top: 0.5rem;
}
</style>
