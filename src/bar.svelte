<script>
    import Icon from "@iconify/svelte";

    function toggleFullScreen() {
        if (document.fullscreenElement) {
            document.exitFullscreen();
            return;
        }
        document.body.requestFullscreen();
    }

    function display() {
        if (showRest) {
            return;
        }
        showRest = true;
    }

    function hide() {
        showRest = false;
    }

    export let showRest = false;
</script>

<main>
    <div class="bar" on:mouseover={display} on:mouseleave={hide}>
        {#if showRest}
            <div class="rest">
                <div on:click={toggleFullScreen}>
                    <Icon icon="solar:full-screen-bold"></Icon>
                </div>
            </div>
        {/if}
        <div>
            <Icon icon="solar:settings-bold"></Icon>
        </div>
    </div>
</main>

<style>
    main {
        width: 100%;
        display: flex;
    }

    @keyframes ani-bar-in {
        from {
            opacity: 0;
            transform: translateY(-0.8rem) scale(0.95);
        }
        to {
            opacity: 1;
            transform: none;
        }
    }

    @keyframes ani-bar-out {
        from {
            opacity: 1;
            transform: none;
        }
        to {
            opacity: 0;
            transform: translateY(-0.8rem) scale(0.95);
        }
    }

    @keyframes ani-elements-in {
        from {
            opacity: 0;
            transform: translateX(-0.8rem);
        }
        70% {
            opacity: 1;
        }
        to {
            opacity: 1;
            transform: none;
        }
    }

    .bar:hover {
        animation-name: ani-bar-in;
        animation-duration: 0.235s;
        animation-fill-mode: forwards;
    }

    .bar {
        opacity: 0;
        display: flex;
        margin-left: auto;
        padding: 0.2rem;
        gap: 0.2rem;
        background-color: #f7f7f7;
        border-radius: 0.8rem;
        margin-top: 0.4rem;
        animation-name: ani-bar-out;
        animation-duration: 0.235s;
        animation-fill-mode: forwards;
    }

    .bar:hover > div > div {
        animation-name: ani-elements-in;
        animation-duration: 0.355s;
        animation-fill-mode: forwards;
    }

    .bar > div,
    .bar > div > div {
        display: flex;
        aspect-ratio: 1;
        height: 2rem;
        cursor: pointer;
        align-items: center;
        justify-content: center;
    }

    .bar > div > :global(*) {
        margin: auto;
    }

    .rest {
        background-color: #ededed;
        border-radius: 0.6rem;
    }

    @media (prefers-color-scheme: dark) {
        .bar {
            background-color: #141414;
        }
        .rest {
            background-color: #000000;
        }
    }
</style>
