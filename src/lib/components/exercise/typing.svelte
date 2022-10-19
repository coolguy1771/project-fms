<script>
  // Component Props
  export let body
  export let currentProgress
  export let progress
  export let indicators
  export let spectateMode = false
  // Here we import some game related stuff
  //import { currentPlayer } from "store/game/index.js";
  //import { WordsContainer } from "helpers/content.js";
  // We set some basic values
  const { words, characters } = new WordsContainer(body)

  // Here's happening our reactive magic
  $: isCorrect = (index) => index <= progress
  $: isIncorrect = (index) => index <= currentProgress && index > progress
  $: nextLetter = characters[progress]
  $: nextLetterIncorrect = characters[progress] !== characters[currentProgress]
</script>

<div class="content-box">
  <!-- Iterate over all the words -->
  {#each words as word, index}
    <span class="word" data-word-index={index}>
      <!-- Iterate over all the word's characters -->
      {#each word.characters as { key, index }}
        <span
          class="char"
          class:correct={isCorrect(index)}
          class:incorrect={isIncorrect(index)}
          data-char-index={index}
        >
          {@html key === ' ' ? '&#8197;' : key}
        </span>

        <!-- Iterate over indicators... -->
        {#each indicators as indicator (indicator.id)}
          <!--  ...and show the one that's on current character -->
          {#if indicator.progress === index}
            <span
              class={`indicator`}
              class:current={($currentPlayer &&
                indicator.id === $currentPlayer.id) ||
                spectateMode}
              style={`color: ${indicator.color}`}
            >
              <div
                class={`indicator-name`}
                style={`background-color: ${indicator.color}`}
              >
                {indicator.name}
              </div>
            </span>
          {/if}
        {/each}
      {/each}
    </span>
  {/each}
</div>

{#if nextLetter && !spectateMode}
  <kbd class="next-letter" class:incorrect={nextLetterIncorrect}>
    {#if nextLetterIncorrect}
      Press backspace
    {:else}y
      {nextLetter.key === ' ' ? 'Space' : nextLetter.key}
    {/if}
  </kbd>
{/if}
