<script lang="ts">
  import { FormGroup, Input, Label } from 'sveltestrap';
	import { buildSearchBox } from '@coveo/headless';
  import { searchEngine } from "../SearchEngine";
  import { writable } from "svelte/store";

  export let searchAsYouTypeDelay = 500;
  export const searchBoxController = buildSearchBox(searchEngine);
  export const searchBoxState = writable(searchBoxController.state);
  searchBoxController.subscribe(() => searchBoxState.set(searchBoxController.state));

  let text = "";
  let timer;
  $: searchBoxController.updateText(text);

  function handleKeyUp(e) {
    if (e.key === "Enter") {
      searchBoxController.submit();
    }
  }

  function handleInputChange(e) {
    clearTimeout(timer);
    timer = setTimeout(() => {
      searchBoxController.submit()
    }, searchAsYouTypeDelay);
  }
</script>

<FormGroup>
  <Label for="exampleSearch">Search</Label>
  <Input
    type="search"
    name="search"
    id="exampleSearch"
    placeholder="search placeholder"
    bind:value={text}
    on:keyup={handleKeyUp}
    on:input={handleInputChange} />
</FormGroup>
<!-- <input type="search" bind:value={text} on:keyup={handleKeyUp} on:input={handleInputChange} /> -->