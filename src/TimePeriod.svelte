<script>
  export let label = "P"; // time pediod label: M | H | S | (P as default)
  export let span = "00"; // 00 <= span <= 59, as two-digi string

  const OFF_COLOR = "#444"; // dark-gray
  const ON_COLOR = "#79FE0C"; // fluorescent-green
  const NUM_BIN_ARRAY = Object.freeze([
    // decimal (0-9) to binary look-up table
    [0, 0, 0, 0],
    [0, 0, 0, 1],
    [0, 0, 1, 0],
    [0, 0, 1, 1],
    [0, 1, 0, 0],
    [0, 1, 0, 1],
    [0, 1, 1, 0],
    [0, 1, 1, 1],
    [1, 0, 0, 0],
    [1, 0, 0, 1],
  ]);
  const MAT_WIDTH = 2;
  const MAT_HEIGHT = 4;
  let colorMat = Array(MAT_WIDTH).fill(Array(MAT_HEIGHT).fill(OFF_COLOR));

  function getColorMat(span) {
    return span
      .split("") // into two digits
      .map((digit) => NUM_BIN_ARRAY[Number(digit)]) // into binary array
      .map((row) => row.map((on) => (on ? ON_COLOR : OFF_COLOR))); // into color
  }

  $: colorMat = getColorMat(span);
</script>

<section id="time-period_container">
  <header class="container" id="label_container">
    <span id="label-text">
      {label}
    </span>
  </header>
  <svg viewBox="0 0 60 150" width="80" height="150">
    {#each [0, 40] as x, i (x)}
      {#each [0, 40, 80, 120] as y, j (y)}
        <rect {x} {y} width="35" height="35" style="fill: {colorMat[i][j]}" />
      {/each}
    {/each}
    Sorry, your browser does not support inline SVG.
  </svg>
</section>

<style>
  .container {
    display: grid;
    place-items: center;
  }

  #time-period_container {
    min-width: 60px;
  }

  #label_container {
    font-size: clamp(5vw, 20px, 10vw);
    width: 100px;
    margin: 10px 0px;
  }

  #label-text {
    text-align: center;
    font-family: "Orbitron", sans-serif;
  }
</style>
