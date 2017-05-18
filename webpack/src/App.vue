<template>
  <div id="app">
      <div class="container">
    <Navigation></Navigation>
    <router-view></router-view>
    <div class="row list-footer">
      <div class="col-sm-3">
        <router-link to="/" class="brand-logo-footer">Tech Jobs</router-link>
      </div>
      <div class="col-sm-offset-6 col-sm-3">
        <router-link to="/manage-positions" class="link-footer">Manage Positions</router-link>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
import Navigation from './components/Navigation'

export default {
  name: 'app',
  components: {
    Navigation
  }
}
</script>

<style lang="scss">
@import url('../node_modules/flexboxgrid/dist/flexboxgrid.css');
$logo-font-family: 'Dosis', serif;
$base-font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
$base-font-size: 12px;
$base-color: rgb(0,0,0);
$alt-color: rgb(255, 255, 255);
$gray-color: rgb(191, 191, 191);
$gray-color-hover: rgba(191, 191, 191, 0.5);
$color-green: #4CAF50;
$color-blue: #2196f3;
$light-gray-color: rgb(155, 155, 155);

* {
  box-sizing: border-box;
}

html {
  font-size: $base-font-size;
  color: $base-color;
  font-family: $base-font-family;
}

body {
  margin: 0;
  padding: 0;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  margin: 0;
  padding: 0;
}

h1 {
  font-size: 5rem;
}

h2 {
  font-size: 4.2rem;
}

h3 {
  font-size: 3.6rem;
}

h4 {
  font-size: 3.0rem;
}

h5 {
  font-size: 2.4rem;
}

h6 {
  font-size: 1.5rem;
}
.container {
  width:840px;
  position:relative;
}
.btn {
  display:inline-block;
  padding:10px 25px;
  border:0;
  color:white;
  text-align:center;
  border-radius:5px;
  font-size:1.2em;
  text-transform:uppercase;
  text-decoration:none;
  letter-spacing: 1px;
  &:focus {
    outline:none;
  }
}
.btn-green {
  background:$color-green;
  transition:all 350ms ease-in-out;
  box-shadow:0 0 5px RGBA(76, 175, 80, .4);
  &:hover {
    transform:scale(1.025);
    box-shadow:0 0 10px RGBA(76, 175, 80, .6);
  }
}
.btn-red {
  background:#e53935;
  transition:all 350ms ease-in-out;
  box-shadow:0 0 5px RGBA(229, 57, 53, .4);
  &:hover {
    transform:scale(1.025);
    box-shadow:0 0 5px RGBA(229, 57, 53, .6);
  }
}
.btn-blue {
  background:#2196f3;
  transition:all 350ms ease-in-out;
  box-shadow:0 0 5px RGBA(33, 150, 243, .4);
  &:hover {
    transform:scale(1.025);
    box-shadow:0 0 5px RGBA(33, 150, 243, .6);
  }
}

#app {
}
</style>
