<script>
  import DarkMode from "./lib/DarkMode.svelte";
  import Divider1 from "./lib/Divider1.svelte";
  let dark = true;
</script>

<main style={dark ? "--backgroundColor: black" : "--backgroundColor: white"}>
  <section>
    <h1>Thomas Freeman</h1>
    <img class="head" src="/src/assets/factory.jpeg" alt="3d head scan" />

    <!-- <DarkMode bind:dark /> -->
  </section>
  <section class="project">
    <Divider1 />
    <h2>My Messaging Service</h2>
    <p>
      Lorem ipsum dolor, sit amet consectetur adipisicing elit. Nisi, fugit
      quisquam. Rem similique magnam cumque quod fugiat corporis doloribus
      aspernatur, at dolores. Ratione beatae quasi sint reiciendis
      necessitatibus quibusdam vitae?
    </p>
    <img class="blob" src="/src/assets/blob1.svg" alt="blob1" />
    <img class="blob" src="/src/assets/blob2.svg" alt="blob2" />
  </section>
</main>

<style>
  :global(:root) {
    --margin-left: 5rem;
  }

  h1 {
    margin: 0rem 0rem 0rem 7rem;
    padding-top: 5rem;
    color: #050405;
    font-size: xxx-large;
  }

  h2 {
    padding-top: 1rem;
  }

  img.head {
    margin: 8rem;
    height: 20rem;
    width: 20rem;
    object-fit: cover;
    border-radius: 50%;
    z-index: 5;
  }
  section {
    position: relative;
    height: 50rem;
  }

  .project > :not(:first-child) {
    margin-left: var(--margin-left);
  }

  p {
    max-width: calc(100% - 40rem - var(--margin-left));
  }

  main > :nth-child(2) {
    margin: 0%;
    background-color: rgb(5, 4, 5);
  }

  .blob {
    position: absolute;
    width: 40rem;
    top: 4rem;
    right: 0rem;
    z-index: 4;
  }

  .blob[src="/src/assets/blob1.svg"] {
    z-index: 3;
  }
</style>
