<template>
  <div id="graph-wrapper">
    <h2>Goals chart:</h2>
    <p class="subhead">
      Your goals are automatically charted here. (Hover to see goal names.)
    </p>
    <ul id="graph">
      <li
        v-for="goal in goals"
        :key="goal.name"
        :style="{
          'grid-column': `${goal.flexibility} / ${Number(goal.flexibility) +
            1}`,
          'grid-row': `${goal.enjoyability} / ${Number(goal.enjoyability) + 1}`
        }"
      >
        {{ goal.completed == 'true' ? '✅' : '❌' }}
        <span
          :style="{ left: labelPlacement(goal.flexibility) }"
          class="label"
          >{{ goal.name }}</span
        >
      </li>
      <div class="background-holder">
        <div class="quadrant" aria-hidden="true">
          Achievement
        </div>
        <div class="quadrant" aria-hidden="true">
          Creativity
        </div>
        <div class="quadrant" aria-hidden="true">
          Results
        </div>
        <div class="quadrant" aria-hidden="true">
          Learning
        </div>
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  name: '',
  components: {},
  props: {
    goals: {
      type: Array,
      required: true
    }
  },
  methods: {
    labelPlacement(val) {
      val = Number(val)
      if (val === 1) {
        return '0'
      } else if (val === 10) {
        return '-200%'
      } else {
        return '-100%'
      }
    }
  }
}
</script>

<style lang="scss" scoped>
#graph-wrapper {
  margin: 6rem 0 8rem;
}

#graph {
  display: grid;
  grid-template-columns: repeat(10, 1fr);
  grid-template-rows: repeat(10, 1fr);
  width: 100%;
  min-height: 720px;
  border-top: 1px solid #ccc;
  border-left: 1px solid #ccc;
  border-collapse: collapse;
  position: relative;
  list-style-type: none;
  padding: 0;

  li {
    font-size: 2rem;
    overflow: visible;
    z-index: 2;
    display: flex;
    width: 100%;
    height: 100%;
    justify-content: center;
    align-items: center;
    position: absolute;
    text-align: center;

    &:hover .label {
      opacity: 1;
    }

    .label {
      font-family: 'Permanent Marker';
      opacity: 0;
      font-size: 1rem;
      width: 300%;
      transition: opacity 0.2s;
      background: rgba(255, 255, 255, 0.95);
      padding: 0.5rem;
      bottom: 0;
      position: absolute;
      text-align: center;
      border: 1px solid #ccc;
      border-radius: 5px;
      display: block;
      line-height: 1.2;
      box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.2);
    }
  }
}

.background-holder {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;

  .quadrant {
    display: grid;
    place-content: center;
    color: #eee;
    font-family: 'Permanent Marker';
    font-size: calc(1.4rem);
    z-index: 0;
    border-right: 1px solid #ccc;
    border-bottom: 1px solid #ccc;
  }
}
</style>
