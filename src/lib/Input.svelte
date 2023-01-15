<script>
  let min = 0;
  let max = 0;
  let hoursPerDay = 0;
</script>


<input bind:value={hoursPerDay} type="number" min="{min}" max="{max}">
<h1>{hoursPerDay}</h1>


<style>
  input {
   align-content: left;
   font-size: 20px; 
  }
</style>