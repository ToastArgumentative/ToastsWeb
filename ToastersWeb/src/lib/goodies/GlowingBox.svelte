<!-- src/GlowingBox.svelte -->
<script>
    import DownloadButtonGreen from "$lib/assets/DownloadIconGreen.svg";
    import DownloadButtonRed from "$lib/assets/DownloadIconRed.svg";

    export let title = "";
    export let titleLink = "";
    export let text = 'Default Text';
    export let showFullText = false;


    export let downloadLink = '';
    export let downloadGoodOrBad = "good";

    export let maxWidth = "400px";
    export let top = 'auto';
    export let right = 'auto';
    export let bottom = 'auto';
    export let left = 'auto';


    function toggleText(event) {
        if (event.type === 'click' || event.keyCode === 13 || event.keyCode === 32) {
            showFullText = !showFullText;
        }
    }

    function startDownload(event) {
        if (downloadLink !== '') {
            const link = document.createElement('a');
            link.href = downloadLink;
            link.download = downloadLink.split('/').pop();
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }
        event.preventDefault(); // Prevent the default action for the keydown event
    }
</script>

<div class="glowing-box" role="button" tabindex="0"
     on:click={toggleText}
     on:keydown={toggleText}
     style="top: {top}; right: {right}; bottom: {bottom}; left: {left}; position: fixed; max-width: {maxWidth};">
    <div class="title-download-wrapper">
        {#if title}
            {#if titleLink}
                <a class="titleLink" href={titleLink}>{title}</a>
            {/if}
            {#if !titleLink}
                <h1 class="title">{title}</h1>
            {/if}
        {/if}
        {#if downloadLink}
            <button on:click|stopPropagation={startDownload} on:keydown|stopPropagation={event => (event.key === 'Enter' || event.key === ' ') && startDownload(event)} class="download-button">
                {#if downloadGoodOrBad === "good"}
                    <img src={DownloadButtonGreen} class="icon" alt="This archive is ready for production!">
                {/if}
                {#if downloadGoodOrBad === "bad"}
                    <img src={DownloadButtonRed} class="icon" alt="This archive is not production ready!">
                {/if}
            </button>
        {/if}

    </div>
    <div class="content-wrapper">
        {@html showFullText ? text : text.slice(0, 100) + '...'}
    </div>
</div>


<style>
    .glowing-box {
        padding: 20px;
        border: 2px solid #ffffff; /* White border */
        color: #ffffff; /* White text */
        background-color: rgba(18, 18, 18, 0.3); /* Dark background with transparency */
        box-shadow: 0 0 8px rgba(111, 30, 181, 0.8), /* Innermost glow */
        0 0 16px rgba(142, 10, 10, 0.8), /* Middle glow */
        0 0 24px rgba(154, 3, 178, 0.8); /* Outermost glow */
        border-radius: 24px; /* Rounded corners */
        text-align: center;
        font-size: 16px;
        width: fit-content;
        margin: auto;
        line-height: 1.5; /* Improves readability for blocks of text */
        overflow: auto; /* Makes the content scrollable if it overflows */
        max-height: 200px; /* Adjust based on your needs */
        word-wrap: break-word; /* Ensures long words do not cause overflow */
        z-index: 100; /* Ensure it's above other content */
        position: fixed; /* This is crucial for positioning */
    }
    .glowing-box::-webkit-scrollbar {
        display: block;
    }

    .content-wrapper {
        display: flex;
        flex-direction: row; /* Align items horizontally */
        align-items: center; /* Center-align items vertically */
        justify-content: space-between; /* Push the title to the left and the download button to the right */
        width: 100%;
    }
    .title-download-wrapper {
        display: flex;
        justify-content: space-between; /* This will push the title to the center and the download button to the right */
        align-items: center;
        width: 100%;
    }

    .title {
        text-align: center;
        flex-grow: 1; /* Allows the title to take up the maximum available space */
    }
    .titleLink , .title {
        text-align: center;
        flex-grow: 1;
        font-size: 26px;
        color: #ffffff;
    }

    .download-button {
        background: none;
        border: none;
        cursor: pointer;
        /* Adjust the size of the button if needed */
    }

    .icon {
        width: 48px; /* Adjust based on your needs */
        height: 48px; /* Adjust based on your needs */
        /* Ensure the icon is visible and appropriately sized */
    }

</style>
