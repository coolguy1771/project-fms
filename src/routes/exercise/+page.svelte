<script>
  import { base } from '$app/paths'
  import { Progress } from '@svelteuidev/core'

  const typingPractice = {
    name: 'Typing Practice',
    description: 'Practice typing',
    url: base + '/exercise/typing',
    progress: localStorage.getItem('typingPracticeProgress') || 0,
  }

  const drawingPractice = {
    name: 'Drawing Practice',
    description: 'Practice drawing',
    url: base + '/exercise/drawing',
    progress: localStorage.getItem('drawingPracticeProgress') || 0,
  }

  const signingPractice = {
    name: 'Signing Practice',
    description: 'Practice signing',
    url: base + '/exercise/signing',
    progress: localStorage.getItem('dawingPracticeProgress') || 0,
  }

  const exercises = [typingPractice, drawingPractice, signingPractice]
</script>

<svelte:head>
  <title>Exercise</title>
</svelte:head>

<div>
  <ul>
    <h1>Exercises</h1>
    {#each exercises as exercise}
      <div class="exercise">
        <h2>{exercise.name}</h2>
        <p>{exercise.description}</p>
        <Progress
          color="orange"
          value={exercise.progress}
          label="{exercise.progress}%"
          size="xl"
          radius="xs"
          striped
          animate
        />
        <a href={exercise.url}>Start</a>
      </div>
    {/each}
  </ul>
</div>

<style>
  h2 {
    margin: 0;
    font-weight: bold;
  }
  .exercise {
    width: 100%;
    height: 100%;
    justify-content: left;
    align-items: center;
    display: block;
    margin-bottom: 20px;
  }
  a {
    background-color: #4caf50; /* Green */
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    width: 100%;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
  }
</style>
