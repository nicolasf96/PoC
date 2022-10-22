<script>

let poks = []
let count = 0
let yes = false

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

  function handleClick(p){
    p.checked = !p.checked
    if(p.checked){
      count++
    }else{
      if(count!=0){
        count--
      }
    }
    console.log(p)
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
          <div class="navbar-item has-dropdown is-hoverable">
            <a class="navbar-link" href="https://bulma.io/documentation/overview/start/">
              Listados
            </a>
            <div class="navbar-dropdown is-boxed">
              <a class="navbar-item" href="https://bulma.io/documentation/overview/start/">
                Listado1
              </a>
              <a class="navbar-item" href="https://bulma.io/documentation/overview/modifiers/">
                Listado2
              </a>
              <a class="navbar-item" href="https://bulma.io/documentation/columns/basics/">
                Listado3
              </a>
            </div>
          </div>
        </div>
    
        <div class="navbar-end">
          <div class="navbar-item">
            Sort
          </div>
        </div>
      </div>
    </nav>
  </div>
</div>


<div class="columns is-centered">
  <div class="column is-10 ">
    {count} of {poks.length} selected ({(count/poks.length)*100}%)
  </div>
</div>

<div class="columns is-centered">
  <div class="column is-10">
    {#each poks as p, i}
      <div class="card pokcard no-shadow">
        <div class="card-header no-shadow">
          {p.name}
          <label class="checkbox">
            <input type="checkbox" class:checked={p.checked} bind:checked={p.checked} on:click|preventDefault={() => handleClick(p)} >
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
    box-shadow: 0 0 0 3px hotpink;
  }
</style>
