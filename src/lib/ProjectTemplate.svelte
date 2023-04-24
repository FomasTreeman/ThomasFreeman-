<script>
  import Divider1 from "./Divider1.svelte";
</script>

<Divider1 flipped={false} />
<article>
  <h2>My automated betting bot</h2>
  <p>
    This project was a significant undertaking, proposed by a friend, and is
    very open-ended. I utilized skills in Shell scripting, socket handling,
    security, cypress/web scraping, and Excel. Additionally, I created a custom
    logging system and previously deployed it on my NAS within a Docker
    container but found a limitation with a tool i was using and later removed
    the need for E2E testing tools for scraping and thereby also not needing a
    docker container.
  </p>
  <h3>UI:</h3>
  <p>
    Clients were unaware of their trades and wanted to track the bot&lsquo;s
    progress. To help, I created a website using svelte-kit and a more simple
    mobile app for Android users. The website provided graphs, trade history,
    and fun stats. I also created a developer page secured by password to manage
    app settings and git branch/tag updates.
  </p>
  <h3>How it works:</h3>
  <p>
    We scrape from a tips wesbite the relavant data and check it against our
    'system', these are a set of rules that we have created to determine if a
    bet is worth it. If it is, we then create a stream/open a websocket to
    betfair api waiting for the odds to come into that 'systems' range. Once
    they do, we place a bet.
  </p>
  <h3>Future:</h3>
  <p>
    In the future i hope to attempt a more mathematical approach and net a
    profit from laying all trades in a market.
  </p>
  <h3>Skill and tools used/learned:</h3>
  <p>
    More advanced shell scripting; tool such as pm2, docker, vi, executable
    shell scripts for CI, but I know use github actions and for a true CI/CD
    pipeline. In terms of more devOps I have got the option to remotely change
    variables/settings of the app live. Also sigInts are emailed to me for peace
    of mind.
  </p>
  <h3>Issues I had to overcome:</h3>
  <p>
    Had trouble scraping the tips website, originally tried Nightmarejs, but
    rewrote using cypress + jquery for logging benefits. Later needed to scrape
    the site for different betting data but parallelization required Cypress
    Cloud subscription. Workaround using asynchronous cypress processes caused
    login cookie conflicts. Discovered that using fetch request to get raw html
    of the page and parsing with cheerio.js was quicker and easier.
  </p>
</article>
<img class="blob" src="blob1.svg" alt="blob1" />
<img class="blob" src="blob2.svg" alt="blob2" />
<Divider1 flipped={true} />

<style>
  :not(:first-child) {
    margin-left: var(--margin-left);
  }

  p {
    max-width: calc(100% - 40vw - var(--margin-left) - 2rem);
  }

  .blob {
    position: absolute;
    width: 40vw;
    top: 4rem;
    right: 0rem;
    z-index: 4;
  }

  .blob[src="blob1.svg"] {
    z-index: 3;
  }

  article {
    height: inherit;
    overflow-y: scroll;
  }

  article > * {
    /* overriding article default  */
    margin-left: 0px !important;
  }

  @media (max-width: 800px) {
    :not(:first-child) {
      margin-left: 2rem;
    }

    .blob {
      display: none;
    }

    article {
      margin-right: 1rem;
    }

    h2 {
      margin-top: 0rem;
    }

    h3 {
      margin-left: 0px !important;
      margin-bottom: 0.5rem;
    }

    p {
      max-width: 100%;
      padding: 0%;
      margin: 0px !important;
    }
  }
</style>
