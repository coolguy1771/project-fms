<script>
  import { fade } from 'svelte/transition'

  const typingPractice = {
    name: 'Typing Practice',
    description: 'Practice typing',
    url: window.location.pathname + '/exercise/typing',
    progress: localStorage.getItem('typingPracticeProgress') || 0,
  }

  const drawingPractice = {
    name: 'Drawing Practice',
    description: 'Practice drawing',
    url: window.location.pathname + '/exercise/drawing',
    progress: localStorage.getItem('drawingPracticeProgress') || 0,
  }

  const signingPractice = {
    name: 'Signing Practice',
    description: 'Practice signing',
    url: window.location.pathname + '/exercise/signing',
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
      <div class="exercise">
        <li>
          <h2>{exercise.name}</h2>
          <p>{exercise.description}</p>
          <p>{exercise.progress} %</p>
          <a href={exercise.url}>Start</a>
        </li>
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
    margin-bottom: 30px;
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
