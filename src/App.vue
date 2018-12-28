<template>
  <div>
  <div class="site-header">
    <div class="container">
      <a href="/" class="branding">
        <img src="images/logo.png" alt="" class="logo">
        <div class="logo-type">
          <h1 class="site-title">Weather Application</h1>
          <small class="site-description">In Deg. Celsius</small>
        </div>
      </a>

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

    </div>
  </div>
  <!-- .site-header -->

  </div>
</template>
