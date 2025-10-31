<script lang="ts">
  // https://fusejs.io/
  import Fuse from "fuse.js";
  import StateSearchResults from "./StateSearchResults.svelte";
  import type { State } from "./types";

  let props = $props<{ states: State[]; keys: string[]; query: string }>();

  let fuse = $derived(
    new Fuse<State>(props.states, { keys: props.keys, threshold: 0.2 })
  );

  let display: State[] = $derived(
    props.query.trim()
      ? fuse.search(props.query.trim()).map((r) => r.item)
      : props.states
  );
</script>

<StateSearchResults results={display} provider="Fuse.js" />
