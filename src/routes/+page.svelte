<script>
  import Greeting from '../lib/components/greeting.svelte'
  import { fade } from 'svelte/transition'

  let visited = false
  let userName = localStorage.getItem('name') || ''

  if (userName !== '') {
    visited = true
  }

  function setName() {
    localStorage.setItem('name', userName)
    visited = true
  }
</script>

{#if !visited}
  <h1>What should we call you?</h1>
  <input bind:value={userName} />
  <button on:click={setName}>Submit</button>
{:else}
  <div transition:fade={{ delay: 300, duration: 300 }}>
    <Greeting name={userName} />
    <button
      on:click={() => {
        window.location.href = '/exercise'
      }}
    >
      Start
    </button>
  </div>
{/if}

<style>
  button {
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
