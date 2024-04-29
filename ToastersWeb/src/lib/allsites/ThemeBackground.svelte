<!-- src/ThemeBackground.svelte -->

<style>
    :global(body) {
        background: linear-gradient(to right, #0a0c1b, #1d1e33, #302b4e, #1d1e33, #0a0c1b);
        color: #fff; /* Ensures that text is white for better readability on a dark background */
        height: 100vh; /* This makes sure that the background covers the whole visible part of the webpage */
        margin: 0; /* Removes the default margin provided by browsers */
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>
