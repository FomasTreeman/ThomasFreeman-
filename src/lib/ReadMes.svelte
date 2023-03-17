<script>
  import showdown from "showdown";
  import { onMount } from "svelte";
  import { Base64 } from "../../node_modules/js-base64";
  let mds = [];
  const pinned = [
    "Comms",
    "Weather-TM",
    // "SoonTHC",
    "KodiTV",
    // "Three.js-Experiment",
    // "face-recognition-brain",
    // "Boids_Development",
    // "Portfolio",
  ];

  async function getHtml() {
    return await new showdown.Converter();
  }

  let promise = getHtml();

  onMount(async () => {
    let pinnedMds = [];
    const resp = await fetch(
      `https://api.github.com/users/FomasTreeman/repos?per_page=100`,
      {
        headers: {
          Accept: "application/vnd.github+json",
          Authorization: import.meta.env.TOKEN,
        },
      }
    );
    const repos = await resp.json();
    const repoNames = repos.map((repo) => repo.full_name.split("/")[1]);
    const pinnedRepos = repoNames.filter((name) => pinned.includes(name));
    await Promise.all(
      pinnedRepos.map(async (repoName) => {
        const resp = await fetch(
          `https://api.github.com/repos/FomasTreeman/${repoName}/readme`
        );
        const json = await resp.json();
        pinnedMds.push(Base64.decode(json.content));
      })
    );
    mds = pinnedMds;
  });
</script>

<!-- .md file -->
{#each mds as md, index}
  <div class={index % 2 == 0 ? "flip" : ""}>
    <img src="{pinned[index]}.png" alt="project scrnsht" />
    <article id="md ">
      {#await promise}
        <p>... waiting</p>
      {:then converter}
        {@html converter.makeHtml(md)}
      {:catch}
        <p>page in development</p>
      {/await}
    </article>
  </div>
{/each}

<style>
  article {
    background-color: black;
    mix-blend-mode: luminosity;
    max-width: 76%;
    /* margin-block: 2rem;
    margin-inline: auto;
    */
    padding: 3rem;
    /* border-radius: 2rem; */
    box-shadow: 10px 10px 10px rgba(59, 52, 21, 0.375);
  }

  div {
    display: flex;
    justify-content: space-around;
    align-items: center;
    margin: 5rem;
    gap: 1rem;
  }

  .flip {
    flex-direction: row-reverse;
  }

  img {
    height: 20rem;
    /* margin: 2rem; */
  }
</style>
