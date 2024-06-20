<script>

  import { onMount } from "svelte";

  import Stars from "./lib/Stars.svelte";
  import Cards from "./lib/Cards.svelte";

  let audio; // Definir la variable de audio

  const startCounter = (element, target, suffix) => {
    const duration = 3500; // 3.5 segundos
    let counter = 0;
    const startTime = Date.now();

    const updateCounter = () => {
      const currentTime = Date.now();
      const elapsedTime = currentTime - startTime;
      if (elapsedTime < duration) {
        counter = Math.floor((target / duration) * elapsedTime);
        element.textContent = counter.toLocaleString() + suffix;
        requestAnimationFrame(updateCounter);
      } else {
        element.textContent = target.toLocaleString() + suffix;
      }
    };

    updateCounter();
  };

  const handleIntersect = (entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        const target = parseInt(entry.target.dataset.target, 10);
        const suffix = entry.target.dataset.suffix || "";
        startCounter(entry.target, target, suffix);
        observer.unobserve(entry.target);
      }
    });
  };

  let observer;

  onMount(() => {
    // Obtener el elemento de audio del DOM
    audio = document.querySelector("audio");

    // Reproducir el audio al cargar la página
    if (audio) {
      audio.play().catch((error) => {
        console.log("Error al reproducir el audio:", error);
      });
    }

    // Observar los elementos que requieren contador
    const elements = document.querySelectorAll(".counter");
    observer = new IntersectionObserver(handleIntersect);

    elements.forEach((element) => {
      observer.observe(element);
    });
  });


  const cardsData = [
    { color: '#8FFF9A', hoverImage: '/images/image1.png' },
    { color: '#8FFF9A', hoverImage: '/images/image2.png' },
    { color: '#FF7B5E', hoverImage: '/images/image3.png' },
    { color: '#CF1E1E', hoverImage: '/images/image4.png' },
    { color: '#FFFBA3', hoverImage: '/images/image5.png' },
    { color: '#8FFF9A', hoverImage: '/images/image6.png' },
    // Add more cards as needed
  ];
</script>


