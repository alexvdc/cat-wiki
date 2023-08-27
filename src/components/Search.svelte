<script>
  export let data;

  let searchBreed = ""; // Variable pour stocker le texte de recherche entré par l'utilisateur
  let suggestions = [];

  function updateSuggestions() {
    if (searchBreed.trim() === "") {
      suggestions = [];
    } else {
      suggestions = data.filter((breed) =>
        breed.name.toLowerCase().includes(searchBreed.toLowerCase())
      );
    }
  }

  function selectSuggestion(suggestion) {
    searchBreed = suggestion.name;
    suggestions = [];
  }
</script>

<label for="search">
  <input
    class="search"
    type="text"
    placeholder="Search"
    bind:value={searchBreed}
    on:input={updateSuggestions}
  />

  <span class="material-icons">search</span>
  {#if suggestions.length > 0}
    <ul>
      {#each suggestions as suggestion (suggestion.id)}
        <li on:click={() => selectSuggestion(suggestion)}>
          <a href={`/cats/${suggestion.id}`}>{suggestion.name}</a>
        </li>
      {/each}
    </ul>
  {/if}
</label>

<style>
  label {
    position: relative;
    display: flex;
    align-items: center;
    padding: 3.5rem 0;
  }
  input {
    position: relative;
    padding: 1rem 1.5rem;
    border-radius: 2rem;
    border: none;
    outline: none;
    width: 100%;
    font-size: var(--fz-a);
    font-family: var(--ff1);
    color: var(--primary);
  }

  input::placeholder {
    opacity: 1;
  }
  .material-icons {
    position: absolute;
    right: 1rem;
    width: 24px;
    color: var(--primary);
  }

  ul {
    position: absolute;
    padding: 1rem 0.5rem;
    border-radius: 1.5rem;
    top: 8rem;
    /* height: 500px; */
    width: 100%;
    max-height: 220px;
    background-color: var(--white);
    overflow-y: scroll;
  }

  a {
    display: inline-block;
    color: var(--black);
    padding: 1rem 0.5rem;
    font-size: 18px;
    width: 100%;
    border-radius: 0.75rem;
    transition: background-color 0.2s ease-in-out;
  }

  a:hover {
    background-color: var(--gray);
  }

  @media (max-width: 768px) {
    label {
      padding: 1.5rem 0;
    }
  }
</style>
