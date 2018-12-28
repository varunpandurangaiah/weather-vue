<template>
<!-- Default snippet for navigation -->
<div class="main-navigation" id="nav">
  <button type="button" class="menu-toggle"><i class="fa fa-bars"></i></button>
  <ul class="menu">
      <router-link to="/"><li class="menu-item current-menu-item"><a>Home</a></li></router-link>
      <router-link to="/about"><li class="menu-item"><a>About</a></li></router-link>
  </ul> <!-- .menu -->
</div> <!-- .main-navigation -->

<div class="mobile-navigation"></div>
<router-view/>
</template>

<script>
export default {
    name: 'AppNavigation'
};
</script>
