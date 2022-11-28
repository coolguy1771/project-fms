<script>
  import Done from '$lib/sounds/correct.mp3'
  import Timer from '$lib/components/timer.svelte'
  import { toast, SvelteToast } from '@zerodevx/svelte-toast'

  let doneSound = new Audio(Done)
  function done() {
    doneSound.play()
    progress = parseInt(progress) + 10
    if (progress >= 100) {
      toast.push('You have completed the exercise!')
      progress = 100
    }
    if (progress < 100) {
      toast.push({ msg: 'Good job! Keep going!', duration: 2000 })
    }
    if (timer <= 5) {
      timer = timer + 5
    }
    toast.push({ msg: 'Increasing Difficulty', duration: 2000 })
    localStorage.setItem('signingProgress', progress)
    localStorage.setItem('signingTimer', localStorage.getItem('signingTimer') - 5)
    //Wait for 1 second before reloading
    setTimeout(function () {
      location.reload()
    }, 1500)
  }
  function notDone() {
    toast.push({
      msg: 'You did not complete the exercise in time, please try again',
      duration: 2000,
    })
    setTimeout(function () {
      location.reload()
    }, 1000)
  }
  let progress = localStorage.getItem('signingProgress') || 0
  let timer = localStorage.getItem('signingTimer') || 60
</script>

<div>
  <h3>Please sign your name</h3>
</div>

<SvelteToast />

<div class="timer">
  <!-- Timer -->
  <Timer countdown={timer} on:completed={notDone} />
</div>
<div class="content">
  <iframe
    height="460"
    width="625"
    title="Signing Practice"
    src="https://editor.p5js.org/apradh25/full/527IUzG5p"
  />
</div>

<button on:click={done}>I'm Done</button>

<style>
  .content {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .timer {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 1rem;
  }
  button {
    position: absolute;
    bottom: 0;
    right: 0;
    margin: 1rem;
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 0.5rem;
    background-color: green;
    color: white;
    font-size: 1.5rem;
    font-weight: bold;
    cursor: pointer;
  }
</style>
