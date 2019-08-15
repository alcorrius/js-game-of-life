<script>
  import Canvas from "./Canvas.svelte";

  const canvasProps = {
    fieldSize: 100,
    numberOfCellsInRow: 10,
    started: false
  };

  let buttonName = "Start";

  let onStart = () => {
    canvasProps.started = !canvasProps.started;
    buttonName = canvasProps.started == true ? "Stop" : "Start";
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
      <input bind:value={canvasProps.fieldSize} />
      <label>Cells in row</label>
      <input bind:value={canvasProps.numberOfCellsInRow} />
    </p>
    <button on:click={onStart}>{buttonName}</button>
  </div>

  <div class="column2">
    <Canvas {...canvasProps} />
  </div>

</div>
