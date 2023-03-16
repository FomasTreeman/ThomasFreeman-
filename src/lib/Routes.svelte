<script>
  import Stack from "./Stack.svelte";

  function scrollIntoView({ target }) {
    const el = document.querySelector(target.getAttribute("href"));
    if (!el) return;
    el.scrollIntoView({
      behavior: "smooth",
    });
  }
</script>

<div class="flex">
  <div class="flex column">
    <a class="card" href="#about" on:click|preventDefault={scrollIntoView}>
      About
    </a>
    <a class="card" href="#project" on:click|preventDefault={scrollIntoView}>
      Comms
    </a>
    <a class="card" href="#readmes" on:click|preventDefault={scrollIntoView}>
      ReadMe
    </a>
  </div>
</div>
<span class="stack">
  <Stack />
</span>

<style>
  .flex {
    margin-left: var(--margin-left);
    display: flex;
  }

  .column {
    max-height: 10rem;
    flex-direction: column;
    flex-wrap: wrap;
    align-content: baseline;
  }

  .stack {
    display: flex;
    align-items: center;
    margin-top: 5rem;
    width: 100%;
    overflow-x: hidden;
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
</style>
