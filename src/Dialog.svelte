<script>
    export let dialog;
</script>

<dialog bind:this={dialog} on:close>
    <slot />
</dialog>

<style>
    dialog::backdrop {
        backdrop-filter: blur(8px);
    }

    dialog {
        background-color: transparent;
        border: 0;
        padding: 0;
        margin: 0;
        outline: none;
        height: 100vh;
        height: 100dvh;
        width: 100vw;
        max-width: 100vw;
        max-height: 100vh;
        max-height: 100dvh;
    }
</style>
