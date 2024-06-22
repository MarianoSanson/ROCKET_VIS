<script>
import { onMount } from 'svelte';
let bar;
let container;
let waveformimg

const updateBarPosition = () => {
    const containerHeight = container.offsetHeight;
    const scrollPosition = window.scrollY;
    const maxScroll = containerHeight - window.innerHeight;
    const scrollPercent = Math.min(scrollPosition / maxScroll, 1);
    const barPosition = scrollPercent * waveformimg.offsetWidth;

    bar.style.left = `${barPosition}px`;
};

onMount(() => {
    window.addEventListener('scroll', updateBarPosition);
    updateBarPosition(); // Initialize position
});
</script>

<style>
.container {
    position: relative;
    height: 200vh; /* Adjust based on your needs */
}

.waveform {
    position: relative;
    height: 20vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

#waveformimg{
    width: 70vw;
}

#bar {
    position: absolute;
    top: 0;
    height: 100%;
    width: 2px;
    background-color: red;
    transition: left 0.1s ease-out;
}
</style>

<div class="container" bind:this={container}>
<div class="waveform">
    <img src="./images/2001waveform.png" alt='waveform' bind:this={waveformimg} id="waveformimg" />
    <div id="bar" bind:this={bar}></div>
</div>
</div>
