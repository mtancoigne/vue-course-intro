<template>
  <div class="composant">
    Ceci est mon composant
    <div>
      <!--
      le "slot" correspond au bloc qui sera donné en tant que
      contenu de ce composant
      -->
      <slot/>
    </div>
    On le voit bien, il est rouge
  </div>
</template>

<style>
  .composant {
    background-color: red;
  }
</style>
