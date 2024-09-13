<template>
  <header>
    <nav>
      <ul>
        <li>
          <img src="../src/assets/logo.png" alt="Bonster-Logo" class="img-items-logo">
        </li>
        <li>
          <router-link to="/">
            <img src="../src/assets/home.png" alt="home">
            <span class="text1">Home</span>
          </router-link>
        </li>
        <li>
          <router-link to="/productos">
            <img src="../src/assets/Producto.png" alt="producto">
            <span class="text1">Producto</span>
          </router-link>
        </li>
        <li>
          <router-link to="/cotizador">
            <img src="../src/assets/cotizador.png" alt="cotizar">
            <span class="text1">Cotizar</span>
          </router-link>
        </li>
      </ul>
    </nav>
  </header>
  <router-view />
</template>

<style>
html {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  background-color: #F2F2F2;
}

body {
  margin: 0;
}

header {
  position: fixed;
  z-index: 200;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 0px;
  gap: 0px;
  float: left;
}

nav ul {
  list-style: none;
  overflow: hidden;
}

nav ul li {
  float: left;
}

nav ul li a {
  display: flex;
  padding: 20px;
  position: relative;
  align-items: center;
  border-radius: 10%;
  gap: 10px;  
}

nav ul li a:hover {
  background: #4F4050;
  text-emphasis-color: #F2F2F2;
}

.text1 {
  position: absolute;
  color: #4F4050;
  top: 68px;
  left: 22px;
}
</style>