<script>
	export let formFields = [];  // Array of objects describing each field
	export let maxWidth = "400px";
	export let top = 'auto';
	export let right = 'auto';
	export let bottom = 'auto';
	export let left = 'auto';

	function handleSubmit(event) {
		event.preventDefault();
		const formData = new FormData(event.target);
		const formProps = {};
		formData.forEach((value, key) => { formProps[key] = value; });
		console.log('Form Data:', formProps); // Handle form submission logic here
	}
</script>

<form on:submit={handleSubmit} class="glowing-box"
			style="top: {top}; right: {right}; bottom: {bottom}; left: {left}; position: fixed; max-width: {maxWidth};">
	{#each formFields as {label, type, name, placeholder}, index}
		<div class="input-wrapper">
			<label for={name}>
				{label}
				<input type={type} id={name} name={name} placeholder={placeholder} />
			</label>
		</div>
	{/each}
	<button type="submit" class="submit-button">Submit</button>
</form>

<style>
    .glowing-box {
        padding: 20px;
        border: 2px solid #ffffff;
        color: #ffffff;
        background-color: rgba(18, 18, 18, 0.6);
        box-shadow: 0 0 8px rgba(111, 30, 181, 0.8),
        0 0 16px rgba(142, 10, 10, 0.8),
        0 0 24px rgba(154, 3, 178, 0.8);
        border-radius: 24px;
        text-align: center;
        font-size: 16px;
        width: fit-content;
        margin: auto;
        line-height: 1.5;
        overflow: auto;
        max-height: 90vh;
        word-wrap: break-word;
        z-index: 100;
        position: fixed;
    }
    .input-wrapper {
        margin-bottom: 10px;
    }
    input {
        width: 100%;
        padding: 8px;
        margin-top: 4px;
        box-sizing: border-box;
        border-radius: 4px;
        border: 1px solid #ccc;
        background-color: #fff;
        color: #333;
    }
    .submit-button {
        padding: 10px 20px;
        color: #fff;
        background-color: #4CAF50; /* Green background */
        border: none;
        border-radius: 4px;
        cursor: pointer;
    }
    .submit-button:hover {
        background-color: #45a049;
    }
</style>
