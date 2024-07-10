<script>
import { onMount } from "svelte";
import { fade } from 'svelte/transition';

let scrollContainer;

let showPresupuestoActual = false;
let showRecaudacionActual = false;

function handlePresupuestoClick() {
    showPresupuestoActual = !showPresupuestoActual;
}

function handleRecaudacionClick() {
    showRecaudacionActual = !showRecaudacionActual;
}

onMount(() => {
    let startX, scrollLeft;

    // Mouse and trackpad scrolling
    scrollContainer.addEventListener("wheel", (e) => {
        if (e.deltaY !== 0) {
            e.preventDefault();
            scrollContainer.scrollLeft += e.deltaY * 5; // Adjust the multiplier as needed
        }
    });

    // Touch scrolling for trackpads
    scrollContainer.addEventListener("touchstart", (e) => {
        startX = e.touches[0].pageX - scrollContainer.offsetLeft;
        scrollLeft = scrollContainer.scrollLeft;
    });

    scrollContainer.addEventListener("touchmove", (e) => {
        e.preventDefault();
        const x = e.touches[0].pageX - scrollContainer.offsetLeft;
        const walk = (x - startX) * 3; // Adjust the multiplier as needed
        scrollContainer.scrollLeft = scrollLeft - walk;
    });
});
</script>

<main>
    <div class="overlay-container">
<section class="sixth_section">
    <h1 id="section_header">FICHA TECNICA</h1>
    <div bind:this={scrollContainer} class="scroll-container">
    <div class="section-content Director">
        <h1 class="technic_head">Dirigida Por</h1>
        <div class="row">
        <h3>Stanley Kubrick</h3>
        <img src="/images/stanley-kubrick.png" alt="Stanley Kubrick" />
        </div>
    </div>

    <div class="section-content Genero">
        <h1>Género</h1>
        <h3>Ciencia Ficción</h3>
        <div class="row">
        <img src="/images/backshot-1.png" alt="backshot-1">
        <img src="/images/backshot-2.png" alt="backshot-2">
        </div>
    </div>

    <div class="section-content Duracion-Año">
        <div class="row">
        <div class="release_year">
            <h1>Año de lanzamiento</h1>
            <h3 class="counter" data-target="1968">1968</h3>
        </div>

        <div class="movie_length">
            <h1>Duración</h1>
            <h3 class="counter" data-target="142" data-suffix=" minutos">142 minutos</h3>
        </div>
        </div>
    </div>

    <div class="section-content Presupuesto">
        <h1>Presupuesto</h1>
        <div class="row">
        <button class="money-button" on:click={handlePresupuestoClick} on:keydown={(e) => (e.key === 'Enter' || e.key === ' ') && handlePresupuestoClick()} aria-label="Show Presupuesto Actual">
            <img src="/images/money-svg.svg" alt="money-svg">
        </button>
        <h3 class="counter" data-target="10" data-suffix="M USD">10 M USD</h3>
        {#if showPresupuestoActual}
            <h3 id="presupuesto_actual" class="counter" data-target="84" data-suffix="M USD (2024)" transition:fade>84 M USD (2024)</h3>
        {/if}
        </div>
    </div>

    <div class="section-content Recaudacion">
        <h1>Recaudación</h1>
        <div class="row">
        <button class="money-button-2" on:click={handleRecaudacionClick} on:keydown={(e) => (e.key === 'Enter' || e.key === ' ') && handleRecaudacionClick()} aria-label="Show Recaudacion Actual">
            <img src="/images/money-svg.svg" alt="money-svg">
        </button>
        <h3 class="counter" data-target="146" data-suffix="M USD">146 M USD</h3>
        {#if showRecaudacionActual}
            <h3 id="recaudacion_actual" class="counter" data-target="1168" data-suffix="M USD (2024)" transition:fade>1168 M USD (2024)</h3>
        {/if}
        </div>
    </div>
    </div>

</section>
</div>
</main>

<style>
.overlay-container {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 50vh;
    background-color: rgb(255, 0, 0); /* Adjust transparency as needed */
    z-index: 1; /* Ensure it overlays other content */
}
#section_header {
    color: aliceblue;
    font-size: 50px;
    text-align: center;
}



.scroll-container {
    display: flex;
    overflow-x: auto;
    scroll-behavior: smooth;
    width: 100%;
    color: aliceblue;
}

.section-content {
    min-width: 70vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 5%;
}

.row {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 20px;
    margin-bottom: 2rem;
}

.technic_head {
    font-size: 80px;
    font-weight: 400;
    margin: 0;
}

h3 {
    font-size: 120px;
    margin: 80px 0;
}

.counter {
    font-size: 120px;
    margin: 0;
}

.money-button,
.money-button-2 {
    cursor: pointer;
    background: none;
    border: none;
    outline: none;
    height: fit-content;
}

#presupuesto_actual,
#recaudacion_actual {
    font-size: 120px;
    margin: 0;
    color: #8fff9a;
    transition: opacity 0.5s ease-in-out;
}
</style>
