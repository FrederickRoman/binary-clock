<script>
  import { onMount } from "svelte";
  import TimePeriod from "./TimePeriod.svelte";

  let date = new Date();
  const zeroPad = (n) => `${n < 10 ? "0" : ""}${n}`;

  onMount(() => {
    const intervalId = setInterval(() => (date = new Date()), 1000);
    return () => clearInterval(intervalId);
  });

  $: hours = zeroPad(date.getHours());
  $: minutes = zeroPad(date.getMinutes());
  $: seconds = zeroPad(date.getSeconds());
</script>

<main class="container" id="main">
  <section class="decimal-time_container">
    <header id="decimal-time">{hours} : {minutes} : {seconds}</header>
  </section>
  <section class="binary-time_container">
    <TimePeriod label="H" span={hours} />
    <TimePeriod label="M" span={minutes} />
    <TimePeriod label="S" span={seconds} />
  </section>
</main>

<style>
  .container {
    display: grid;
    place-items: center;
  }

  .binary-time_container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: center;
  }
  .decimal-time_container {
    display: grid;
    place-items: center;
  }

  #main {
    width: 100vw;
    height: 100vh;
  }

  #decimal-time {
    font-size: 10vw;
    font-family: 'Orbitron', sans-serif;
  }
</style>
