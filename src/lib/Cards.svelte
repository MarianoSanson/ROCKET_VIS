<script>
export let cards = [];
</script>

<style>
.cards {
    height: fit-content;
    display: flex;
    margin-top: 100px;
    gap: 5px;
    z-index: 10;
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
    color: white solid;
    transition: 400ms;
    background-size: cover;
    background-position: center;
    border: 2px solid;
}

.cards .card:hover {
    width: 330px;
}

.cards .card:hover img {
    display: block;
}

.cards:hover > .card:not(:hover) {
    filter: blur(10px);
    transform: scale(0.9, 0.9);
}

.card img {
    display: none;
    width: 100%;
    height: 100%;
    border-radius: 10px;
}
</style>

<div class="cards">
{#each cards as { color, hoverImage, stroke }}
    <div class="card" style="background-color: {color}; border-color: {stroke}">
    <img src={hoverImage} alt="hover images" />
    </div>
{/each}
</div>