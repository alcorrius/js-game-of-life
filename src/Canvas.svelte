<script>
    import { onMount } from 'svelte';
    let canvas;
    let ctx;

    const fieldSize = 800;
    const numberOfCellsInRow = 50;
    const framesPerSecond = 8;
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

    onMount(() => {
        canvas = document.getElementById('canvas');
        ctx = canvas.getContext('2d');
        drawGrid(ctx);
    });
</script>

<style>
    #canvas {
        display: block;
        margin: 0 auto;
    }
</style>

<canvas id="canvas" width="800" height="800"></canvas>