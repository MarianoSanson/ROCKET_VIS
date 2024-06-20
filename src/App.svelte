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

  const colorIntro = '#8FFF9A';
  const colorAccionCreciente = '#FF7B5E';
  const colorClimax = '#CF1E1E';
  const colorDecreciente= '#FFFBA3';
  const colorResolucion = '#7EFFFF';

  const cardsDataNarrative = [
    { color: colorIntro, stroke:colorIntro, hoverImage: '/images/narrative/narrative2.png' },
    { color: colorIntro, stroke:colorIntro, hoverImage: '/images/narrative/narrative3.png' },
    { color: colorAccionCreciente, stroke:colorAccionCreciente, hoverImage: '/images/narrative/narrative4.png' },
    { color: colorClimax, stroke:colorClimax, hoverImage: '/images/narrative/narrative5.png' },
    { color: colorDecreciente, stroke:colorDecreciente, hoverImage: '/images/narrative/narrative6.png' },
    { color: colorIntro, stroke:colorIntro, hoverImage: '/images/narrative/narrative7.png' },
    { color: colorIntro, stroke:colorIntro, hoverImage: '/images/narrative/narrative8.png' },
    { color: colorIntro, stroke:colorIntro, hoverImage: '/images/narrative/narrative13.png' },
    { color: colorAccionCreciente, stroke:colorAccionCreciente, hoverImage: '/images/narrative/narrative15.png' },
    { color: colorAccionCreciente, stroke:colorAccionCreciente, hoverImage: '/images/narrative/narrative16.png' },
    { color: colorClimax, stroke:colorClimax, hoverImage: '/images/narrative/narrative19.png' },
    { color: colorIntro, stroke:colorIntro, hoverImage: '/images/narrative/narrative21.png' },
    { color: colorIntro, stroke:colorIntro, hoverImage: '/images/narrative/narrative24.png' },
    { color: colorIntro, stroke:colorIntro, hoverImage: '/images/narrative/narrative29.png' },
    { color: colorIntro, stroke:colorIntro, hoverImage: '/images/narrative/narrative32.png' },
    { color: colorIntro, stroke:colorIntro, hoverImage: '/images/narrative/narrative34.png' },
    { color: colorAccionCreciente, stroke:colorAccionCreciente, hoverImage: '/images/narrative/narrative35.png' },
    { color: colorAccionCreciente, stroke:colorAccionCreciente, hoverImage: '/images/narrative/narrative37.png' },
    { color: colorClimax, stroke:colorClimax, hoverImage: '/images/narrative/narrative48.png' },
    { color: colorClimax, stroke:colorClimax, hoverImage: '/images/narrative/narrative43.png' },
    { color: colorDecreciente, stroke:colorDecreciente, hoverImage: '/images/narrative/narrative45.png' },
    { color: colorDecreciente, stroke:colorDecreciente, hoverImage: '/images/narrative/narrative49.png' },
    { color: colorResolucion, stroke:colorResolucion, hoverImage: '/images/narrative/narrative53.png' },
    { color: colorIntro, stroke:colorIntro, hoverImage: '/images/narrative/narrative57.png' },
    { color: colorIntro, stroke:colorIntro, hoverImage: '/images/narrative/narrative58.png' },
    { color: colorIntro, stroke:colorIntro, hoverImage: '/images/narrative/narrative59.png' },
    { color: colorAccionCreciente, stroke:colorAccionCreciente, hoverImage: '/images/narrative/narrative67.png' },
    { color: colorAccionCreciente, stroke:colorAccionCreciente, hoverImage: '/images/narrative/narrative69.png' },
    { color: colorClimax, stroke:colorClimax, hoverImage: '/images/narrative/narrative83.png' },
    { color: colorResolucion, stroke:colorResolucion, hoverImage: '/images/narrative/narrative89.png' },
  ];

  const cardsDataColor = [
    { color: '#3A3328', stroke:'#EAE2DC', hoverImage: '/images/narrative/narrative2.png' },
    { color: '#81624F', stroke:'#040807', hoverImage: '/images/narrative/narrative3.png' },
    { color: '#E6D6C0', stroke:'#C5B97B', hoverImage: '/images/narrative/narrative4.png' },
    { color: '#B29276', stroke:'#060606', hoverImage: '/images/narrative/narrative5.png' },
    { color: '#77849B', stroke:'#E3BD8E', hoverImage: '/images/narrative/narrative6.png' },
    { color: '#030506', stroke:'#3C3B3F', hoverImage: '/images/narrative/narrative7.png' },
    { color: '#BECCC8', stroke:'#961136', hoverImage: '/images/narrative/narrative8.png' },
    { color: '#7B9AA5', stroke:'#040404', hoverImage: '/images/narrative/narrative13.png' },
    { color: '#F8F6F8', stroke:'#3D221F', hoverImage: '/images/narrative/narrative15.png' },
    { color: '#2C6C94', stroke:'#61140E', hoverImage: '/images/narrative/narrative16.png' },
    { color: '#211818', stroke:'#FDEBE1', hoverImage: '/images/narrative/narrative19.png' },
    { color: '#020404', stroke:'#A6A3A5', hoverImage: '/images/narrative/narrative21.png' },
    { color: '#BBBDBE', stroke:'#7396B7', hoverImage: '/images/narrative/narrative24.png' },
    { color: '#161B22', stroke:'#B57AB7', hoverImage: '/images/narrative/narrative29.png' },
    { color: '#252F40', stroke:'#B57AB7', hoverImage: '/images/narrative/narrative32.png' },
    { color: '#BBB6BC', stroke:'#911913', hoverImage: '/images/narrative/narrative34.png' },
    { color: '#341821', stroke:'#BF2517', hoverImage: '/images/narrative/narrative35.png' },
    { color: '#3E070C', stroke:'#90674F', hoverImage: '/images/narrative/narrative37.png' },
    { color: '#BF1828', stroke:'#060000', hoverImage: '/images/narrative/narrative48.png' },
    { color: '#020300', stroke:'#DAA451', hoverImage: '/images/narrative/narrative43.png' },
    { color: '#3D434E', stroke:'#D49F66', hoverImage: '/images/narrative/narrative45.png' },
    { color: '#AA1B13', stroke:'#AA1B13', hoverImage: '/images/narrative/narrative49.png' },
    { color: '#710A07', stroke:'#508374', hoverImage: '/images/narrative/narrative53.png' },
    { color: '#212D35', stroke:'#A9AEBE', hoverImage: '/images/narrative/narrative57.png' },
    { color: '#C198AF', stroke:'#C79858', hoverImage: '/images/narrative/narrative58.png' },
    { color: '#2D6463', stroke:'#FAE3B0', hoverImage: '/images/narrative/narrative59.png' },
    { color: '#63756F', stroke:'#4B4E21', hoverImage: '/images/narrative/narrative67.png' },
    { color: '#77514F', stroke:'#E6404E', hoverImage: '/images/narrative/narrative69.png' },
    { color: '#A8B6BF', stroke:'#28282A', hoverImage: '/images/narrative/narrative83.png' },
    { color: '#CED5E4', stroke:'#C1CEE4', hoverImage: '/images/narrative/narrative89.png' },
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
      Para el analisis narrativo de la pelicula, decidimos particionarla en segmentod de
      5 minutos, y a cada segmento asignarle un momento en el arco narrativo:
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
      <Cards cards={cardsDataNarrative}/>
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
      <Cards cards={cardsDataColor}/>
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
