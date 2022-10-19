<script>
  import { fade } from 'svelte/transition'

  const typingPractice = {
    name: 'Typing Practice',
    description: 'Practice typing',
    url: '/exercise/typing',
    progress: localStorage.getItem('typingPracticeProgress') || 0,
  }

  const drawingPractice = {
    name: 'Drawing Practice',
    description: 'Practice drawing',
    url: '/exercise/drawing',
    progress: localStorage.getItem('dawingPracticeProgress') || 0,
  }

  const signingPractice = {
    name: 'Signing Practice',
    description: 'Practice signing',
    url: '/exercise/signing',
    progress: localStorage.getItem('dawingPracticeProgress') || 0,
  }

  const exercises = [typingPractice, drawingPractice, signingPractice]
</script>

<svelte:head>
  <title>Exercise</title>
</svelte:head>

<div transition:fade={{ delay: 300, duration: 300 }}>
  <h1>Exercises</h1>
  <ul>
    {#each exercises as exercise}
      <li>
        <a href={exercise.url}>
          <h2>{exercise.name}</h2>
          <!-- Gif of exercise being preformed </p> -->
          <p>{exercise.description}</p>
          <p>{exercise.progress}</p>
        </a>
      </li>
    {/each}
  </ul>
</div>

<style>
</style>
