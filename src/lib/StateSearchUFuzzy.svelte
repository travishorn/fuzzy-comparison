<script lang="ts">
  // https://github.com/leeoniya/uFuzzy
  import uFuzzy from "@leeoniya/ufuzzy";
  import StateSearchResults from "./StateSearchResults.svelte";
  import type { State } from "./types";

  let props = $props<{ states: State[]; keys: string[]; query: string }>();

  let uf = $derived(new uFuzzy());

  // Create searchable strings by combining values from the specified keys
  let haystack = $derived(
    props.states.map((state: State) =>
      props.keys.map((key: string) => state[key as keyof State]).join(" ")
    )
  );

  let display: State[] = $derived.by(() => {
    const trimmedQuery = props.query.trim();
    if (!trimmedQuery) {
      return props.states;
    }

    const result = uf.search(haystack, trimmedQuery);
    const [idxs, info, order] = result;

    // If no matches, return empty array
    if (!idxs || idxs.length === 0 || !info || !order) {
      return [];
    }

    // Map the results back to USState objects
    // order is a double-indirection array, so we use info.idx[order[i]]
    return order.map((orderIdx) => props.states[info.idx[orderIdx]]);
  });
</script>

<StateSearchResults results={display} provider="uFuzzy" />
