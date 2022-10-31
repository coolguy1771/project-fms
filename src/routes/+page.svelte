<script>
  import Greeting from '../lib/components/greeting.svelte'
  import { fade } from 'svelte/transition'

  let userName = localStorage.getItem('name')
</script>

<svelte:head>
  <title>Home</title>
</svelte:head>

<div transition:fade={{ delay: 300, duration: 300 }}>
  <Greeting name={userName} />
  <button
    on:click={() => {
      window.location.href = window.location.pathname + '/exercise'
    }}
  >
    Start
  </button>
</div>

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
