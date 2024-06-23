<script>
import { onMount } from 'svelte';
let bar;
let container;
let waveformimg;

const startPosition = -7000; // Change to your desired start position
const endPosition = 6000; // Change to your desired end position

    const handleScroll = () => {
        const scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
        const scrollHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight;
        const scrollPercentage = (scrollTop / scrollHeight);

        // Calculate the bar's position based on start and end positions
        const maxScrollRange = endPosition - startPosition;
        const barPosition = startPosition + (scrollPercentage * maxScrollRange);

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
    height: 100vh;
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
