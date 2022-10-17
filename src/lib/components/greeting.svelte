<script>
  import { onMount } from 'svelte'

  export let name

  let now = new Date()

  let weekdays = ['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT']
  let months = [
    'JAN',
    'FEB',
    'MAR',
    'APR',
    'MAY',
    'JUN',
    'JUL',
    'AUG',
    'SEP',
    'OCT',
    'NOV',
    'DEC',
  ]

  $: day = weekdays[now.getDay()]
  $: month = months[now.getMonth()]
  $: date = now.getDate().toString()

  $: {
    if (date.length < 2) date = '0' + date
  }

  $: greeting = greetingText(now.getHours(), name)

  function greetingText(hours, name) {
    let greeting
    switch (Math.floor(hours / 6)) {
      case 0:
        greeting = 'Good night'
        break
      case 1:
        greeting = 'Good morning'
        break
      case 2:
        greeting = 'Good afternoon'
        break
      default:
        greeting = 'Good evening'
        break
    }

    return `${greeting}, ${name}!`
  }

  onMount(() => {
    const interval = setInterval(() => {
      now = new Date()
    }, 30000)

    return () => {
      clearInterval(interval)
    }
  })
</script>

<section>
  <h1>{greeting}</h1>
  <h2>{day}, {month} {date}</h2>
</section>

<style>
  section {
    z-index: 1;
  }
</style>
