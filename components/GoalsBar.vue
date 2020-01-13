<template>
  <div>
    <NewGoal @addGoal="addGoal" :goals="goals" />
    <article>
      <h2>Your goals:</h2>
      <p class="subhead">
        These are your goals from the past year. Use the form above to add
        {{ goals.length > 0 ? 'more' : 'some' }}.
      </p>
      <table id="goals-list">
        <thead>
          <tr>
            <th>Goal:</th>
            <th>Successful:</th>
            <th>Enjoyability<br />(1–10):</th>
            <th>Flexibility<br />(1–10):</th>
          </tr>
        </thead>
        <tbody is="transition-group" name="fadeInUp">
          <template v-for="goal in goals">
            <tr :key="goal.name">
              <td>
                <b>{{ goal.name }}</b>
              </td>
              <td>{{ goal.completed == 'true' ? '✅' : '❌' }}</td>
              <td>{{ goal.enjoyability }}</td>
              <td>
                {{ goal.flexibility }}
                <button
                  @click="deleteGoal"
                  :data-goal="goal.name"
                  class="delete-button"
                >
                  Remove
                </button>
              </td>
            </tr>
          </template>
        </tbody>
      </table>
    </article>
  </div>
</template>

<script>
import NewGoal from './NewGoal'

export default {
  name: 'GoalsBar',
  components: { NewGoal },
  props: {
    goals: {
      type: Array,
      required: true
    }
  },
  methods: {
    addGoal(goal) {
      this.$emit('addGoal', goal)
    },
    deleteGoal(e) {
      this.$emit('deleteGoal', e.target.dataset.goal)
    }
  }
}
</script>

<style lang="scss">
.subhead {
  font-style: italic;
}

table {
  width: 100%;
  text-align: left;
  border-collapse: collapse;

  tr {
    transition: alls 0.15s ease-in-out;
  }

  td {
    font-family: 'Permanent Marker';
    position: relative;
  }

  th {
    border-color: inherit;
  }

  td,
  th {
    padding: 0.5em 0;
    border-bottom: 1px solid #ccc;

    & + th,
    & + td {
      text-align: center;
    }
  }
}

.delete-button {
  position: absolute;
  right: 0;
  opacity: 0;
  transform: translateY(1em);
  pointer-events: none;
  transition: all 0.15s ease-in-out;
  top: 0.35rem;
  margin-top: 0;
  border-radius: 5px;
  display: block;
}

tr:hover {
  background: #f8f8f8;
}

tr:hover .delete-button {
  opacity: 1;
  transform: translateY(0);
  pointer-events: initial;
}
</style>
