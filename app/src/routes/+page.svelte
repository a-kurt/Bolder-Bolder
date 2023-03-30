<script>
	import '../app.css';
	import { onMount } from 'svelte';

	let inputText = '';
	let outputText = '';

	function transformText() {
		try {
			const lines = inputText.split('\n');
			let transformedText = '';
			lines.forEach((line, index) => {
				const words = line.split(/(\s+)/);
				words.forEach((word, wordIndex) => {
					if (word.length >= 2) {
						const firstTwoLetters = word.substr(0, 2);
						const remainingLetters = word.substr(2);
						transformedText += `<span class="font-bold">${firstTwoLetters}</span><span class="font-light">${remainingLetters}</span>`;
					} else {
						transformedText += `${word}`;
					}
					if (wordIndex !== words.length - 1) {
						transformedText += ' ';
					}
				});
				if (index !== lines.length - 1) {
					transformedText += `<span><br><span>`;
				}
			});
			outputText = transformedText;
		} catch (error) {
			console.error('Error transforming text:', error);
			// Handle the error here, such as displaying an error message to the user
		}
	}

	function handleKeyPress(event) {
		if (event.key === 'Enter') {
			transformText();
		}
	}
</script>

<div class="flex flex-col 2xl:flex-row justify-center h-screen items-center 2xl:mx-32">
	<h1
		class="text-4xl font-bold my-8 2xl:absolute 2xl:top-6 2xl:left-1/2 2xl:transform 2xl:-translate-x-1/2"
	>
		Bolder Bolder
	</h1>
	<textarea
		class="w-10/12 h-2/3 textarea textarea-bordered resize-none textarea-primary text-lg"
		placeholder="Enter text..."
		bind:value={inputText}
		aria-label="Enter text to be transformed"
	/>
	<button
		class="btn btn-m sm:btn-sm md:btn-md lg:btn-lg btn-success my-3 2xl:mx-6"
		on:click={transformText}
		on:keypress={handleKeyPress}
	>
		Transform
	</button>
	<div
		class="mb-3 pointer-events-none w-10/12 h-2/3 textarea textarea-bordered resize-none textarea-secondary text-lg"
		contenteditable="true"
		bind:innerHTML={outputText}
		aria-describedby="transformed-text"
	/>
</div>

<footer class="footer footer-center p-10 bg-primary text-primary-content">
	<div>
		<img width="100" height="100" viewBox="0 0 24 24" src="/logo.png" alt="logo">
		<p>Copyright © 2023 Atakan Kurt - All rights reserved.</p>
	</div>
	<div>
		<div class="grid grid-flow-col gap-4">
			<a  href="https://www.linkedin.com/in/atakankurt/" target="_blank"
				><svg
					xmlns="http://www.w3.org/2000/svg"
					width="24"
					height="24"
					viewBox="0 0 24 24"
					class="fill-current"
					><path
                    d="M21.6 0H2.4C1.1 0 0 1.1 0 2.4v19.2C0 22.9 1.1 24 2.4 24h19.2c1.3 0 2.4-1.1 2.4-2.4V2.4C24 1.1 22.9 0 21.6 0zM7.8 20.3H4.9V9.7h2.9v10.6zM6.4 8.7H6.4c-1 0-1.6-.7-1.6-1.5 0-.9.6-1.5 1.6-1.5s1.6.7 1.6 1.5c-.1.8-.7 1.5-1.6 1.5zm14.2 11.6h-2.9v-5.2c0-1.2-.4-2-1.4-2-1.6 0-1.8 1.2-1.8 2.4v5h-2.9V9.7h2.8v1.3h.1c.4-.8 1.3-1.6 2.7-1.6 2 0 2.4 1.3 2.4 3.1v5.8z"/>
                    </svg
				></a
			>
			<a  href="https://github.com/a-kurt" target="_blank"
				><svg
					xmlns="http://www.w3.org/2000/svg"
					width="24"
					height="24"
					viewBox="0 0 24 24"
					class="fill-current"
					><path d="M12 .318c-6.628 0-12 5.372-12 12 0 5.303 3.438 9.8 8.205 11.387.6.111.82-.258.82-.577 0-.285-.01-1.04-.015-2.042-3.338.724-4.042-1.61-4.042-1.61-.546-1.383-1.333-1.753-1.333-1.753-1.09-.746.083-.73.083-.73 1.207.086 1.84 1.242 1.84 1.242 1.07 1.84 2.809 1.305 3.495.998.108-.787.419-1.305.763-1.605-2.665-.305-5.466-1.332-5.466-5.93 0-1.31.465-2.383 1.235-3.22-.135-.304-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.4 3-.405 1.02.005 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.872.12 3.176.765.837 1.23 1.91 1.23 3.22 0 4.61-2.805 5.62-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.688.825.572 4.76-1.587 8.195-6.084 8.195-11.387 0-6.628-5.372-12-12-12z"/></svg
				></a
			>
		</div>
	</div>
</footer>

