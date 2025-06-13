<script lang="ts">
	import * as mathjs from "mathjs";

	$effect(() => {
		let textBox = document.getElementById("textBox") as HTMLInputElement;

		let buttons = document.querySelectorAll("button");
		let buttonsMap: Map<string, HTMLButtonElement> = new Map();

		buttons.values().forEach((btn) => {
			btn.addEventListener("click", () => {
				switch (btn.textContent) {
					case ".":
						if (!textBox.value.includes(".")) textBox.value += ".";
						break;
					case "C":
						textBox.value = "";
						break;
					case "=":
						textBox.value = mathjs.evaluate(textBox.value);
						break;
					default:
						textBox.value += btn.textContent;
						break;
				}
			});

			buttonsMap.set(btn.textContent!, btn);
		});
		console.log(buttonsMap);

		textBox.addEventListener("keypress", (event) => {
			event.preventDefault();
			switch (event.key) {
				case "0":
				case "1":
				case "2":
				case "3":
				case "4":
				case "5":
				case "6":
				case "7":
				case "8":
				case "9":
				case ".":
				case "+":
				case "-":
				case "*":
				case "/":
					let btn = buttonsMap.get(event.key);
					btn?.click();
					break;
				default:
					console.log(event.key);
					break;
			}
		});
	});
</script>

<main class="container">
	<input
		id="textBox"
		style="grid-area: text-box;"
		type="text"
		placeholder="..."
	/>
	<button>7</button> <button>8</button> <button>9</button> <button>+</button>
	<button>4</button> <button>5</button> <button>6</button> <button>-</button>
	<button>1</button> <button>2</button> <button>3</button> <button>*</button>
	<button>0</button> <button>.</button> <button>=</button> <button>/</button>
	<button>C</button>
</main>

<style>
	:root {
		font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
		font-size: 16px;
		line-height: 24px;
		font-weight: 400;

		color: #0f0f0f;
		background-color: #f6f6f6;

		font-synthesis: none;
		text-rendering: optimizeLegibility;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		-webkit-text-size-adjust: 100%;
	}

	.container {
		display: grid;
		grid-template-columns: repeat(4, auto);
		grid-row: repeat(5, 50px);
		grid-template-areas:
			"text-box text-box text-box text-box"
			"seven eight nine plus"
			"four five six minus"
			"one two three star"
			"zero dot equals division"
			"C C C C";
		margin: 0;
		gap: 8px;
	}

	input,
	button {
		border-radius: 8px;
		border: 1px solid transparent;
		padding: 0.6em 1.2em;
		font-size: 1em;
		font-weight: 500;
		font-family: inherit;
		color: #0f0f0f;
		background-color: #ffffff;
		transition: border-color 0.25s;
		box-shadow: 0 2px 2px rgba(0, 0, 0, 0.2);
	}

	button {
		cursor: pointer;
	}

	button:hover {
		border-color: #396cd8;
	}
	button:active {
		border-color: #396cd8;
		background-color: #e8e8e8;
	}

	input,
	button {
		outline: none;
	}

	@media (prefers-color-scheme: dark) {
		:root {
			color: #f6f6f6;
			background-color: #2f2f2f;
		}

		input,
		button {
			color: #ffffff;
			background-color: #0f0f0f98;
		}
		button:active {
			background-color: #0f0f0f69;
		}
	}
</style>
