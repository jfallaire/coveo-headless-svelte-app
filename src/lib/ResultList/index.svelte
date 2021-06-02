<script lang="ts">
  import { Card } from 'sveltestrap';
  import { buildResultList } from '@coveo/headless';
  import { searchEngine } from "../SearchEngine";
  import { writable } from "svelte/store";

  export const resultListController = buildResultList(searchEngine);
  export const resultListState = writable(resultListController.state);
  resultListController.subscribe(() => resultListState.set(resultListController.state));
</script>

<div>
  {#if $resultListState.results.length === 0}
    {#if $resultListState.isLoading}
      <span>Loading...</span>
    {:else}
      <div>No Results</div>
    {/if}
  {:else}
    {#each $resultListState.results as { clickUri, title, excerpt }}
      <Card body>
        <a href={clickUri}>{title}</a>
        <div class="excerpt">{excerpt}</div>
      </Card>
    {/each}
  {/if}
</div>