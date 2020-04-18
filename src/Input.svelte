<script>
  let value = "";
  let loading = false;
  let response = [];
  const handleInput = () => (value = event.target.value);

  $: if (value.length > 2) {
    loading = true;
    fetch(`http://www.omdbapi.com/?s=${value}&apikey=fd906ccc`)
      .then(res => res.json())
      .then(apiResponse => {
        response = apiResponse.Search || [];
        loading = false;
      });
  }
</script>

<input placeholder="Search movies..." {value} on:input={handleInput} />

{#if loading > 0}
  <strong>Buscando ...</strong>
{:else if response.length > 0}
  <strong>Tenemos {response.length}</strong>
{:else}
  <strong>No hay resultados</strong>
{/if}
