<script>
  import { onMount } from "svelte";
  export let user;
  let name = "";
  let pokemons = [];
  let result = [];
  onMount(async () => {
    await fetch("https://pokeapi.co/api/v2/pokemon?limit=100&offset=0")
      .then((res) => res.json())
      .then((response) => {
        pokemons = response.results;
        console.log("🐹", pokemons);
      });
    change();
  });

  function change() {
    result = pokemons.filter(
      (pokemon) => pokemon.name.substring(0, name.length) === name
    );
  }
</script>

<main>
  <h1>Hello {user}!</h1>
  <input
    bind:value={name}
    on:input={change}
    type="text"
    placeholder="search pokemon"
  />

  <div class="container">
    {#each result as pokemon}
      <div class="container__item">
        <img
          src={`./pokemon/${pokemon.name}.jpg`}
          alt={pokemon.name}
          width="100"
        />
        <p>{pokemon.name}</p>
      </div>
    {/each}
  </div>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    max-width: 240px;
    margin: 0 auto;
    height: 100%;
    text-align: center;
    align-items: center;
  }
  input {
    width: 300px;
    margin-bottom: 15px;
  }
  input:focus {
    outline: none;
  }
  .container {
    display: flex;
    flex-flow: row wrap;
    align-content: space-between;
    justify-content: space-between;
    flex: 1;
    overflow-y: scroll;
    width: 100%;
    max-width: 1500px;
  }
  .container__item {
    width: fit-content;
    height: fit-content;
    display: flex;
    justify-content: center;
    flex-direction: column;
    height: 200px;
  }
  .container__item:hover {
    border: 1px solid black;
    border-radius: 2px;
  }
  .container__item img {
    flex: 0.8;
  }
  .container__item p {
    flex: 0.2;
  }
  ul {
    list-style: none;
  }
  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
