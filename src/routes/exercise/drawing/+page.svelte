<script>
  import Done from '$lib/sounds/correct.mp3'
  import Timer from '$lib/components/timer.svelte'
  import { toast, SvelteToast } from '@zerodevx/svelte-toast'

  let doneSound = new Audio(Done)
  let timer = localStorage.getItem('drawingTimer') || 60
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
    if (time <= 5) {
      timer = timer + 5
    }
    toast.push({ msg: 'Increasing Difficulty', duration: 2000 })
    localStorage.setItem('signingProgress', progress)
    localStorage.setItem('drawingTimer', localStorage.getItem('drawingTimer') - 5)
    //Wait for 1 second before reloading
    setTimeout(function () {
      location.reload()
    }, 1000)
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

  let progress = localStorage.getItem('drawingProgress') || 0
  let drawingobjects = [
    'A',
    'B',
    'C',
    'D',
    'E',
    'F',
    'G',
    'H',
    'I',
    'J',
    'K',
    'L',
    'M',
    'N',
    'O',
    'P',
    'Q',
    'R',
    'S',
    'T',
    'U',
    'V',
    'W',
    'X',
    'Y',
    'Z',
  ]
  let drawingobject =
    drawingobjects[Math.floor(Math.random() * drawingobjects.length)]
</script>

<div>
  <h3>Draw A '{drawingobject}'</h3>
</div>
<SvelteToast />
<div class="timer">
  <!-- Timer -->
  <Timer countdown={timer} on:completed={notDone} />
</div>

<div class="content">
  <iframe
    height="650"
    width="900"
    title="Drawing Practice"
    src="https://editor.p5js.org/aniketgarg1/full/6wWCNepZI"
  />
</div>
<button on:click={done}> I'm done </button>

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
