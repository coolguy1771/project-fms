<script>
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
  $: word

  function checkLetter(letter) {
    if (letter === word[0]) {
      word = word.slice(1)
      if (word.length === 0) {
        words = words.slice(1)
        if (words.length === 0) {
          done(exercise)
        } else {
          word = words[0]
          letters = word.split('')
        }
      }
    }
  }
</script>

<h1>Typing Practice</h1>

<div class="content">
  <div class="word">
    {#each letters as letter}
      <span class="letter">{letter}</span>
    {/each}
  </div>
  <div class="input">
    <input
      type="text"
      bind:value={word}
      on:keyup={checkLetter(word.split('', 1))}
    />
  </div>
</div>

<style>
  .invalid {
    color: red;
  }
</style>
