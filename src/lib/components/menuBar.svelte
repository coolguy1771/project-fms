<script>
  import { page } from '$app/stores'
  import { base } from '$app/paths'
  import github from '$lib/images/github.svg'
</script>

<header>
  <div class="corner" />

  <nav>
    <ul>
      <li class:active={$page.url.pathname === '/'}>
        <a href="{base}/">Home</a>
      </li>
      <li class:active={$page.url.pathname.startsWith('/exercise')}>
        <a href="{base}/exercise">Exercise</a>
      </li>
      <li class:active={$page.url.pathname === '/progress'}>
        <a href="{base}/progress">Progress</a>
      </li>
      <li class:active={$page.url.pathname === '/about'}>
        <a href="{base}/about">About</a>
      </li>
    </ul>
  </nav>

  <div class="corner">
    <a href="https://github.com/coolguy1771/project-fms">
      <img src={github} alt="GitHub" />
    </a>
  </div>
</header>

<style>
  header {
    display: flex;
    justify-content: space-between;
  }

  .corner {
    width: 3em;
    height: 3em;
  }

  .corner a {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
  }

  .corner img {
    width: 3em;
    height: 3em;
    object-fit: contain;
    fill: white;
  }

  nav {
    display: flex;
    justify-content: center;
  }

  ul {
    position: relative;
    padding: 0;
    margin: 0;
    height: 3em;
    display: flex;
    justify-content: center;
    align-items: center;
    list-style: none;
    background: var(--background);
    background-size: contain;
  }

  li {
    position: relative;
    height: 100%;
  }

  li.active::before {
    --size: 6px;
    content: '';
    width: 0;
    height: 0;
    position: absolute;
    top: 0;
    left: calc(50% - var(--size));
    border: var(--size) solid transparent;
    border-top: var(--size) solid var(--color-theme-1);
  }

  nav a {
    display: flex;
    height: 100%;
    align-items: center;
    padding: 0 0.5rem;
    color: var(--color-text);
    font-weight: 700;
    font-size: 0.8rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    text-decoration: none;
    transition: color 0.2s linear;
  }

  a:hover {
    color: var(--color-theme-1);
  }
</style>
