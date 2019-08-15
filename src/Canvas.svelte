<script>
  import { onMount } from "svelte";

  export let fieldSize = 800;
  export let numberOfCellsInRow = 50;
  export let started = false;

  const initialFillDensity = 0.9;

  let canvas;
  let ctx;
  let grid = [];
  let cellSize;
  let intervalId;

  $: {
    if (started) {
      //draw grid
      ctx.clearRect(0, 0, fieldSize, fieldSize);
      drawGrid(ctx);
      randomFill(ctx);

      //run task
      intervalId = setInterval(() => {
        draw(ctx);
      }, 500);
    } else {
      clearInterval(intervalId);
    }
  }

  $: {
    cellSize = fieldSize / numberOfCellsInRow;
  }

  const drawGridLine = (ctx, xb, yb, xe, ye) => {
    ctx.lineWidth = 1;
    ctx.beginPath();
    ctx.moveTo(xb, yb);
    ctx.lineTo(xe, ye);
    ctx.stroke();
  };

  const drawGrid = ctx => {
    for (let i = 0; i <= fieldSize; i += cellSize) {
      drawGridLine(ctx, i, 0, i, fieldSize);
      drawGridLine(ctx, 0, i, fieldSize, i);
    }
    ctx.fill();
  };

  let randomFill = ctx => {
    for (let i = 0; i < numberOfCellsInRow; i++) {
      grid.push([[]]);
      for (let j = 0; j < numberOfCellsInRow; j++) {
        grid[i][j] = Math.random() > initialFillDensity ? 1 : 0;
        if (grid[i][j] == 1) {
          ctx.beginPath();
          ctx.arc(
            cellSize / 2 + i * cellSize,
            cellSize / 2 + j * cellSize,
            cellSize / 3,
            0,
            2 * Math.PI
          );
          ctx.fill();
        }
      }
    }
  };

  let draw = ctx => {
    console.log("draw");
    for (let i = 0; i < numberOfCellsInRow; i++) {
      for (let j = 0; j < numberOfCellsInRow; j++) {
        grid[i][j] = Math.random() > initialFillDensity ? 1 : 0;
        if (grid[i][j] == 1) {
          ctx.fillStyle = "black";
          ctx.beginPath();
          ctx.arc(
            cellSize / 2 + i * cellSize,
            cellSize / 2 + j * cellSize,
            cellSize / 3,
            0,
            2 * Math.PI
          );
          ctx.fill();
        } else {
          ctx.fillStyle = "white";
          ctx.beginPath();
          ctx.arc(
            cellSize / 2 + i * cellSize,
            cellSize / 2 + j * cellSize,
            cellSize / 3,
            0,
            2 * Math.PI
          );
          ctx.fill();
        }
      }
    }
  };

  onMount(() => {
    console.log("mount");
    ctx = canvas.getContext("2d");
  });
</script>

<style>
  canvas {
    display: block;
    margin: 0 auto;
  }
</style>

<canvas bind:this={canvas} width={fieldSize} height={fieldSize} />
