<script>
    export let cards = [];
</script>

<style>
    .cards {
        height: fit-content;
        display: flex;
        margin-top: 100px;
        gap: 5px;
    }

    .cards .card {
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        text-align: center;
        height: 150px;
        width: 30px;
        border-radius: 10px;
        color: white;
        transition: 400ms;
    }

    .cards .card:hover {
        width: 330px;
        background-size: cover;
        background-position: center;
    }

    .cards:hover > .card:not(:hover) {
        filter: blur(10px);
        transform: scale(0.9, 0.9);
    }
</style>

<div class="cards">
    {#each cards as { color, hoverImage }}
        <div class="card" style="background-color: {color}; background-image: url({hoverImage})"></div>
    {/each}
</div>