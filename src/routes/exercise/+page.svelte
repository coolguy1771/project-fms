<script>
  import { base } from '$app/paths'
  import { Progress } from '@svelteuidev/core'

  const typingPractice = {
    name: 'Typing Practice',
    description:
      'In this exercise practice typing the displayed words as fast and as accurately as you can. To check the completed word click the check button.',
    url: base + '/exercise/typing',
    progress: localStorage.getItem('typingProgress') || 0,
  }

  const drawingPractice = {
    name: 'Drawing Practice',
    description:
      "In this exercise practice tracing the pictures displayed on the screen. To finish click the I'm done button.",
    url: base + '/exercise/drawing',
    progress: localStorage.getItem('drawingProgress') || 0,
  }

  const signingPractice = {
    name: 'Signing Practice',
    description:
      "In this exercise practice tracing the letters displayed on the screen. To finish click the I'm done button.",
    url: base + '/exercise/signing',
    progress: localStorage.getItem('signingProgress') || 0,
  }

  const exercises = [typingPractice, signingPractice, drawingPractice]
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
        {#if exercises.progress > 0}
          <Progress
            color="orange"
            value={exercise.progress}
            label="{exercise.progress}%"
            size="xl"
            radius="xs"
            striped
            animate
          />
          <a href={exercise.url}>Continue</a>
        {:else}
          <a href={exercise.url}>Start</a>
        {/if}
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
