<script lang="ts">
  import { onMount } from "svelte";

  import Stars from "./lib/Stars.svelte";
  import Cards from "./lib/Cards.svelte";
  import FifthSection from "./lib/FifthSection.svelte";
  import SixthSection from "./lib/SixthSection.svelte";

  import { cardsDataColor, cardsDataNarrative } from "./lib/cardsData.js";

  let audio; // Definir la variable de audio

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
      segmentos de 5 minutos y a cada segmento asignarle un momento en el arco
      narrativo
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
      pelicula para poder visualizar patrones en el uso del color
    </p>
    <div class="narratives_container">


      <div class="narrative">
        <div class="category" style="background-color:#CF1E1E; z-index:20"></div>
        <h4 style="font-size: 22px; font-weight:400">Color principal</h4>
      </div>

      <div id="example_card"></div>

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

  <SixthSection />

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
      Universidad Torcuato Di Tella | Licenciatura en Tecnología Digital | Visualización de Datos
    </h3>
  </section>
</main>
|

<style>
  *{
    font-family: 'Urbanist';
  }

  :global(html, body) {
    background: radial-gradient(ellipse at bottom, #1b2735 0%, #090a0f 100%);
    margin: 0;
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
    z-index: 10;
    margin: 0;
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
