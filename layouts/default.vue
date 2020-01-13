<template>
  <div>
    <nuxt />
    <footer>
      <p>
        &copy; 2020
        <a href="https://joshcollinsworth.com" target="_blank"
          >Josh Collinsworth</a
        >. <br />Built with
        <a href="https://nuxtjs.org/" target="_blank">NuxtJS</a>; based on
        <a
          href="https://medium.com/@karenborchert/want-to-actually-achieve-those-2020-goals-know-your-type-897070f92be9"
          target="_blank"
          >this Medium post</a
        >
        by Karen Borchert.
      </p>
    </footer>
  </div>
</template>

<style lang="scss">
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 18px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  color: #101820;
}

body {
  margin: 0;
}

h1,
h2,
h3 {
  font-family: 'Permanent Marker';
  margin-bottom: 0;
  margin-top: 1em;
}

h2 {
  font-size: 2.5rem;
}

*,
*:before,
*:after {
  box-sizing: border-box;
}

article {
  margin-top: 4rem;
}

p {
  margin-top: 0;
}

button {
  padding: 0.5rem 1rem;
  font-size: 0.8rem;
  border-radius: 5px;
  font-weight: bold;
  line-height: 0.8rem;
  margin-top: 2rem;
}

.fadeInUp {
  &-enter-active {
    transition: all 0.3s ease-in-out;
    width: 100%;
  }

  &-leave-active {
    position: absolute;
  }

  &-enter,
  &-leave-to {
    opacity: 0;
    transform: translateY(0.1em);
  }

  &-move {
    transition: transform 0.3s;
  }
}

footer {
  padding: 1rem;
  text-align: center;
  font-size: 0.9rem;
}
</style>