<main>
  <Stars />
  <audio bind:this={audio} src="/audio/2001-AUDIO.mp3" preload="auto"></audio>
  <section class="first_section">
    <div class="planets">
      <img src="/images/moon.png" alt="Moon" class="moon" />
      <img src="/images/earth.png" alt="Earth" class="earth" />
      <img src="/images/sun.png" alt="Sun" class="sun" />
      <div class="typewriter">
        <h1 style="color: aliceblue; font-size:70px">
          2001: UNA ODISEA DEL ESPACIO
        </h1>
      </div>
    </div>
  </section>

  <section class="second_section">
    <div class="introduction">
      <img
        src="/images/portada-2001.png"
        alt="portada pelicula"
        id="movie_image"
      />

      <p id="summary">
        "2001: Una odisea del espacio" es una película de ciencia ficción de
        1968 dirigida por Stanley Kubrick, basada en una historia de Arthur C.
        Clarke. La película se centra en un misterioso monolito que parece
        influir en la evolución humana desde la prehistoria hasta el futuro. En
        el año 2001, una misión espacial hacia Júpiter a bordo de la nave
        Discovery One enfrenta desafíos inesperados. La película explora temas
        profundos sobre la inteligencia, la tecnología y el destino de la
        humanidad, presentando una experiencia cinematográfica única y
        filosófica.
      </p>
    </div>
  </section>

  <section class="third_section">
    <h1 id="section_header">ANÁLISIS NARRATIVO</h1>
    <p style="color: aliceblue; font-size:21px; text-align:center">
      Dividimos la narrativa de la pelicula en cinco categorias diferentes y,
      además, decidimos asignarle a cada frame una duración de 5 minutos
    </p>
    <div class="narratives_container">
      <div class="narrative">
        <div class="category" style="background-color: #8FFF9A;"></div>
        <h4>Introducción</h4>
      </div>

      <div class="narrative">
        <div class="category" style="background-color: #FF7B5E;"></div>
        <h4>Acción Creciente</h4>
      </div>

      <div class="narrative">
        <div class="category" style="background-color: #CF1E1E;"></div>
        <h4>Climax</h4>
      </div>

      <div class="narrative">
        <div class="category" style="background-color: #FFFBA3;"></div>
        <h4>Acción Decreciente</h4>
      </div>

      <div class="narrative">
        <div class="category" style="background-color: #7EFFFF;"></div>
        <h4>Resolución</h4>
      </div>
    </div>
    <div class="narrative_analysis">
      <Cards cards={cardsData}/>
    </div>
  </section>

  <section class="fourth_section">
    <Stars />
    <h1 id="section_header">COLOR</h1>
    <p style="color: aliceblue; font-size:21px; text-align:center">
      Nos propusimos analizar cómo el uso del color en las escenas de la
      pelicula se relaciona con lo que estas buscan transmitir.<br />A raiz de
      esto llegamos a la siguiente clasificacion:
    </p>
    <div class="narratives_container">
      <div class="narrative">
        <div class="category" style="background-color: #F18200;"></div>
        <h4>Cálido Saturado</h4>
      </div>

      <div class="narrative">
        <div class="category" style="background-color: #A97C48;"></div>
        <h4>Cálido Desaturado</h4>
      </div>

      <div class="narrative">
        <div class="category" style="background-color: #9DF3FF;"></div>
        <h4>Frio Saturado</h4>
      </div>

      <div class="narrative">
        <div class="category" style="background-color: #CECECE;"></div>
        <h4>Frio Desaturado</h4>
      </div>
    </div>
    <div class="narrative_analysis">
      <div class="cards">
        <div class="card" style="background-color: #F18200;"></div>
        <div class="card neutro" style="background-color: #CECECE;"></div>
        <div class="card desarrollo" style="background-color: #A97C48;"></div>
        <div class="card tension" style="background-color: #A97C48;"></div>
        <div class="card neutro" style="background-color: #A97C48;"></div>
        <div class="card desarrollo" style="background-color: #CECECE;"></div>
        <div class="card tension" style="background-color: #9DF3FF;"></div>
        <div class="card neutro" style="background-color: #F18200;"></div>
        <div class="card desarrollo" style="background-color: #CECECE;"></div>
        <div class="card tension" style="background-color: #9DF3FF;"></div>
        <div class="card neutro" style="background-color: #F18200;"></div>
        <div class="card desarrollo" style="background-color: #CECECE;"></div>
        <div class="card tension" style="background-color: #CECECE;"></div>
        <div class="card tension" style="background-color: #CECECE;"></div>
        <div class="card neutro" style="background-color: #CECECE;"></div>
        <div class="card tension" style="background-color: #CECECE;"></div>
        <div class="card tension" style="background-color: #F18200;"></div>
        <div class="card neutro" style="background-color: #F18200;"></div>
        <div class="card tension" style="background-color: #9DF3FF;"></div>
        <div class="card tension" style="background-color: #CECECE;"></div>
        <div class="card neutro" style="background-color: #F18200;"></div>
        <div class="card tension" style="background-color: #F18200;"></div>
        <div class="card tension" style="background-color: #F18200;"></div>
        <div class="card neutro" style="background-color: #CECECE;"></div>
        <div class="card tension" style="background-color: #F18200;"></div>
        <div class="card tension" style="background-color: #F18200;"></div>
        <div class="card tension" style="background-color: #9DF3FF;"></div>
        <div class="card neutro" style="background-color: #9DF3FF;"></div>
        <div class="card tension" style="background-color: #9DF3FF;"></div>
        <div class="card tension" style="background-color: #CECECE;"></div>
      </div>
    </div>
  </section>

  <section class="fifth_section">
    <h1 id="section_header">DESCOMPOSICION DEL AUDIO</h1>
  </section>

  <div id="stars"></div>
  <div id="stars2"></div>
  <div id="stars3"></div>

  <section class="sixth_section">
    <h1 id="section_header">FICHA TECNICA</h1>
    <div class="row">
      <div class="technic_container">
        <h3 id="technic_head">Dirigida por</h3>
        <h3 id="technic_text">Stanley Kubrick</h3>
      </div>

      <div>
        <h3 id="technic_head">Género</h3>
        <h3 id="technic_text">Ciencia Ficción</h3>
      </div>

      <div>
        <h3 id="technic_head">Duración</h3>
        <h3
          id="technic_text"
          data-target="142"
          data-suffix=" minutos"
          class="counter"
        >
          142 minutos
        </h3>
      </div>
    </div>

    <div class="row">
      <div>
        <h3 id="technic_head">Año de lanzamiento</h3>
        <h3 id="technic_text" data-target="1968">1968</h3>
      </div>

      <div>
        <h3 id="technic_head">Presupuesto</h3>
        <h3
          id="technic_text"
          data-target="10"
          data-suffix="M USD"
          class="counter"
        >
          10M USD
        </h3>
        <h3
          id="technic_text"
          data-target="84"
          data-suffix="M USD (2024)"
          class="counter"
          style="font-weight: bold;"
        >
          84M USD (2024)
        </h3>
      </div>

      <div>
        <h3 id="technic_head">Recaudación</h3>
        <h3
          id="technic_text"
          data-target="146"
          data-suffix="M USD"
          class="counter"
        >
          146M USD
        </h3>
        <h3
          id="technic_text"
          data-target="1168"
          data-suffix="M USD (2024)"
          class="counter"
          style="font-weight: bold;"
        >
          1168M USD (2024)
        </h3>
      </div>
    </div>
  </section>
  
  <section class="seventh_section">
    <h1 style="color: aliceblue; font-size: 300px; margin: 0">GRACIAS!</h1>
    <div class="icon_links">
      <a href="" class="social_icon">
          <img src="/images/figma-icon.svg" alt="figma-icon">
      </a>

      <a href="https://github.com/MarianoSanson/ROCKET_VIS" class="social_icon" target="_blank">
        <img src="/images/github-icon.svg" alt="github-icon">
      </a>
    </div>
    <h3 style="color: aliceblue;">Mariano Sanson y Nicolas Wolodarsky</h3>
    <h3 style="color: aliceblue;">Universidad Torcuato Di Tella | Licenciatura en Tecnología Digital</h3>
  </section>
