<script lang="ts">
  import StateSearchFuse from "./lib/StateSearchFuse.svelte";
  import StateSearchFuzzysort from "./lib/StateSearchFuzzysort.svelte";
  import StateSearchUFuzzy from "./lib/StateSearchUFuzzy.svelte";
  import StateSearchLunr from "./lib/StateSearchLunr.svelte";
  import StateSearchOrama from "./lib/StateSearchOrama.svelte";
  import type { State } from "./lib/types";

  let query = $state("");

  const states: State[] = [
    { abbreviation: "AL", name: "Alabama" },
    { abbreviation: "AK", name: "Alaska" },
    { abbreviation: "AZ", name: "Arizona" },
    { abbreviation: "AR", name: "Arkansas" },
    { abbreviation: "AS", name: "American Samoa" },
    { abbreviation: "CA", name: "California" },
    { abbreviation: "CO", name: "Colorado" },
    { abbreviation: "CT", name: "Connecticut" },
    { abbreviation: "DE", name: "Delaware" },
    { abbreviation: "DC", name: "District of Columbia" },
    { abbreviation: "FL", name: "Florida" },
    { abbreviation: "GA", name: "Georgia" },
    { abbreviation: "GU", name: "Guam" },
    { abbreviation: "HI", name: "Hawaii" },
    { abbreviation: "ID", name: "Idaho" },
    { abbreviation: "IL", name: "Illinois" },
    { abbreviation: "IN", name: "Indiana" },
    { abbreviation: "IA", name: "Iowa" },
    { abbreviation: "KS", name: "Kansas" },
    { abbreviation: "KY", name: "Kentucky" },
    { abbreviation: "LA", name: "Louisiana" },
    { abbreviation: "ME", name: "Maine" },
    { abbreviation: "MD", name: "Maryland" },
    { abbreviation: "MA", name: "Massachusetts" },
    { abbreviation: "MI", name: "Michigan" },
    { abbreviation: "MN", name: "Minnesota" },
    { abbreviation: "MS", name: "Mississippi" },
    { abbreviation: "MO", name: "Missouri" },
    { abbreviation: "MT", name: "Montana" },
    { abbreviation: "NE", name: "Nebraska" },
    { abbreviation: "NV", name: "Nevada" },
    { abbreviation: "NH", name: "New Hampshire" },
    { abbreviation: "NJ", name: "New Jersey" },
    { abbreviation: "NM", name: "New Mexico" },
    { abbreviation: "NY", name: "New York" },
    { abbreviation: "NC", name: "North Carolina" },
    { abbreviation: "ND", name: "North Dakota" },
    { abbreviation: "MP", name: "Northern Mariana Islands" },
    { abbreviation: "OH", name: "Ohio" },
    { abbreviation: "OK", name: "Oklahoma" },
    { abbreviation: "OR", name: "Oregon" },
    { abbreviation: "PA", name: "Pennsylvania" },
    { abbreviation: "PR", name: "Puerto Rico" },
    { abbreviation: "RI", name: "Rhode Island" },
    { abbreviation: "SC", name: "South Carolina" },
    { abbreviation: "SD", name: "South Dakota" },
    { abbreviation: "TN", name: "Tennessee" },
    { abbreviation: "TX", name: "Texas" },
    { abbreviation: "TT", name: "Trust Territories" },
    { abbreviation: "UT", name: "Utah" },
    { abbreviation: "VT", name: "Vermont" },
    { abbreviation: "VA", name: "Virginia" },
    { abbreviation: "VI", name: "Virgin Islands" },
    { abbreviation: "WA", name: "Washington" },
    { abbreviation: "WV", name: "West Virginia" },
    { abbreviation: "WI", name: "Wisconsin" },
    { abbreviation: "WY", name: "Wyoming" },
  ];

  const keys = ["abbreviation", "name"];
</script>

<input type="text" bind:value={query} placeholder="Search" />

<main>
  <StateSearchFuse {states} {keys} {query} />
  <StateSearchFuzzysort {states} {keys} {query} />
  <StateSearchUFuzzy {states} {keys} {query} />
  <StateSearchLunr {states} {keys} {query} />
  <StateSearchOrama {states} {keys} {query} />
</main>

<style>
  :global(body) {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    margin: 0;
    padding: 0;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
      "Helvetica Neue", Arial, sans-serif;
  }

  :global(#app) {
    padding: 2rem;
    display: flex;
    flex-direction: column;
    gap: 2rem;
  }

  input {
    padding: 1rem 1.5rem;
    width: 100%;
    max-width: 600px;
    font-size: 1.1rem;
    border: none;
    border-radius: 12px;
    background: rgba(255, 255, 255, 0.95);
    transition: all 0.3s ease;
    outline: none;
    margin: 0 auto;
    display: block;
  }

  input:focus {
    background: rgba(255, 255, 255, 1);
    box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
    transform: translateY(-2px);
  }

  input::placeholder {
    color: #9ca3af;
  }

  main {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    gap: 2rem;
    width: 100%;
    max-width: 1600px;
    margin: 0 auto;
  }

  @media (max-width: 768px) {
    main {
      grid-template-columns: 1fr;
    }

    :global(#app) {
      padding: 1rem;
    }
  }
</style>
