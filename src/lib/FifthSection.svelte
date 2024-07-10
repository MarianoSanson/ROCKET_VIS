<script>
    import { onMount } from 'svelte';

    let bar;
    let waveformSection;
    let waveformimg;
    let sceneImage;
    let scene = 1;

    const handleScroll = () => {
    const sectionTop = waveformSection.getBoundingClientRect().top + window.scrollY + 3;
    const sectionHeight = waveformSection.offsetHeight;
    const scrollTop = window.scrollY;
    const sectionScrollTop = scrollTop - sectionTop;
    const maxScroll = sectionHeight - window.innerHeight;
    const scrollPercentage = Math.min(Math.max(sectionScrollTop / maxScroll, 0), 1);

    // Calculate the bar's position based on the section scroll percentage
    const maxScrollRange = waveformimg.clientWidth; // Use the width of the image
    const barPosition = (scrollPercentage * maxScrollRange) + 263;

    // Update the scene based on scroll percentage
    scene = Math.floor(scrollPercentage*170) + 1; // Assuming you have 1000 images
    sceneImage.src = `/images/scroly/${scene}.png`;

    bar.style.left = `${barPosition}px`;
    };

    onMount(() => {
        window.addEventListener('scroll', handleScroll);
        return () => {
        window.removeEventListener('scroll', handleScroll);
        };
    });
    </script>
    
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
    #section_header {
        color: aliceblue;
        font-size: 50px;
        text-align: center;
    }
    #escena{
        z-index: 10;
        height: 50vh;
        border-radius: 3vh; 
    
    }
    .waveform {
        position: relative;
        height: 20vh;
        display: flex;
        justify-content: center;
        align-items: start;
    }
    
    #waveformimg {
        width: 65vw;
    }
    
    #bar {
        position: absolute;
        top: 0;
        height: 14.6vh;
        width: 2px;
        background-color: orange;
        transition: left 0.1s ease-out;
        z-index: 1;
    }
    
    .fifth_section {
        height: 1000vh;
        padding-top: 30px;
        margin: 50px;
        position: relative;
    }
    
    .stickyContainer {
        position: sticky;
        top: 5vh;
        height: 100vh;
    }
    
    .scene{
        height: 50vh;
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 200000;
    }
    
    
    </style>
    
    <section class="fifth_section" bind:this={waveformSection}>
    <div class="stickyContainer">
        <h1 id="section_header">DESCOMPOSICION DEL AUDIO</h1>
        <p style="color: aliceblue; font-size: 21px; text-align: center;">
        Nos propusimos analizar cómo el uso del color en las escenas de la
        pelicula se relaciona con lo que estas buscan transmitir.<br />A raiz de
        esto llegamos a la siguiente clasificacion:
        </p>
        <div class="waveform">
            <img src="./images/2001waveform.png" alt="waveform" bind:this={waveformimg} id="waveformimg" />
            <div id="bar" bind:this={bar}></div>
        </div>
        <div class="scene">
            <img bind:this={sceneImage} alt="Scene" id="escena" />
        </div>
    </div>
    </section>
    