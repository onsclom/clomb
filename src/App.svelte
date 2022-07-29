<script>
  import { time_ranges_to_array } from "svelte/internal";

  // import svelteLogo from './assets/svelte.svg'
  // import Counter from './lib/Counter.svelte'

  let time = new Date();
  time.setMinutes(time.getMinutes() - time.getTimezoneOffset());
  let today = time.toJSON().slice(0, 10);

  let grades = [];
  for (let i = 0; i < 10; i++) {
    grades.push(i);
  }

  let clombs = [];
  let newClimb = false;
  let flashClimb = false;
  let grade;

  function submitClimb() {
    let climb = `${grade} ${newClimb ? "🆕" : ""} ${flashClimb ? "⚡" : ""}`;
    console.log(climb)
    clombs.push(climb);
    newClimb = false;
    flashClimb = false;
    clombs = clombs;
  }
</script>

<main>
  <h1 style="text-align: center;">clomb tracker</h1>

  <div style="text-align: center;">
    <button> &lt; </button>
    <input type="date" value={today} />
    <button disabled> > </button>
  </div>
  <div>
    <div class="inputForm">
      <select bind:value={grade}>
        {#each grades as grade}
          <option value={"V" + grade}>{"V" + grade}</option>
        {/each}
      </select>
      <div>
        <label for="new">new</label>
        <input id="new" type="checkbox" bind:checked={newClimb} />
      </div>
      <div>
        <label for="flash">flash</label>
        <input
          id="flash"
          type="checkbox"
          bind:checked={flashClimb}
          disabled={!newClimb == true}
        />
      </div>
      <button on:click={submitClimb}> add send </button>
    </div>
  </div>
  <div style="text-align: center">
  {#each clombs as clomb}
  <div class="climb">
    <button>X</button><span>{clomb}</span>
  </div>
  {/each}
  </div>
</main>

<style>
  .inputForm {
    text-align: center;
    border: 1px solid black;
    padding: 1rem;
    margin: 1rem;
  }

  .climb {
    margin: .25rem;
  }
</style>
