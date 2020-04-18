<script>
  let value = "";
  const handleInput = () => (value = event.target.value);

  $: if (value.length > 2) {
    fetch(`http://www.omdbapi.com/?s=${value}&apikey=fd906ccc`)
      .then(res => res.json())
      .then(apiResponse => {
        let reponse = apiResponse.Search;
        console.log(reponse);
      });
  }
</script>

<input type="text" {value} on:input={handleInput} />
