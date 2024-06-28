<script>
    import Icon from "@iconify/svelte";

    function toggleFullScreen() {
        if (document.fullscreenElement) {
            document.exitFullscreen();
            return;
        }
        document.body.requestFullscreen();
    }

    export let showRest = false;
</script>

<main>
    <div class="bar">
        {#if showRest}
            <div on:click={toggleFullScreen}>
                <Icon icon="solar:full-screen-bold"></Icon>
            </div>
        {/if}
        <div
            on:click={() => {
                showRest = !showRest;
            }}
        >
            <Icon icon="solar:settings-bold"></Icon>
        </div>
    </div>
</main>

<style>
    main {
        width: 100%;
        display: flex;
    }

    .bar:hover {
        opacity: 1;
    }

    .bar {
        opacity: 0;
        display: flex;
        margin-left: auto;
        padding: 0.2rem;
        gap: 0.2rem;
        background-color: #f4f4f4;
        border-radius: 0.8rem;
        margin-top: 0.4rem;
        transition: opacity 0.234s;
    }

    .bar > div {
        display: flex;
        aspect-ratio: 1;
        height: 2rem;
        cursor: pointer;
    }

    .bar > div > :global(*) {
        margin: auto;
    }

    @media (prefers-color-scheme: dark) {
        .bar {
            background-color: #141414;
        }
    }
</style>
