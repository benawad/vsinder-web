<script lang="ts">
  import { onMount } from "svelte";
  import CodeCard from "./CodeCard.svelte";

  import type { Profile } from "./types";

  let profiles: Profile[] = [];

  onMount(async () => {
    const r = await fetch("https://api.vsinder.com/leaderboard");
    const data = await r.json();
    profiles = data.profiles;
  });
</script>

<style>
  main {
    text-align: center;
  }
  main > div {
    margin-bottom: 50px;
  }
  main > div > div {
    display: flex;
    margin-bottom: 8px;
    align-items: center;
    justify-content: center;
  }
</style>

<main>
  {#each profiles as p, i}
    <div>
      <div>
        <CodeCard profile={p} />
      </div>
      <h1>{p.numLikes} likes</h1>
    </div>
  {/each}
</main>
