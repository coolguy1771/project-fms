<script>
  import Done from '$lib/sounds/correct.mp3'

  let doneSound = new Audio(Done)
  function done() {
    doneSound.play()
    progress = parseInt(progress) + 10
    localStorage.setItem('signingProgress', progress)
    //Wait for 1 second before reloading
    setTimeout(function () {
      location.reload()
    }, 1500)
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