</main>

<style>
  @font-face {
    font-family: "Futura";
    src: url("public\images\fonts\Futura Medium.ttf") format("truetype");
    font-weight: normal;
    font-style: normal;
  }

  :global(html, body) {
    background: radial-gradient(ellipse at bottom, #1b2735 0%, #090a0f 100%);
    margin: 0;
  }

  audio {
    display: none;
  }

  * {
    font-family: Futura;
  }

  section {
    scroll-snap-align: start;
    height: 100vh;
  }

  h4 {
    color: aliceblue;
    font-weight: 800;
  }

  .planets {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .planets img {
    position: absolute;
    transition: transform 0.3s ease;
  }

  .moon,
  .earth,
  .sun {
    position: absolute;
    transition: top 0.3s ease;
  }

  .moon {
    z-index: 3;
    animation: moonTransition 16s forwards;
  }

  .earth {
    z-index: 2;
    animation: earthTransition 16s forwards;
  }

  .sun {
    z-index: 1;
    animation: sunTransition 16s forwards;
  }

  @keyframes sunTransition {
    0% {
      transform: translateY(0);
    }
    100% {
      transform: translateY(-65%);
    }
  }

  @keyframes moonTransition {
    0% {
      transform: translateY(0);
    }
    100% {
      transform: translateY(20%);
    }
  }

  @keyframes earthTransition {
    0% {
      transform: translateY(0);
    }
    100% {
      transform: translateY(-100%);
    }
  }

  .typewriter {
    z-index: 5;
    margin-top: 200px;
  }

  .typewriter h1 {
    overflow: hidden; /* Ensures the content is not revealed until the animation */
    border-right: 0.15em solid orange; /* The typwriter cursor */
    white-space: nowrap; /* Keeps the content on a single line */
    margin: 0 auto; /* Gives that scrolling effect as the typing happens */
    letter-spacing: 0.15em; /* Adjust as needed */
    animation:
      typing 7.5s steps(40, end),
      blink-caret 0.75s step-end infinite;
  }

  /* The typing effect */
  @keyframes typing {
    0% {
      width: 0;
    }
    100% {
      width: 100%;
    }
  }

  /* The typewriter cursor effect */
  @keyframes blink-caret {
    from,
    to {
      border-color: transparent;
    }
    50% {
      border-color: orange;
    }
  }

  .introduction {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    gap: 10%;
    height: 100vh;
  }

  #summary {
    color: aliceblue;
    font-size: 27.7px;
    text-align: left;
    margin: 0;
    height: 583.675px;
    width: 394.062px;
  }

  #movie_image {
    height: 80vh;
  }

  .third_section {
    padding-top: 50px;
    margin: 50px;
  }

  #section_header {
    color: aliceblue;
    font-size: 50px;
    text-align: center;
  }

  .narratives_container {
    display: flex;
    flex-direction: row;
    gap: 100px;
    justify-content: center;
    margin-top: 80px;
  }

  .narrative {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .category {
    width: 40px;
    height: 40px;
    border-radius: 4px;
  }

  .narrative_analysis {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .fourth_section {
    padding-top: 30px;
    margin: 50px;
  }

  .fifth_section {
    padding-top: 30px;
    margin: 50px;
  }

  .sixth_section {
    padding-top: 30px;
    margin: 50px;
  }

  .row {
      display: flex;
      flex-direction: row;
      justify-content: space-around;
      padding-bottom: 100px;
  }

  .technic_container {
      display: flex;
      flex-direction: column;
      justify-items: left;
  }

  #technic_head {
      font-size: 1.5em;
      color: aliceblue;
      margin: 10px;
      font-weight: 500;
  }

  #technic_text {
      font-size: 2.5em;
      color: aliceblue;
      margin: 10px;
      font-weight: 500;
  }

  .seventh_section{
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .icon_links{
    display: flex;
    flex-direction: row;
    padding: 25px;
  }

  .social_icon{
    transition: 0.5s;
  }

  a:hover{
    transform: translateY(-10px);
  }
</style>
