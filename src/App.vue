<script setup>

</script>
  
<template>
  <h1>vue</h1>
</template>

<style lang="css">

  /*==========Reset==========*/
  *, *::before, *::after {
        margin: 0;
        padding: 0;
        border: 0;
        box-sizing: border-box;
        outline: none;
        text-decoration: none;
        list-style: none;
        appearance: none;
        font-family: 'Poppins', sans-serif;
    }

  /*==========Base==========*/
  :root {

    --primary-color: hsl(25, 76%, 90%);
    --dark-color: hsl(0, 0%, 13%);
    --black-color: hsl(0, 0%, 0%);
    --white-color: hsl(0, 0%, 100%);
    --green-color: hsl(154, 100%, 81%);
    --red-color: hsl(347, 100%, 71%);

    --transition: all 400ms ease-in-out;
    --shadow: 0px 1px 3px hsla(0, 0%, 0%, 0.5);
    --shadow-1: 0px 3px 6px hsla(0, 0%, 0%, 0.4);

    --container-lg: 80%;
    --container-md: 90%;
    --container-max-wd: 1800px;

  }

  /*==========Base==========*/
  body {
    background: var(--primary-color);
    color: var(--dark-color);
    height: 300rem;
  }

  ::-webkit-scrollbar {
    width: .5rem;
  }
  ::-webkit-scrollbar-track {
    background: var(--dark-color);
  }
  ::-webkit-scrollbar-thumb {
    background: var(--primary-color);
  }
  .container {
    width: var(--container-lg);
    max-width: var(--container-max-wd);
    margin-inline: auto;  
  }

  /*==========Quiz==========*/

</style>