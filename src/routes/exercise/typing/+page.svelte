<script>
  import { SvelteToast, toast } from '@zerodevx/svelte-toast'
  import Correct from '$lib/sounds/correct.mp3'
  import Incorrect from '$lib/sounds/incorrect.mp3'

  let invalid
  let words = [
    'apple',
    'banana',
    'orange',
    'pear',
    'grape',
    'strawberry',
    'blueberry',
    'raspberry',
    'blackberry',
    'watermelon',
    'pineapple',
    'mango',
    'kiwi',
    'lemon',
    'lime',
    'coconut',
    'peach',
    'apricot',
    'cherry',
    'plum',
    'pepper',
    'tomato',
    'potato',
    'carrot',
    'onion',
    'garlic',
    'celery',
    'lettuce',
    'spinach',
    'broccoli',
    'cauliflower',
    'cucumber',
    'zucchini',
    'squash',
    'corn',
    'bean',
    'pea',
    'eggplant',
    'pumpkin',
    'mushroom',
    'chicken',
    'beef',
    'pork',
    'fish',
    'lobster',
    'crab',
    'shrimp',
    'oyster',
    'salmon',
    'tuna',
    'sardine',
    'egg',
    'cheese',
    'butter',
    'milk',
    'yogurt',
    'bread',
    'rice',
    'pasta',
    'noodle',
    'flour',
    'sugar',
    'salt',
    'pepper',
    'oil',
    'vinegar',
    'water',
    'juice',
    'coffee',
    'tea',
    'beer',
    'wine',
    'whiskey',
    'vodka',
    'rum',
    'gin',
    'soda',
    'juice',
    'milkshake',
    'smoothie',
    'cake',
    'cookie',
    'pie',
    'ice cream',
    'chocolate',
    'candy',
    'gum',
    'chewing gum',
    'lollipop',
    'cotton candy',
    'soda',
    'pop',
    'soda pop',
    'popcorn',
    'chips',
    'fries',
    'french fries',
    'pizza',
    'sandwich',
    'burger',
    'hot dog',
    'taco',
  ]
  let word = words[Math.floor(Math.random() * words.length)]
  let letters = word.split('')
  let userInput
  let progress = localStorage.getItem('typingProgress') || 0
  let correctSound = new Audio(Correct)
  let incorrectSound = new Audio(Incorrect)

  function checkWord() {
    if (userInput == word) {
      invalid = false
      word = words[Math.floor(Math.random() * words.length)]
      letters = word.split('')
      userInput = ''
      toast.push({ msg: 'Correct!', duration: 2000 })
      correctSound.play()
      progress = parseInt(progress) + 10
      localStorage.setItem('typingProgress', progress)
    } else {
      invalid = true
      toast.push({ msg: 'That was incorrect, try again', duration: 2000 })
      incorrectSound.play()
    }
  }
</script>

<h1>Typing Practice</h1>

<SvelteToast />
<div class="content">
  <div class="word">
    {#each letters as letter}
      <span class="noSelect" class:invalid>{letter}</span>
    {/each}
  </div>
  <div class="input">
    <input type="text" spellcheck="false" bind:value={userInput} />
    <button on:click={checkWord}>Check</button>
  </div>
</div>

<style>
  .input {
    align-items: left;
    font-family: monospace;
    font-size: 2rem;
  }
  .word {
    align-items: left;
    font-family: monospace;
    font-size: 6rem;
  }
  button {
    margin-top: 1rem;
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 0.5rem;
    background-color: green;
    color: white;
    font-size: 1.5rem;
    font-weight: bold;
    cursor: pointer;
  }
  .noSelect {
    -webkit-touch-callout: none; /* iOS Safari */
    -webkit-user-select: none; /* Safari */
    -khtml-user-select: none; /* Konqueror HTML */
    -moz-user-select: none; /* Old versions of Firefox */
    -ms-user-select: none; /* Internet Explorer/Edge */
    user-select: none; /* Non-prefixed version, currently
                                  supported by Chrome, Edge, Opera and Firefox */
  }
</style>
