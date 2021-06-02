<script lang="ts">
  import { FormGroup, Input, Card, CardBody, CardTitle, CardHeader } from 'sveltestrap';
  import { buildFacet } from '@coveo/headless';
  import { searchEngine } from "../SearchEngine";
  import { writable } from "svelte/store";

  export let field:string;
  export let title:string = 'no title';
  let options = { 
    field: field,
    numberOfValues: 10,
    sortCriteria: 'occurrences' as any
  }
  export const facetController = buildFacet(searchEngine, {options});
  export const facetState = writable(facetController.state);
  facetController.subscribe(() => facetState.set(facetController.state));

  function getFacetLabel(facetValue){
    return `${facetValue.value} (${facetValue.numberOfResults} results)`;
  }
</script>

<Card>
  <CardHeader>
    <CardTitle>{title}</CardTitle>
  </CardHeader>
  <CardBody>
  {#if $facetState.values.length === 0}
    <div>No facet values</div>
  {:else}
    <div>
      {#each $facetState.values as fv}
        <Input
          type="checkbox"
          checked={facetController.isValueSelected(fv)}
          disabled={$facetState.isLoading}
          label={getFacetLabel(fv)}
          on:change={()=>{facetController.toggleSelect(fv)}}
        />
      {/each}
    </div>
  {/if}
  </CardBody>
</Card>
