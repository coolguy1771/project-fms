<script>
  import { fade } from 'svelte/transition'

  import Typing from '$lib/components/exercise/typing.svelte'
  import Drawing from '$lib/components/exercise/drawing.svelte'
  import Signing from '$lib/components/exercise/signing.svelte'

  let exercise = window.location.pathname.split('/')[2]
</script>

<div transition:fade={{ delay: 300, duration: 300 }}>
  {#if exercise === 'typing'}
    <Typing />
  {:else if exercise === 'drawing'}
    <Drawing />
  {:else if exercise === 'signing'}
    <Signing />
  {/if}
</div>

<style>
</style>
