<script>
  import showdown from 'showdown';
  import { onMount } from 'svelte';
  import { Base64 } from '../../node_modules/js-base64';
  import ReadMeTitle from './ReadMeTitle.svelte';
  import Saos from 'saos';

  let repos = [];
  const productions = {
    Comms: 'https://comm-a.vercel.app/',
    'Weather-TM': 'https://fac27.github.io/Weather-TM/',
  };

  const pinned = [
    'Comms',
    'Weather-TM',
    // "SoonTHC",
    'KodiTV',
    // "Three.js-Experiment",
    // "face-recognition-brain",
    // "Boids_Development",
    // "Portfolio",
  ];

  async function getHtml() {
    return new showdown.Converter();
  }

  let promise = getHtml();

  onMount(async () => {
    const tempRepos = [];
    const resp = await fetch(
      `https://api.github.com/users/FomasTreeman/repos?per_page=100`,
      {
        headers: {
          Accept: 'application/vnd.github+json',
          Authorization: import.meta.env.TOKEN,
        },
      }
    );
    const jsonResp = await resp.json();
    const repoNames = jsonResp.map((repo) => repo.full_name.split('/')[1]);
    const pinnedRepos = repoNames.filter((name) => pinned.includes(name));
    await Promise.all(
      pinnedRepos.map(async (repoName) => {
        const resp = await fetch(
          `https://api.github.com/repos/FomasTreeman/${repoName}/readme`
        );
        const json = await resp.json();
        tempRepos.push({
          md: Base64.decode(json.content),
          name: repoName,
          url: `https://github.com/FomasTreeman/${repoName}`,
        });
      })
    );
    repos = tempRepos;
  });

  function renderHtml(html) {
    let reducedHtml = html.slice(0, 1000);

    return reducedHtml;
  }

  function handleObserver(x) {
    console.info(x.detail.observing);
  }
</script>

<!-- .md file -->
{#each repos as repo, index}
  <!-- <div class={index % 2 == 0 ? "flip" : ""}> -->
  <Saos
    animation={'slide-in-bottom 1s cubic-bezier(0.35, 0.5, 0.65, 0.95) both'}
  >
    <div>
      <!-- <img src="{repo.name}.png" alt="project scrnsht" /> -->
      <article id="md ">
        {#await promise}
          <h1>... waiting</h1>
        {:then converter}
          <header>
            {#if productions[repo.name]}
              <a href={productions[repo.name]} class="prod-link">
                <ReadMeTitle {repo} />
              </a>
            {:else}
              <ReadMeTitle {repo} />
            {/if}
          </header>
          {@html renderHtml(converter.makeHtml(repo.md))}
          <button>...</button>
          <!-- {@html converter.makeHtml(repo.md)} -->
        {:catch}
          <h1>page in development</h1>
        {/await}
      </article>
    </div>
  </Saos>
{/each}
<Saos on:update={handleObserver}>...</Saos>

<style>
  article {
    background-color: black;
    mix-blend-mode: luminosity;
    max-width: 76%;
    padding: 3rem;
    box-shadow: 10px 10px 10px rgba(59, 52, 21, 0.375);
  }

  div {
    display: flex;
    justify-content: space-around;
    align-items: center;
    margin: 5rem;
    gap: 1rem;
  }
  /* 
  .flip {
    flex-direction: row-reverse;
  } */

  a {
    z-index: 20;
  }

  a.prod-link {
    font-weight: 800;
    font-size: 3rem;
    color: greenyellow;
    text-decoration-line: underline;
  }

  a.prod-link:hover {
    mix-blend-mode: lighten;
  }

  @-webkit-keyframes -global-slide-in-bottom {
    0% {
      -webkit-transform: translateY(1000px);
      transform: translateY(1000px);
      opacity: 0;
    }
    100% {
      -webkit-transform: translateY(0);
      transform: translateY(0);
      opacity: 1;
    }
  }
  @keyframes -global-slide-in-bottom {
    0% {
      -webkit-transform: translateY(1000px);
      transform: translateY(1000px);
      opacity: 0;
    }
    100% {
      -webkit-transform: translateY(0);
      transform: translateY(0);
      opacity: 1;
    }
  }

  @media (max-width: 768px) {
    article {
      max-width: 100%;
      padding: 2rem;
      /* temporary solution for image */
      overflow-x: hidden;
    }
    div {
      margin: 0%;
      margin-top: 4rem;
    }
  }
</style>
