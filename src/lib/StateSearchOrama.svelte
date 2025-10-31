<script lang="ts">
  // https://docs.orama.com/
  import { create, search, insert } from "@orama/orama";
  import StateSearchResults from "./StateSearchResults.svelte";
  import type { State } from "./types";

  let props = $props<{ states: State[]; keys: string[]; query: string }>();

  // Create and populate Orama database with states
  let db = $derived.by(() => {
    const database = create({
      schema: {
        abbreviation: "string",
        name: "string",
      },
    });

    // Insert all states into the database
    props.states.forEach((state: State) => {
      insert(database, {
        abbreviation: state.abbreviation,
        name: state.name,
      });
    });

    return database;
  });

  let display: State[] = $derived.by(() => {
    if (!props.query.trim()) {
      return props.states;
    }

    // Perform search using Orama
    const searchResult = search(db, {
      term: props.query.trim(),
    });

    // Handle both sync and async results (Orama search may return Promise in some cases)
    if (searchResult instanceof Promise) {
      // If async, return empty array for now (would need $effect for proper async handling)
      return [];
    }

    // Create a Map of abbreviation to USState for efficient lookup
    const stateMap = new Map<string, State>(
      props.states.map((state: State) => [state.abbreviation, state])
    );

    // Map search results back to USState objects
    return searchResult.hits
      .map((hit) => {
        const abbreviation = hit.document.abbreviation as string;
        return stateMap.get(abbreviation);
      })
      .filter((state): state is State => state !== undefined);
  });
</script>

<StateSearchResults results={display} provider="Orama" />
