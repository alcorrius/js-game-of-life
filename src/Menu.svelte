<script>
	import Canvas from './Canvas.svelte';

	let fieldSize = 100;
	let numberOfCellsInRow = 10
	let started = false;
	let buttonName = "Start";

	let onStart = () => {
		started = !started;
		buttonName = started == true ? "Stop" : "Start";
	};

</script>



<style>
	.grid-container {
		display: grid;
	}
	.column1 {
		grid-column: 1 / 2;
	}
	.column2 {
		grid-column: 2 / 2;
	}
</style>



<div class="grid-container">
	<div class="column1">
		<h2>Menu</h2>
		<p>
			<label>Field size</label>
			<input bind:value={fieldSize} />
			<label>Cells in row</label>
			<input bind:value={numberOfCellsInRow} />
		</p>
		<button on:click={onStart}>{buttonName}</button>
	</div>

	<div class="column2">
		<Canvas started={started} fieldSize={fieldSize} numberOfCellsInRow={numberOfCellsInRow} onStart=/>
	</div>

</div>