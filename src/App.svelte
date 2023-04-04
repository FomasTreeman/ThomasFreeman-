<script>
  import About from "./lib/About.svelte";
  import Background from "./lib/Background.svelte";
  import ProjectTemplate from "./lib/ProjectTemplate.svelte";
  import ReadMes from "./lib/ReadMes.svelte";
  import Routes from "./lib/Routes.svelte";
  // import Contact from "./lib/Contact.svelte";

  let dark = true;
  let scrollY;
  let innerHeight;
  let scroll;

  $: scroll = scrollY / innerHeight;
</script>

<main style={dark ? "--backgroundColor: black" : "--backgroundColor: white"}>
  <Background />
  <img
    src="globe.png"
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
    <Routes />
  </section>

  <section id="readmes">
    <h1 class="center title">MY PROJECTS.</h1>
    <ReadMes />
  </section>
</main>
<svelte:window bind:scrollY bind:innerHeight />

<style>
  :global(:root) {
    --margin-left: 5rem;
  }

  :global(.center) {
    display: block;
    text-align: center;
    margin-inline: auto;
  }

  section {
    position: relative;
    height: 50rem;
  }

  section#about {
    padding-top: 3rem;
  }

  section#project {
    position: relative;
    margin: 0%;
    background-color: rgb(5, 4, 5);
    padding-top: 5rem;
  }

  section#routes {
    margin-block: calc(76px * 2);
    height: fit-content;
  }

  .title {
    font-size: xx-large;
  }

  #readmes .title {
    margin-top: 5rem;
    max-width: max-content;
    padding: 1rem;
    border: 0.5rem solid var(--color);
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
