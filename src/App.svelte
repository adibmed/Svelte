<script>
  import { onMount } from "svelte";

  let name = "pikachu";
  let src = "./pokemon/abra.jpg";
  let pokemons = {};
  export let user;
  onMount(async () => {
    await fetch("https://pokeapi.co/api/v2/pokemon?limit=1118&offset=0")
      .then((res) => res.json())
      .then((response) => {
        pokemons = response.results;
        console.log("🐹", pokemons);
      });
  });

  function change() {
	  console.log("Change 🐹");
  }

</script>

<main>
  <h1>Hello {user}!</h1>
  <h2>{name}</h2>
  <input bind:value={name} on:input={change} type="text" placeholder="search pokemon" />

  <ul>
    <li><img src={`./pokemon/${name}.jpg`} alt={name} width="200" /></li>
  </ul>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
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
