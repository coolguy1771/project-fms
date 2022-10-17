<script>
  import { fade } from 'svelte/transition'
</script>

<div transition:fade={{ delay: 300, duration: 300 }}>
  <h1>About Us</h1>

  <h2>What is Project FMS?</h2>

  <p>
    Project FMS is a project that aims to help people with motor disabilities.
  </p>

  <h2>Who are we?</h2>

  <p>We are a group of students from Arizona State University.</p>

  <h2>How can I help?</h2>

  <p>
    You can help by contribting to our project on <a
      a
      href="https://github.com/coolguy1771/project-fms">GitHub</a
    >.
  </p>
</div>

<style>
</style>
