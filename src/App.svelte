<script>
  import canvasimg from "../src/assets/canvas.png";
  let type = "number";
  let hoursPerDay = 1;
  let days = 1;
  const today = new Date();
  const endDate = new Date("2023, 2, 15")
  const daysLeft = Math.floor((endDate.getTime() - today.getTime()) / (1000 * 3600 * 24)); 
  let level = 22;
  let points = 735;
  const maxPoints = 50 * 1000;
  let collectedPoints = (level - 1) * 1000 + points;
  let remainingPoints = maxPoints - collectedPoints;
  let dailyGoal = Math.ceil(remainingPoints / daysLeft);

  
  const prices = [60, 100, 200]
  let quantity = [Math.ceil(hoursPerDay/3)*days, days, Math.ceil(days/3)];
  let costs = [prices[0] * quantity[0], prices[1] * quantity[1], prices[2] * quantity[2]]
  let costsPerHour = [costs[0] / (hoursPerDay * days), costs[1] / (hoursPerDay * days), costs[2] / (hoursPerDay * days)]

  /*TJ's toller Canvas Code - start*/

  let canvas = document.createElement('canvas');

  canvas.id = "canv";
  canvas.width = 562;
  canvas.height = 98;
  canvas.style.zIndex = "8";
  canvas.style.position = "absolute";


  let div = document.getElementById("canvas");
  div.appendChild(canvas);

  let ctx = canvas.getContext("2d");
  const image = new Image();
  image.src = canvasimg;
  image.addEventListener(
      "load",
      () => {
          ctx.drawImage(image, 0, 0);

          ctx.font = '35pt calibri';
          ctx.textAlign = 'left';
          ctx.textBaseline = 'top';
          ctx.fillStyle = '#ffeac2';
          ctx.shadowBlur = 20;
          ctx.fillText(String(level), 150, 5);

          ctx.font = '25pt calibri';
          ctx.textAlign = 'right';
          ctx.textBaseline = 'top';
          ctx.fillStyle = '#fff';
          ctx.shadowBlur = 20;
          ctx.fillText(String(level), 420, 15);
      },
      false
  );

  /*TJ's toller Canvas Code - end*/

  function calculate() {
    quantity = [Math.ceil(hoursPerDay/3)*days, days, Math.ceil(days/3)];
    costs = [prices[0] * quantity[0], prices[1] * quantity[1], prices[2] * quantity[2]]
    costsPerHour = [costs[0] / (hoursPerDay * days), costs[1] / (hoursPerDay * days), costs[2] / (hoursPerDay * days)]
  }
  function calculateDailyGoal() {
    collectedPoints = (level - 1) * 1000 + points;
    remainingPoints = maxPoints - collectedPoints;
    dailyGoal = Math.ceil(remainingPoints / daysLeft);

    let ctx = canvas.getContext("2d");
    const image = new Image();
    image.src = canvasimg;
    image.addEventListener(
        "load",
        () => {
            ctx.drawImage(image, 0, 0);

            ctx.font = '35pt calibri';
            ctx.textAlign = 'left';
            ctx.textBaseline = 'top';
            ctx.fillStyle = '#ffeac2';
            ctx.shadowColor = "black";
            ctx.shadowBlur = 20;
            ctx.fillText(String(level), 150, 5);

            ctx.font = '25pt calibri';
            ctx.textAlign = 'right';
            ctx.textBaseline = 'top';
            ctx.fillStyle = '#fff';
            ctx.shadowColor = "black";
            ctx.shadowBlur = 20;
            ctx.fillText(String(points), 420, 15);
        },
        false
    );
  }
</script>

<h1>Devils Moon Calculator</h1>

<hgroup>
  <h2>Event Progress Calculator</h2>
  <h3>Calculate your daily goal for points in order to finish the event</h3>
</hgroup>
<div id="canv" style="width: 562px; heigth: 98px;"></div>
<h3>What level is your next?</h3>
<input bind:value={level} on:input={calculateDailyGoal} type="number" min="1" max="50">
<h3>How many points have you already collected to unlock level {level}?</h3>
<input bind:value={points} on:input={calculateDailyGoal} type="number" min="0" max="1000">
<p style="font-size: 25px;">You need to collect <b>{dailyGoal} points every day</b> to reach the remaining {50 - level + 1} levels by February 15.<br>
  In total you have to collect {remainingPoints} points. ({collectedPoints} / {maxPoints} Points)</p>
<br><br>

<hgroup>
  <h2>Contract Booster Calculator</h2>
  <h3>Calculate the most efficient booster contract</h3>
</hgroup>
<h3>How many hours do you play per day?</h3>
<input bind:value={hoursPerDay} on:input={calculate} type="number" min="1" max="24">
<h3>How many days in a row do you play?</h3>
<input bind:value={days} on:input={calculate} type="number" min="1" max="90">
<br><br>
<table>
  <tr>
    <th>Contract</th>
    <th>Price</th>
    <th>Quantity</th>
    <th>Costs</th>
    <th>Costs per Hour</th>
  </tr>
  <tr>
    <td>3h Contract</td>
    <td>{prices[0]}</td>
    <td>{quantity[0]}</td>
    <td>{costs[0]}</td>
    <td>{costsPerHour[0].toFixed(2)}</td>
  </tr>
  <tr>
    <td>24h Contract</td>
    <td>{prices[1]}</td>
    <td>{quantity[1]}</td>
    <td>{costs[1]}</td>
    <td>{costsPerHour[1].toFixed(2)}</td>
  </tr>
  <tr>
    <td>3 Day Contract</td>
    <td>{prices[2]}</td>
    <td>{quantity[2]}</td>
    <td>{costs[2]}</td>
    <td>{costsPerHour[2].toFixed(2)}</td>
  </tr>
</table> 



<style>
</style>
