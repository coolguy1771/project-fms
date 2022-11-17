<script>
  import '../app.css'
  import MenuBar from '$lib/components/menuBar.svelte'
  import { fade } from 'svelte/transition'
  import { onMount } from 'svelte'

  let visible = false
  let visited = false
  let userName = ''

  function setName() {
    localStorage.setItem('name', userName)
    visited = true
  }

  onMount(() => {
    visible = true
    if (localStorage.getItem('name') != null) {
      visited = true
      userName = localStorage.getItem('name')
    }
  })
</script>

{#if visible}
  <main id="container" transition:fade={{ delay: 300, duration: 300 }}>
    <MenuBar />
    {#if !visited}
      <h1>What should we call you?</h1>
      <input bind:value={userName} />
      <button class="nameButton" on:click={setName}>Submit</button>
    {:else}
      <slot />
    {/if}
  </main>
{:else}
  <div>
    <h1 class="loading">Loading...</h1>
  </div>
{/if}

<style>
  .loading {
    text-align: center;
    margin-top: 50px;
  }

  main {
    align-items: stretch;
    display: grid;
    grid-column-gap: 20px;
    grid-row-gap: 3vh;
    grid-template-columns: 1fr;
    grid-template-rows: auto;
    justify-items: stretch;
    margin-left: auto;
    margin-right: auto;
    margin-top: 5vh;
    width: 80%;
  }

  @media screen and (max-width: 1260px) {
    main {
      align-items: stretch;
      display: grid;
      grid-column-gap: 10px;
      grid-row-gap: 0px;
      grid-template-columns: 1fr;
      grid-template-rows: auto;
      justify-items: stretch;
      margin-bottom: 1vh;
      margin-left: auto;
      margin-right: auto;
      width: 90%;
    }
  }

  @media screen and (max-width: 667px) {
    main {
      align-items: stretch;
      display: grid;
      grid-column-gap: 20px;
      grid-row-gap: 0px;
      grid-template-columns: 1fr;
      grid-template-rows: auto;
      justify-items: stretch;
      margin-bottom: 1vh;
      width: 90%;
    }
  }
  .nameButton {
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
