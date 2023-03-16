<script>
  import Divider1 from "./Divider1.svelte";
</script>

<Divider1 flipped={false} />
<Divider1 flipped={true} />
<h2>My Messaging Service</h2>
<p>
  Lorem ipsum dolor, sit amet consectetur adipisicing elit. Nisi, fugit
  quisquam. Rem similique magnam cumque quod fugiat corporis doloribus
  aspernatur, at dolores. Ratione beatae quasi sint reiciendis necessitatibus
  quibusdam vitae? Lorem ipsum dolor, sit amet consectetur adipisicing elit.
  Incidunt perferendis recusandae dicta temporibus tempore, vel voluptate
  dolores consequuntur nihil fugiat facilis dolor, quaerat deleniti rem minus
  fugit laudantium nemo ut!Lorem Lorem ipsum dolor sit, amet consectetur
  adipisicing elit. Tempore reiciendis odio minima! Ab impedit pariatur et, non
  dolores facere voluptatibus neque, delectus eos doloribus consequuntur minus
  amet quis nesciunt <dolorem class="lorem" />
</p>
<img class="blob" src="blob1.svg" alt="blob1" />
<img class="blob" src="blob2.svg" alt="blob2" />

<style>
  h2 {
    padding-top: 1rem;
  }

  :not(:first-child) {
    margin-left: var(--margin-left);
  }

  p {
    max-width: calc(100% - 42rem - var(--margin-left));
  }

  .blob {
    position: absolute;
    width: 40rem;
    top: 4rem;
    right: 0rem;
    z-index: 4;
  }

  .blob[src="blob1.svg"] {
    z-index: 3;
  }
</style>
