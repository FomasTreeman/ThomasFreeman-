<script>
  import About from "./lib/About.svelte";
  import Background from "./lib/Background.svelte";
  import DarkMode from "./lib/DarkMode.svelte";
  import Divider1 from "./lib/Divider1.svelte";
  import ProjectTemplate from "./lib/ProjectTemplate.svelte";
  import Stack from "./lib/Stack.svelte";
  let dark = true;
  let scrollY;
  let innerHeight;
  let scroll;

  function scrollIntoView({ target }) {
    const el = document.querySelector(target.getAttribute("href"));
    if (!el) return;
    el.scrollIntoView({
      behavior: "smooth",
    });
  }

  $: scroll = scrollY / innerHeight;
</script>

<main style={dark ? "--backgroundColor: black" : "--backgroundColor: white"}>
  <Background />
  <img
    src="/src/assets/globe.png"
    alt="globe"
    style="animation-delay: calc({scroll} * -1s);"
  />
  <section id="about">
    <About />
  </section>

  <section id="project">
    <ProjectTemplate />
  </section>

  <section id="routes">
    <div class="flex">
      <div class="flex column">
        <a class="card" href="#about" on:click|preventDefault={scrollIntoView}>
          About
        </a>
        <a
          class="card"
          href="#project"
          on:click|preventDefault={scrollIntoView}
        >
          Comms
        </a>
      </div>
    </div>
    <span class="stack">
      <Stack />
    </span>
  </section>
</main>
<svelte:window bind:scrollY bind:innerHeight />

<style>
  :global(:root) {
    --margin-left: 5rem;
  }

  .flex {
    margin-left: var(--margin-left);
    display: flex;
  }

  .column {
    max-height: 40rem;
    flex-direction: column;
    flex-wrap: wrap;
    align-content: baseline;
  }

  section {
    position: relative;
    height: 50rem;
  }

  section#routes {
    margin-block: calc(76px * 2);
  }

  section#project {
    margin: 0%;
    background-color: rgb(5, 4, 5);
  }

  .stack {
    display: flex;
    align-items: center;
    height: 100vh;
    width: 100vw;
    overflow: hidden;
  }

  a {
    margin: 1rem;
    padding-block: auto;
    width: 15rem;
    text-align: center;
    background-color: white;
    border-radius: 2rem;
    font-size: xx-large;
    text-transform: uppercase;
    font-weight: 800;
    box-shadow: 10px 10px 0px 0px rgba(0, 0, 0, 0.75);
  }

  a:hover {
    transform: skew(-20deg);
    transition: all 1s cubic-bezier(0.075, 0.82, 0.165, 1);
  }

  img[alt="globe"] {
    display: inline-block;
    position: fixed;
    right: 0px;
    margin: 1rem;
    width: 5rem;
    animation: rotate 1s linear infinite;
    animation-play-state: paused;
    z-index: 20;
  }
</style>
