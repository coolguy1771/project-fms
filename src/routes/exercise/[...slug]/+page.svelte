<script>
  import { onMount } from 'svelte'
  import Typing from '$lib/components/exercise/typing.svelte'
  import Drawing from '$lib/components/exercise/drawing.svelte'
  import Signing from '$lib/components/exercise/signing.svelte'

  let exercise = window.location.pathname.split('/')[2]
  let visible = false

  onMount(() => {
    visible = true
  })
</script>

{#if exercise === 'typing'}
  <Typing />
{:else if exercise === 'drawing'}
  <Drawing />
{:else if exercise === 'signing'}
  <Signing />
{/if}
