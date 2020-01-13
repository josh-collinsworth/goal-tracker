<template>
  <div class="container">
    <h1 class="title">
      Goal Retrospective
    </h1>
    <p>
      <i>
        What is this and how is it used? Read
        <a
          href="https://medium.com/@karenborchert/want-to-actually-achieve-those-2020-goals-know-your-type-897070f92be9"
          target="_blank"
          >this Medium article</a
        >.</i
      >
    </p>
    <GoalsBar @addGoal="addGoal" @deleteGoal="deleteGoal" :goals="goals" />
    <Graph :goals="goals" />
  </div>
</template>

<script>
import Graph from '~/components/Graph.vue'
import GoalsBar from '~/components/GoalsBar.vue'

export default {
  components: {
    Graph,
    GoalsBar
  },
  data() {
    return {
      goals: [],
      defaultGoals: [
        {
          name: 'Run a marathon',
          flexibility: 1,
          enjoyability: 4,
          completed: true
        },
        {
          name: 'MRR',
          flexibility: 4,
          enjoyability: 8,
          completed: false
        },
        {
          name: 'Read 20 books',
          flexibility: 10,
          enjoyability: 7,
          completed: true
        }
      ]
    }
  },
  mounted() {
    const savedGoals = JSON.parse(localStorage.getItem('nuxtGoalRetroGoals'))
    this.goals = savedGoals || this.defaultGoals
  },
  methods: {
    addGoal(newGoal) {
      if (!this.goals.map((goal) => goal.name).includes(newGoal.name)) {
        localStorage.setItem(
          'nuxtGoalRetroGoals',
          JSON.stringify([...this.goals, newGoal])
        )
        this.goals = JSON.parse(localStorage.getItem('nuxtGoalRetroGoals'))
      } else {
        alert('Goal names must be unique')
      }
    },
    deleteGoal(deletedGoal) {
      this.goals = this.goals.filter((goal) => goal.name !== deletedGoal)
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  max-width: calc(720px + 2rem);
  padding: 0 2rem;
}

.title {
  font-size: 3.5rem;
}
</style>
