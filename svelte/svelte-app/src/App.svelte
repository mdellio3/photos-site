<script>
    import fetch from 'svelte/fetch';

    let greeting = '';
    let name = '';
    let imgSrc = '';

    const getGreeting = async (name) => {
        const resp = await fetch('http://localhost:8080/hello?name=' + name);
        if (resp.ok) greeting = await resp.text();
        console.log(resp);
        console.log(greeting);
    }

    const getPhoto = async () => {
      const resp = await fetch('http://localhost:8080/hello');
      const blob = await resp.blob();
      imgSrc = URL.createObjectURL(blob);
    }
</script>

<h1>Svelte + Spring!</h1>
<input type="text" bind:value={name}/>
<button on:click={getGreeting(name)}>Get Greeting</button>
<button on:click={getPhoto}>View Photo</button>
<p>{greeting}</p>
{#if imgSrc != ''}
<img src={imgSrc} alt="Fetched from API" />
{/if}

<style>
    h1, p {
  color: purple;
  text-align: center;
}

input {
  display: block;
  margin: 0 auto;
  padding: 10px;
  font-size: 20px;
}

button {
  display: block;
  margin: 10px auto;
  padding: 10px;
  font-size: 20px;
  background-color: purple;
  color: white;
  border: none;
}

</style>