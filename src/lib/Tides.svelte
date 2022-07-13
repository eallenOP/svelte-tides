<script>
  import { dataset_dev } from "svelte/internal";

  const fetchTides = (async () => {
    const response = await fetch(
      "https://api.niwa.co.nz/tides/data?lat=-45.75&long=170.660"
    );
    return await response.json();
  })();
</script>

{#await fetchTides}
  <p>...waiting</p>
{:then data}
  {#each data.values as tide}
    <p>
      {tide.time} height:
      {tide.value}
    </p>
  {/each}
{:catch error}
  <p>An error occurred!</p>
{/await}
