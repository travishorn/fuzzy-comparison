<script lang="ts">
  import type { State } from "./types";

  let props = $props<{ results: State[]; provider: string }>();
</script>

<div class="container">
  <table>
    <caption>{props.provider}</caption>
    <thead>
      <tr>
        <th>Abbreviation</th>
        <th>Name</th>
      </tr>
    </thead>
    <tbody>
      {#each props.results as state}
        <tr>
          <td>{state.abbreviation}</td>
          <td>{state.name}</td>
        </tr>
      {/each}
    </tbody>
  </table>
</div>

<style>
  .container {
    width: 100%;
    height: 300px;
    overflow: auto;
    display: flex;
    flex-direction: column;
  }

  table {
    border-collapse: collapse;
    width: 100%;
    background: rgba(255, 255, 255, 0.98);
    border-radius: 16px;
    overflow: hidden;
  }

  caption {
    font-size: 0.875rem;
    font-weight: 600;
    color: #ffffff;
    margin-bottom: 0.4rem;
    text-align: center;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  thead {
    background: linear-gradient(135deg, #f9fafb 0%, #f3f4f6 100%);
  }

  th {
    text-align: left;
    font-size: 0.75rem;
    font-weight: 600;
    color: #374151;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    border-bottom: 2px solid #e5e7eb;
  }

  tbody {
    max-height: 500px;
    overflow-y: auto;
    overflow-x: hidden;
  }

  tbody tr {
    transition: all 0.2s ease;
    cursor: pointer;
  }

  tbody tr:hover {
    background: linear-gradient(90deg, #f0f9ff 0%, #e0f2fe 100%);
    transform: scale(1.01);
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
  }

  td {
    vertical-align: top;
    text-align: left;
    font-size: 0.875rem;
    color: #1f2937;
    border-bottom: 1px solid #f3f4f6;
  }

  th,
  td {
    padding: 0.75rem;
  }

  tbody tr:last-child td {
    border-bottom: none;
  }

  tbody tr td:first-child {
    font-weight: 600;
    color: #6366f1;
    font-family: "SF Mono", "Monaco", "Cascadia Code", monospace;
    font-size: 0.8rem;
  }

  tbody tr td:last-child {
    color: #374151;
    font-weight: 500;
  }

  /* Custom scrollbar */
  tbody::-webkit-scrollbar {
    width: 8px;
  }

  tbody::-webkit-scrollbar-track {
    background: #f1f5f9;
    border-radius: 4px;
  }

  tbody::-webkit-scrollbar-thumb {
    background: #cbd5e1;
    border-radius: 4px;
  }

  tbody::-webkit-scrollbar-thumb:hover {
    background: #94a3b8;
  }

  /* Empty state */
  tbody:empty::after {
    content: "No results";
    display: block;
    padding: 2rem;
    color: #9ca3af;
    font-size: 0.875rem;
  }
</style>
