<script>
  import { onMount } from 'svelte'
  import { fade } from 'svelte/transition'
  import { Progress } from '@svelteuidev/core'

  onMount(() => {
    visible = true
  })

  const typingPractice = {
    name: 'Typing Practice',
    description: 'Practice typing',
    progress: localStorage.getItem('typingPracticeProgress') || 0,
  }

  const drawingPractice = {
    name: 'Drawing Practice',
    description: 'Practice drawing',
    progress: localStorage.getItem('drawingPracticeProgress') || 0,
  }

  const signingPractice = {
    name: 'Signing Practice',
    description: 'Practice signing',
    progress: localStorage.getItem('dawingPracticeProgress') || 0,
  }
  const exercises = [typingPractice, signingPractice, drawingPractice]
</script>

<div transition:fade={{ delay: 300, duration: 300 }}>
  <h1>Progress</h1>
  <p>Here you can view your progress across all of the exercises</p>

  {#each exercises as exercise}
    <div class="exercise">
      <li>
        <h2>{exercise.name}</h2>
        <p>{exercise.description}</p>
        <Progress
          color="orange"
          value={exercise.progress}
          label="{exercise.progress}%"
          size="xl"
          radius="xl"
          striped
          animate
        />
      </li>
    </div>
  {/each}
</div>

<style>
</style>
