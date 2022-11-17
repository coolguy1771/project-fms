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
  let progress = localStorage.getItem('signingProgress') || 0
</script>

<div>
  <h3>Please sign your name</h3>
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
