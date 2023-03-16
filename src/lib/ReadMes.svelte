<script>
  import showdown from "showdown";
  import { onMount } from "svelte";
  import { Base64 } from "../../node_modules/js-base64";
  let mds = [];

  onMount(async () => {
    const pinned = [
      "SoonTHC",
      "KodiTV",
      "Weather-TM",
      "Comms",
      // "Three.js-Experiment",
      "face-recognition-brain",
      // "Boids_Development",
      "Portfolio",
    ];
    let pinnedMds = [];
    const resp = await fetch(
      `https://api.github.com/users/FomasTreeman/repos?per_page=100`,
      {
        headers: {
          Accept: "application/vnd.github+json",
          Authorization: "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",
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
{#each mds as md}
  <article>
    {@html new showdown.Converter().makeHtml(md)}
  </article>
{/each}

<style>
  article {
    background-color: #454542;
    max-width: 76%;
    margin-block: 2rem;
    margin-inline: auto;
    padding: 3rem;
  }
</style>
