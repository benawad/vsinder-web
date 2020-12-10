<script lang="ts">
  import { onMount } from "svelte";
  import CodeCard from "./CodeCard.svelte";

  import type { Profile } from "./types";

  let profiles: Profile[] = [];

  onMount(async () => {
    const r = await fetch("http://localhost:3001/leaderboard");
    const data = await r.json();
    profiles = data.profiles;
  });
</script>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  div {
    margin-bottom: 50px;
  }
</style>

<main>
  {#each profiles as p, i}
    <div>
      <CodeCard profile={p} />
      <h1>{p.numLikes} likes</h1>
    </div>
  {/each}
</main>
