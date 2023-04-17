<template>
  <div id="app">
    <div class="app-header">
      <div class="app-header__nav responsive-container">
        <i class="app-header__nav__logo material-symbols-outlined">public</i>
        <h1 class="app-header__nav__title">
          Natural History Museum
        </h1>
      </div>
    </div>
    <div class="app-view">
      <SpacePage />
    </div>
  </div>
</template>

<script>
import SpacePage from './components/SpacePage.vue'

export default {
  name: 'App',
  components: {
    SpacePage
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400;500&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,300,1,0');
#app {
  font-family: 'Open Sans', sans-serif;
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 2rem;
  .app-header {
    position: sticky;
    top: 0;
    display: flex;
    justify-content: center;
    width: 100%;
    height: 3rem;
    background: #ddd;
    &__nav {
      display: flex;
      align-items: center;
      gap: 1rem;
      &__logo {
        color: #242424;
        font-size: 36px;
      }
      &__title {
        color: #242424;
        font-size: 20px;
        font-weight: 500;
      }
    }
  }
  .app-view { 
    display: flex;
    justify-content: center;
    flex: 1 1 0%;
    min-width: 0;
  }
}
.responsive-container {
    width: 100%;
    @media (min-width: 480px){
        width: 480px;
    }
    @media (min-width: 760px){
        width: 760px;
    }
    @media (min-width: 1024px){
        width: 1024px;
    }
    margin-left: auto;
    margin-right: auto;
    padding-left: 2rem;
    padding-right: 2rem;
}
p, h1, h2 {
  margin: 0;
}
* {
  box-sizing: border-box;
  /* Firefox */
  scrollbar-width: auto;
  scrollbar-color: #242424 #ffffff;
}
/* Chrome, Edge, and Safari */
*::-webkit-scrollbar {
  width: 8px;
}
*::-webkit-scrollbar-track {
  background: #ffffff;
}
*::-webkit-scrollbar-thumb {
  background-color: #242424;
  border-radius: 4px;
  border: 2px solid #ffffff;
}
</style>
