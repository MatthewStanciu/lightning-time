<script lang="ts">
  let timeString = "0~0~0~0";
  let milliCharges = 0;
  let charges = 0;
  let sparks = 0;
  let zaps = 0;
  let bolts = 0;

  const millisPerMilliCharge = 82.3974609375; // 86400000 / 16^5

  function updateTime() {
    const time = new Date();
    const millis = 1000 * 60 * 60 * time.getHours() + 1000 * 60 * time.getMinutes() + 1000 * time.getSeconds() + time.getMilliseconds();
    const totalMilliCharges = millis / millisPerMilliCharge
    const totalCharges = totalMilliCharges / 16;
    const totalSparks = totalCharges / 16;
    const totalZaps = totalSparks / 16;
    const totalBolts = totalZaps / 16;

    milliCharges = Math.floor(totalMilliCharges) % 16;
    charges = Math.floor(totalCharges) % 16;
    sparks = Math.floor(totalSparks) % 16;
    zaps = Math.floor(totalZaps) % 16;
    bolts = Math.floor(totalBolts) % 16;

    timeString = bolts.toString(16) + "~" + zaps.toString(16) + "~" + sparks.toString(16) + "|" + charges.toString(16) + milliCharges.toString(16);
  }

  updateTime();
  setInterval(updateTime, 10);
</script>

<div style:background-image={`linear-gradient(${window.innerWidth < 640 ? '180deg' : '90deg'}, rgb(${bolts * 16 + zaps}, 161, 0), rgb(150, ${zaps * 16 + sparks}, 100), rgb(85, 66, ${sparks * 16 + charges}))`}>
  <h1>{timeString}</h1>
</div>

<style>
  div {
    width: 100%;
    height: 100%;
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    font-variant-numeric: tabular-nums;
  }
  h1 {
    font-size: 6rem;
    line-height: 1.1;
    font-family: 'Space Mono';
  }
  @media only screen and (max-width: 640px) {
    h1 {
      font-size: 4rem;
      line-height: 1.1;
      font-family: 'Space Mono';
    }
  }

  @font-face {
    font-family: 'Space Mono';
    font-style: normal;
    font-weight: 400;
    font-display: swap;
    src: url(https://fonts.gstatic.com/s/spacemono/v12/i7dPIFZifjKcF5UAWdDRYEF8RXi4EwQ.woff2) format('woff2');
    unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
  }
  @font-face {
    font-family: 'Space Mono';
    font-style: normal;
    font-weight: 700;
    font-display: swap;
    src: url(https://fonts.gstatic.com/s/spacemono/v12/i7dMIFZifjKcF5UAWdDRaPpZUFWaHi6WZ3Q.woff2) format('woff2');
    unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
  }
</style>