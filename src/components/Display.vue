<template>
  <div class="display">
        <h3> {{ operation }}</h3>
        <h1><code>{{ display }}</code></h1>
  </div>
</template>

<script>
export default {
    props:['display','operation']
}
</script>

<style scoped>
.display{
    min-height: 115px;
    margin: 15px;
    padding: 10px;
    text-align: right;
    background-color: chartreuse;
    border-radius: 15px;
}
.display code {
    color: black;
}
</style>