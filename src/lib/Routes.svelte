<script>
  import Stack from "./Stack.svelte";

  let hidden = true;

  function scrollIntoView({ target }) {
    const el = document.querySelector(target.getAttribute("href"));
    if (!el) return;
    el.scrollIntoView({
      behavior: "smooth",
    });
  }

  $: console.log(hidden);
</script>

<div class="flex column">
  <a
    class="card small-card"
    href="#about"
    on:click|preventDefault={scrollIntoView}
  >
    About Me
  </a>
  <a
    class="card small-card"
    href="#project"
    on:click|preventDefault={scrollIntoView}
  >
    Betting Bot
  </a>
  <a class="card" href="#readmes" on:click|preventDefault={scrollIntoView}>
    ReadMes / <br /> Projects
  </a>
  <button class="card round-card" on:click={() => (hidden = !hidden)}>
    <h1 class:hidden={!hidden}>@</h1>
    <span class="flex" class:hidden>
      <a href="https://github.com/FomasTreeman">
        <img src="github.png" alt="github" />
      </a>
      <a href="https://www.linkedin.com/in/fomas-treeman/">
        <img src="linkedin.png" alt="linkedin" />
      </a>
      <a href="mailto: tom@team-freeman.com">
        <img src="gmail.png" alt="gmail" />
      </a>
    </span>
  </button>
</div>
<!-- <a href="https://www.flaticon.com/free-icons/linkedin" title="linkedin icons"
  >Linkedin icons created by Flaticon</a
> -->
<span class="stack">
  <Stack />
</span>

<style>
  .flex {
    display: flex;
    gap: 1rem;
  }

  .column {
    max-height: 25rem;
    flex-direction: column;
    flex-wrap: wrap;
    align-content: baseline;
    margin-left: var(--margin-left);
  }

  .stack {
    display: flex;
    align-items: center;
    margin-top: 5rem;
    width: 100%;
    overflow-x: hidden;
  }

  .card {
    margin: 1rem;
    width: 23rem;
    height: 23rem;
    background-color: var(--background-color);
    border-radius: 2rem;
    font-size: xx-large;
    text-transform: uppercase;
    font-weight: 800;
    text-align: center;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 10px 10px 0px 0px var(--link-color);
    transition: all 1s cubic-bezier(0.075, 0.82, 0.165, 1);
  }

  .small-card {
    width: 10rem;
    height: 10rem;
  }

  .round-card {
    color: var(--link-color);
    border-radius: 50%;
    font-size: xxx-large;
    box-shadow: none;
    border-color: var(--link-color);
    border-width: 0.5rem;
  }

  a.card:hover {
    transform: scale(1.1);
    transition: all 1s cubic-bezier(0.075, 0.82, 0.165, 1);
    color: var(--link-color-hover);
  }

  .round-card:hover span.flex {
    /* visibility: visible; */
    /* transition: visibility 1s ease-out, opacity 0.5s linear; */
  }

  /* ? signal selected/visible */
  button:not(> .hidden) {
    background-color: yellow;
  }

  .hidden {
    /* fade in from the side */
    visibility: hidden;
  }

  button span.flex {
    position: absolute;
    top: 11.5rem;
  }

  a img {
    width: 3rem;
    height: 3rem;
    animation: rotate 1s ease-in-out infinite;
    animation-play-state: paused;
  }

  a img:hover {
    animation-play-state: running;
  }
</style>
