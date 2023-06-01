<template>
  <div id="app" class="dark-mode app-container">
    <AppHeader />
    <SlideShow />
    <AppFooter />
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'
import SlideShow from './components/SlideShow.vue'

export default {
  name: 'App',
  components: {
    AppHeader,
    AppFooter,
    SlideShow
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

body {
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
  background: #000;
  color: #fff;
}

.dark-mode {
  background-color: #000;
  color: #fff;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.app-container {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

#app>.app-header,
#app>.app-footer {
  flex-shrink: 0;
}

#app>.slideshow {
  flex-grow: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
