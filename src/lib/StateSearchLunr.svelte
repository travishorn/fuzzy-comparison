<script lang="ts">
  // https://lunrjs.com/
  import lunr from "lunr";
  import StateSearchResults from "./StateSearchResults.svelte";
  import type { State } from "./types";

  let props = $props<{ states: State[]; keys: string[]; query: string }>();

  // Create index with abbreviation and name fields
  let index = $derived(
    lunr(function (this: lunr.Builder) {
      this.ref("id");
      this.field("abbreviation");
      this.field("name");

      props.states.forEach((state: State, idx: number) => {
        this.add({
          id: idx.toString(),
          abbreviation: state.abbreviation,
          name: state.name,
        });
      });
    })
  );

  let searchResults = $derived.by(() => {
    if (!props.query.trim()) return [];

    const query = props.query.trim();
    let results = index.search(query);

    // If no results and query is short, try with wildcard for prefix matching
    if (results.length === 0 && query.length < 4) {
      results = index.search(query + "*");
    }

    return results;
  });

  let display: State[] = $derived(
    props.query.trim()
      ? searchResults.map(
          (result: lunr.Index.Result) => props.states[parseInt(result.ref)]
        )
      : props.states
  );
</script>

<StateSearchResults results={display} provider="Lunr" />
