# Poke-ball-Randomizer-
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Pokéball Randomizer (Shake Effect)</title>
  <style>
    body{
      margin:0;
      font-family:Arial, sans-serif;
      background:linear-gradient(180deg,#081124 0%, #071923 60%);
      color:#e6eef8;
      display:flex;
      justify-content:center;
      align-items:center;
      min-height:100vh;
    }
    .container{
      text-align:center;
      max-width:600px;
    }
    h1{color:#ffcb05;}
    .balls{
      display:flex;
      justify-content:center;
      gap:20px;
      margin:20px 0;
    }
    .ball{
      width:100px;
      height:100px;
      border-radius:50%;
      background:linear-gradient(red 50%, white 50%);
      border:5px solid black;
      position:relative;
      cursor:pointer;
      transition:transform 0.2s;
    }
    .ball::before{
      content:"";
      position:absolute;
      top:45%;
      left:50%;
      transform:translate(-50%,-50%);
      width:30px;
      height:30px;
      background:white;
      border:5px solid black;
      border-radius:50%;
    }
    .pokemon{
      margin-top:20px;
      display:none;
      animation: fadeIn 0.5s ease forwards;
    }
    .pokemon img{width:150px;}

    @keyframes fadeIn{from{opacity:0}to{opacity:1}}

    /* Shake animation */
    @keyframes shake {
      0% { transform: rotate(0deg); }
      20% { transform: rotate(15deg); }
      40% { transform: rotate(-15deg); }
      60% { transform: rotate(10deg); }
      80% { transform: rotate(-10deg); }
      100% { transform: rotate(0deg); }
    }
    .shaking {
      animation: shake 0.8s;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Pick a Pokéball</h1>
    <p>Click a ball to reveal a random Pokémon!</p>

    <div class="balls">
      <div class="ball" data-ball="1" style="background:linear-gradient(red 50%, white 50%)"></div>
      <div class="ball" data-ball="2" style="background:linear-gradient(blue 50%, white 50%)"></div>
      <div class="ball" data-ball="3" style="background:linear-gradient(black 50%, yellow 50%)"></div>
    </div>

    <div class="pokemon" id="pokemon">
      <img id="pkImg" src="" alt="Pokemon">
      <h2 id="pkName"></h2>
      <p id="pkType"></p>
    </div>
  </div>

  <script>
    const POKEMON = [
      {id:25,name:'Pikachu',type:'Electric'},
      {id:1,name:'Bulbasaur',type:'Grass/Poison'},
      {id:4,name:'Charmander',type:'Fire'},
      {id:7,name:'Squirtle',type:'Water'},
      {id:39,name:'Jigglypuff',type:'Fairy/Normal'},
      {id:52,name:'Meowth',type:'Normal'},
      {id:131,name:'Lapras',type:'Water/Ice'},
      {id:149,name:'Dragonite',type:'Dragon/Flying'},
      {id:150,name:'Mewtwo',type:'Psychic'}
    ];

    const balls = document.querySelectorAll('.ball');
    const pokemonDiv = document.getElementById('pokemon');
    const pkImg = document.getElementById('pkImg');
    const pkName = document.getElementById('pkName');
    const pkType = document.getElementById('pkType');

    function randomPokemon(){
      return POKEMON[Math.floor(Math.random()*POKEMON.length)];
    }

    balls.forEach(ball=>{
      ball.addEventListener('click',()=>{
        // Shake effect
        ball.classList.add('shaking');
        setTimeout(()=>{
          ball.classList.remove('shaking');
          const pick = randomPokemon();
          pkImg.src = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/${pick.id}.png`;
          pkImg.alt = pick.name;
          pkName.textContent = pick.name;
          pkType.textContent = `Type: ${pick.type}`;
          pokemonDiv.style.display = 'block';
        }, 800);
      });
    });
  </script>
</body>
</html>
