<script>
  import { fade } from 'svelte/transition'
  const typingPractice = {
    name: 'Typing Practice',
    description: 'Practice typing',
    url: '/exercise/typing',
  }

  const drawingPractice = {
    name: 'Drawing Practice',
    description: 'Practice drawing',
    url: '/exercise/drawing',
  }

  const signingPractice = {
    name: 'Signing Practice',
    description: 'Practice signing',
    url: '/exercise/signing',
  }

  const exercises = [typingPractice, drawingPractice, signingPractice]
</script>

<div transition:fade={{ delay: 300, duration: 300 }}>
  <h1>Exercises</h1>
  <ul>
    {#each exercises as exercise}
      <li>
        <a href={exercise.url}>
          <h2>{exercise.name}</h2>
          <p>{exercise.description}</p>
        </a>
      </li>
    {/each}
  </ul>
</div>

<style>
</style>
