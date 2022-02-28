<template>
  <div id="app">
<b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
          <b-collapse id="nav-collapse" is-nav>
           <b-navbar-nav>
             <b-nav-item href="#">
                <router-link to="/">
                <img id="logohome" src="../src/assets/colorpwiki.png" alt="" class="mr-sm-2" width="38px" height="39px" center>
                </router-link> 
              </b-nav-item>
              <b-nav-item href="#" class="mr-sm-6">
                <router-link to="/about">
                <img src="../src/assets/pokebola.png" alt="" class="mr-sm-2" width="30px" height="30px" center>
                </router-link> 
              </b-nav-item>
           </b-navbar-nav>
      <!-- Right aligned nav items -->
      <b-navbar-nav>
        <b-nav-item-dropdown text="Integrantes:" right>
          <b-dropdown-item href="#">David Alexis Gallegos González</b-dropdown-item>
          <b-dropdown-item href="#">Nestor Wilfredo Chavez Ramirez</b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
