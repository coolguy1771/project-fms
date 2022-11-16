<script>
  function done() {
    progress = parseInt(progress) + 10
    localStorage.setItem('signingProgress', progress)
    location.reload()
  }
  let progress = localStorage.getItem('signingProgress') || 0

</script>
<div>
  <h2> Please sign your name</h2>
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
