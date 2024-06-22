<script>
import { onMount } from 'svelte';

let scrollWatcher;

const handleScroll = () => {
    const scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
    const scrollHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight;
    const scrollPercentage = (scrollTop / scrollHeight) * 100;
    scrollWatcher.style.transform = `scaleX(${scrollPercentage / 100})`;
};

onMount(() => {
    scrollWatcher = document.querySelector('.scroll-watcher');
    window.addEventListener('scroll', handleScroll);
    
    return () => {
    window.removeEventListener('scroll', handleScroll);
    };
});
</script>

<style>
@keyframes scrolling {
    to { transform: translateX(-50%); }
}

.scroll-watcher {
    height: 10px;
    position: fixed;
    top: 0;
    z-index: 1000;
    background-color: lime;
    width: 100%;
    transform: scaleX(0);
    transform-origin: left;
}
</style>

<div class="scroll-watcher"></div>
