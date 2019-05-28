<script>
    import { onMount } from 'svelte';

    let canvas;
    let ctx;
    let grid = [];

    const fieldSize = 800;
    const numberOfCellsInRow = 50;
    $: cellSize = fieldSize / numberOfCellsInRow;

    const drawGridLine = (ctx, xb, yb, xe, ye) => {
        ctx.lineWidth = 1;
        ctx.beginPath();
        ctx.moveTo(xb,yb);
        ctx.lineTo(xe,ye);
        ctx.stroke();
    }

    const drawGrid = (ctx) => {
        for(let i = 0; i <= fieldSize; i += cellSize) {
            drawGridLine(ctx, i, 0, i, fieldSize);
            drawGridLine(ctx, 0, i, fieldSize, i);
        }
    }

    let randomFill = (ctx) => {
        for (let i=0; i < numberOfCellsInRow; i++) {
            grid.push([[]]);
            for (let j = 0; j < numberOfCellsInRow; j++) {
                grid[i][j] = Math.random() > 0.9 ? 1 : 0;
                if (grid[i][j] == 1) {
                    ctx.beginPath();
                    ctx.arc(cellSize/2 + i * cellSize, cellSize/2 + j * cellSize, 5, 0, 2 * Math.PI);
                    ctx.fill();
                }
            }
        }
    }

    let start = (ctx) => {
        console.log("started");
    }

    onMount(() => {
        canvas = document.getElementById('canvas');
        ctx = canvas.getContext('2d');
        drawGrid(ctx);
        randomFill(ctx);
        start(ctx);
    });
</script>

<style>
    #canvas {
        display: block;
        margin: 0 auto;
    }
</style>

<canvas id="canvas" width={fieldSize} height={fieldSize}></canvas>