<script lang="ts">
  import { onMount } from "svelte";

  import Stars from "./lib/Stars.svelte";
  import Cards from "./lib/Cards.svelte";
  import FifthSection from "./lib/FifthSection.svelte";

  import { cardsDataColor, cardsDataNarrative } from "./lib/cardsData.js";
  import { fade } from 'svelte/transition';

  let audio; // Definir la variable de audio

  let scrollContainer;

  let showPresupuestoActual = false;
  let showRecaudacionActual = false;

  function handlePresupuestoClick() {
    showPresupuestoActual = true;
  }

  function handleRecaudacionClick() {
    showRecaudacionActual = true;
  }

  const startCounter = (element, target, suffix) => {
    const duration = 2000; // 2 segundos
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

      scrollContainer.addEventListener("wheel", (e) => {
        if (e.deltaY !== 0) {
          e.preventDefault();
          scrollContainer.scrollLeft += e.deltaY * 5; // Aumenta el multiplicador para más movimiento
        }
      });
    }

    // Observar los elementos que requieren contador
    const elements = document.querySelectorAll(".counter");
    observer = new IntersectionObserver(handleIntersect);

    elements.forEach((element) => {
      observer.observe(element);
    });
  });
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
    <h1 id="section_header">LA NARRACIÓN DE UNA ODISEA ESPACIAL</h1>
    <p style="color: aliceblue; font-size:22px; text-align:center">
      Para el analisis narrativo, decidimos particionar la pelicula en
      segmentos de 5 minutos, y a cada segmento asignarle un momento en el arco
      narrativo:
    </p>
    <div class="narratives_container">
      <div class="narrative">
        <div class="category" style="background-color: #8FFF9A;"></div>
        <h4 style="font-size: 22px; font-weight:400">Introducción</h4>
      </div>

      <div class="narrative">
        <div class="category" style="background-color: #FF7B5E;"></div>
        <h4 style="font-size: 22px; font-weight:400">Acción Creciente</h4>
      </div>

      <div class="narrative">
        <div class="category" style="background-color: #CF1E1E;"></div>
        <h4 style="font-size: 22px; font-weight:400">Climax</h4>
      </div>

      <div class="narrative">
        <div class="category" style="background-color: #FFFBA3;"></div>
        <h4 style="font-size: 22px; font-weight:400">Acción Decreciente</h4>
      </div>

      <div class="narrative">
        <div class="category" style="background-color: #7EFFFF;"></div>
        <h4 style="font-size: 22px; font-weight:400">Resolución</h4>
      </div>
    </div>
    <div class="narrative_analysis">
      <Cards cards={cardsDataNarrative} />
    </div>
  </section>

  <section class="fourth_section">
    <Stars />
    <h1 id="section_header">2001 A TRAVES DE LOS COLORES</h1>
    <p style="color: aliceblue; font-size:22px; text-align:center">
      Nos propusimos analizar el uso del color en las escenas de la
      pelicula para poder visualizar patrones en el uso del color.
    </p>
    <div class="narratives_container">

      <div id="example_card"></div>

      <div class="narrative">
        <div class="category" style="background-color:#CF1E1E; z-index:20"></div>
        <h4 style="font-size: 22px; font-weight:400">Color principal</h4>
      </div>

      <div class="narrative">
        <div class="category" style="background-color: #FFFBA3;"></div>
        <h4 style="font-size: 22px; font-weight:400">Color de acento</h4>
      </div>
    </div>
    <div class="narrative_analysis">
      <Cards cards={cardsDataColor} />
    </div>
  </section>
  <Stars />
  <FifthSection />
  <Stars />

  <section class="sixth_section">
    <h1 id="section_header">FICHA TECNICA</h1>
    <div bind:this={scrollContainer} class="scroll-container" style="color: aliceblue;">
      <div class="Director">
        <h1 class="technic_head" style="font-size: 80px; font-weight:400; margin:0;">Dirigida Por</h1>
        <div class="row" style="gap: 0;">
          <h3 style="font-size: 120px; margin:80px">Stanley Kubrick</h3>
          <img src="/images/stanley-kubrick.png" alt="Stanley Kubrick" />
        </div>
      </div>

      <div class="Genero">
        <h1 style="font-size: 80px; font-weight:400; margin:0;">Género</h1>
        <h3 style="font-size: 120px; margin:80px">Ciencia Ficción</h3>
        <div class="row" style="gap: 20px;">
          <img src="/images/backshot-1.png" alt="backshot-1">
          <img src="/images/backshot-2.png" alt="backshot-2">
        </div>
      </div>

      <div class="Duracion-Año">
        <div class="row">
          <div class="release_year">
            <h1 style="font-size: 80px; font-weight:400; margin:0;">Año de lanzamiento</h1>
            <h3 style="font-size: 120px; margin:50px" data-target="1968" class="counter">1968</h3>
          </div>

          <div class="movie_length">
            <h1 style="font-size: 80px; font-weight:400; margin:0;">Duración</h1>
            <h3 style="font-size: 120px; margin:50px"  data-target="142" data-suffix=" minutos" class="counter">142 minutos</h3>
          </div>
        </div>
      </div>

      <div class="Presupuesto">
        <h1 style="font-size: 80px; font-weight:400; margin:0;">Presupuesto</h1>
        <div class="row" style="align-items: center; height: fit-content; margin-top: 50px; gap: 50px;">
          <button class="money-button" on:click={handlePresupuestoClick} on:keydown={(e) => (e.key === 'Enter' || e.key === ' ') && handlePresupuestoClick()} aria-label="Show Presupuesto Actual">
            <img src="/images/money-svg.svg" alt="money-svg">
          </button>
          <h3 style="font-size: 120px; margin: 0;" data-target="10" data-suffix="M USD" class="counter">10 M USD</h3>
          {#if showPresupuestoActual}
            <h3 id="presupuesto_actual" data-target="84" data-suffix="M USD (2024)" class="counter" transition:fade>84 M USD (2024)</h3>
          {/if}
        </div>
      </div>
      
      <div class="Recaudacion">
        <h1 style="font-size: 80px; font-weight:400; margin:0;">Recaudación</h1>
        <div class="row" style="align-items: center; height: fit-content; margin-top: 50px; gap: 50px;">
          <button class="money-button-2" on:click={handleRecaudacionClick} on:keydown={(e) => (e.key === 'Enter' || e.key === ' ') && handleRecaudacionClick()} aria-label="Show Recaudacion Actual">
            <img src="/images/money-svg.svg" alt="money-svg">
          </button>
          <h3 style="font-size: 120px; margin: 0;" data-target="146" data-suffix="M USD" class="counter">146 M USD</h3>
          {#if showRecaudacionActual}
            <h3 id="recaudacion_actual" data-target="1168" data-suffix="M USD (2024)" class="counter" transition:fade>1168 M USD (2024)</h3>
          {/if}
        </div>
      </div>
    </div>
  </section>

  <section class="seventh_section">
    <img
      src="/images/discovery-one.png"
      alt="nave discovery one"
      style="z-index: 10;"
    />
    <div class="icon_links">
      <a href="https://www.figma.com/proto/ZAGqFBeCUV9Vx9rn6HFtiu/PROYECTOS-WOLODARSKY-%7C-SANSON?node-id=827-4372&t=ZWfEgZFww2kAOlRp-1" class="social_icon" target="_blank">
        <!-- cambiar LINK -->
        <img src="/images/figma-icon.svg" alt="figma-icon" />
      </a>

      <a
        href="https://github.com/MarianoSanson/ROCKET_VIS"
        class="social_icon"
        target="_blank"
      >
        <img src="/images/github-icon.svg" alt="github-icon" />
      </a>
    </div>
    <h3 style="color: aliceblue; font-size:24px; font-weight:400;">Mariano Sanson y Nicolas Wolodarsky</h3>
    <h3 style="color: aliceblue; font-size:24px; font-weight:400;">
      Universidad Torcuato Di Tella | Licenciatura en Tecnología Digital
    </h3>
  </section>
</main>
|

<style>
  @font-face {
    font-family: "Futura";
    src: url("/images/fonts/Futura Medium.ttf") format("truetype");
    font-weight: normal;
    font-style: normal;
  }

  :global(html, body) {
    background: radial-gradient(ellipse at bottom, #1b2735 0%, #090a0f 100%);
    margin: 0;
  }

  * {
    font-family: Futura;
  }

  section {
    /* scroll-snap-align: start; */
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
    height: 80vh;
    width: 21vw;
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
    align-items: center;
    height: fit-content;
    margin-top: 80px;
  }

  #example_card{
    height: 150px;
    width: 30px;
    border-radius: 10px;
    background-color: #CF1E1E;
    border: 2px #FFFBA3 solid;
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

  .sixth_section {
    padding-top: 30px;
    margin: 50px;
  }

  .sixth_section {
    height: 100vh;
  }

  .Director {
    color: aliceblue;
    min-width: 100vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    height: fit-content;
    margin-top: 5%;
  }

  .Genero {
    min-width: 100vw;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .Duracion-Año{
    min-width: 100vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 5%;
  }

  .release_year{
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .movie_length{
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .Presupuesto{
    min-width: 100vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 5%;
  }

  .money-button {
    background: none;
    border: none;
    padding: 0;
    cursor: pointer;
    height: fit-content;
  }

  #presupuesto_actual{
    font-size: 120px;
    margin:0;
    color: #8FFF9A;
    transition: opacity 0.5s ease-in-out; /* Transición suave */
  }

  .Recaudacion{
    min-width: 100vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 5%;
  }

  .money-button-2 {
    background: none;
    border: none;
    padding: 0;
    cursor: pointer;
    height: fit-content;
  }

  #recaudacion_actual{
    font-size: 120px;
    margin:0;
    color: #8FFF9A;
    transition: opacity 0.5s ease-in-out; /* Transición suave */
  }

  .scroll-container {
    display: flex;
    overflow-x: hidden;
    scroll-behavior: smooth;
    width: 100%;
    height: 100vh;
  }

  .row {
    display: flex;
    flex-direction: row;
    align-items: center;
  }

  .seventh_section {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .icon_links {
    display: flex;
    flex-direction: row;
    padding: 25px;
  }

  .social_icon {
    transition: 0.5s;
  }

  a:hover {
    transform: translateY(-10px);
  }
</style>
