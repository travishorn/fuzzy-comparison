<script lang="ts">
  // https://github.com/farzher/fuzzysort
  import fuzzysort from "fuzzysort";
  import StateSearchResults from "./StateSearchResults.svelte";
  import type { State } from "./types";

  let props = $props<{ states: State[]; keys: string[]; query: string }>();

  let display: State[] = $derived(
    props.query.trim()
      ? fuzzysort
          .go(props.query.trim(), props.states, { keys: props.keys })
          .map((result) => result.obj)
      : props.states
  );
</script>

<StateSearchResults results={display} provider="Fuzzysort" />
