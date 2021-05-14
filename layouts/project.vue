<template>
  <div class="container">
    <Nuxt />
  </div>
</template>

<style  lang="scss">
  html {
    font-family:
            Arial,
            sans-serif;
    font-size: 16px;
    word-spacing: 1px;
    -ms-text-size-adjust: 100%;
    -webkit-text-size-adjust: 100%;
    -moz-osx-font-smoothing: grayscale;
    -webkit-font-smoothing: antialiased;
    box-sizing: border-box;
  }

  *,
  *::before,
  *::after {
    box-sizing: border-box;
    margin: 0;
  }

  body {
    background-color: #FBFBFB;
    color: #000;
  }

  .container {
    max-width: 1060px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    padding: 0 20px;
  }
  button, input[type="submit"], input[type="reset"] {
    background: none;
    color: inherit;
    border: none;
    padding: 0;
    font: inherit;
    cursor: pointer;
    outline: inherit;
  }
</style>
