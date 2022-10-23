<script>

let poks = []
let count = 0
let progress = 1;

const loadData = async () => {
    const res = await fetch(
      "https://pokeapi.co/api/v2/pokemon?limit=150&offset=0"
    );
    const data = await res.json();
    poks = data.results;
    poks.forEach(p => {
      p.checked = false;
    });
  };
  loadData();

  function calculateProgress(){
    progress = (count/poks.length)*300
  }

  function handleClick(p){
    p.checked = !p.checked
    if(p.checked){
      count++
    }else{
      if(count!=0){
        count--
      }
    }
    calculateProgress()

  }
  
  
</script>

<main>

<div class="columns is-centered navcolor">
  <div class="column is-10">

    <nav class="navbar is-transparent inherit">
      <div class="navbar-brand">
        <a class="navbar-item poctitle" href="google.com">
          PoC Svelte
        </a>
        <div class="navbar-burger" data-target="navbarExampleTransparentExample">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
    
      <div id="navbarExampleTransparentExample" class="navbar-menu">
        <div class="navbar-start">
          
        </div>
    
        <div class="navbar-end">
          <div class="navbar-item">
            <!-- ACA VA ALGO -->
          </div>
        </div>
      </div>
    </nav>
  </div>
</div>


<div class="columns is-centered">
  <div class="column is-7 ">
    {count} of {poks.length} selected
    <div class="bar">
      <div class="progress" style="--progress: {progress}px">
      </div>
    </div>
    ({Math.round((count/poks.length)*100)}%)
  </div>
  <div class="column is-3">
    <button class="button is-small is-info f-right" >Sort</button>
  </div>
</div>

<div class="columns is-centered">
  <div class="column is-10">
    {#each poks as p, i}
      <div class="card pokcard no-shadow" class:checked="{p.checked === true}">
        <div class="card-header no-shadow">
          {p.name}

          <label class="checkbox">
            <input type="checkbox" bind:checked={p.checked} on:click={() => handleClick(p)} >
          </label>
        </div>
        <div class="card-image">
          <img width=80px height=80px src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/{i+1}.png" alt="">
        </div>
      </div>
    {/each}
  </div>
</div>

</main>

<style>

  .pokcard{
    display: inline-block;
    margin: 5px;
    padding: 6px 10px 20px 10px;
    height: 110px;
    width: 110px;
    border: 1px solid rgba(0,0,0,0.1);
    border-radius: 7px;
    font-size: 13px;
    font-weight: 600;
  }

  .card-header .checkbox{
    margin-left: 5px;
  }

  .no-shadow{
    box-shadow: none;
  }

  .poctitle{
    font-size: 28px;
    font-weight: 700;
  }

  .navcolor{
    background-color: blue;
  }

  .inherit{
    background-color: inherit;
  }

  .navbar-item{
    color: white;
  }
  .card-image img{
    margin: auto;
  }

  .checked{
    box-shadow: 0 0 0 2px green;
  }

  div.bar{
    display: inline-block;
    margin-left: 20px;
    padding: 3px;
    height: 25px;
    width: 306px;
    border: 1px solid gray;
    position: relative;
  }
  div.progress{
    border-radius: 0;
    height: 18px;
    background-color: green;
    width: var(--progress);
  }

  .f-right{
    float: right;
  }
</style>
