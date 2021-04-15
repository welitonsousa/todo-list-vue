<template>
  <div>
    <span class="progress">
      <span :style="`width: ${porcentagem}%`" class="porcentagem">
        <h3 class="numeroPorcentagem">{{porcentagem}}%</h3>
      </span>
    </span>
  </div>
</template>

<script>
export default {};
</script>

<style>
</style>
