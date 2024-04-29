<!-- src/GlowingBox.svelte -->
<script>
    import DownloadButtonGreen from "$lib/assets/DownloadIconGreen.svg";
    import DownloadButtonRed from "$lib/assets/DownloadIconRed.svg";

    export let title = "";
    export let titleLink = "";
    export let text = 'Default Text';
    export let hoverText = ''
    export let showFullText = false;

    export let downloadLink = '';
    export let downloadGoodOrBad = "good";

    export let maxWidth = "400px";
    export let top = 'auto';
    export let right = 'auto';
    export let bottom = 'auto';
    export let left = 'auto';

    let tooltipX = 0;
    let tooltipY = 0;
    let showTooltip = false;

    function handleMouseMove(event) {
        tooltipX = event.clientX;
        tooltipY = event.clientY - 50; // Position the tooltip 50px above the mouse
        showTooltip = true;
    }

    function handleMouseLeave() {
        showTooltip = false; // Hide the tooltip when the mouse leaves the box
    }


    function toggleText(event) {
        if (event.type === 'click' || event.keyCode === 13 || event.keyCode === 32) {
            showFullText = !showFullText;
        }
    }



    function startDownload() {
        if (downloadLink !== '') {
            const link = document.createElement('a');
            link.href = downloadLink;
            link.download = downloadLink.split('/').pop();
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }
    }
</script>

<div class="glowing-box" role="button" tabindex="0" on:click={toggleText} on:keydown={toggleText}
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
            <button on:click|stopPropagation={startDownload} class="download-button">
                {#if downloadGoodOrBad === "good"}
                    <img src={DownloadButtonGreen} class="icon" alt="Download file!">
                {/if}
                {#if downloadGoodOrBad === "bad"}
                    <img src={DownloadButtonRed} class="icon" alt="Download file!">
                {/if}
            </button>
        {/if}
        {#if showTooltip}
            <div class="tooltip" style="top: {tooltipY}px; left: {tooltipX}px;">{hoverText}</div>
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
    .tooltip {
        position: fixed;
        padding: 5px 10px;
        color: #ffffff;
        background-color: rgba(0, 0, 0, 0.7);
        border-radius: 5px;
        font-size: 14px;
        white-space: nowrap;
        pointer-events: none; /* Prevents the tooltip from interfering with mouse events */
        display: none; /* Initially hide the tooltip */
    }
    .glowing-box:hover .tooltip {
        display: block; /* Show the tooltip on hover */
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
