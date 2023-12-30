<script setup>
defineProps({
  msg: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <button id="toggleSidebar"><i class="fa-solid fa-bars"></i></button>
  <div class="sidebar">
    <ul>
      <li>
        <a href="#section1" class="nav-link active" data-target="section1"
          >Sección 1</a
        >
      </li>
      <li>
        <a href="#section2" class="nav-link" data-target="section2"
          >Sección 2</a
        >
      </li>
    </ul>
    <button class="DarkModeBtn" id="darkModeToggle">
      <i class="fas fa-moon"></i> Dark Mode
    </button>
  </div>

  <div class="content">
    <!-- Contenido principal -->
    <div id="section1" class="section">
      <h1>Sección 1</h1>
      <p>Contenido de la sección 1...</p>
    </div>

    <div id="section2" class="section">
      <h1>Sección 2</h1>
      <p>Contenido de la sección 2...</p>
    </div>
  </div>

  <div class="scroll-indicator"></div>
</template>

<style scoped>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  transition: 0.3s;
}

body.dark-mode {
  background-color: #222;
  color: #fff;
}

.sidebar {
  height: 100%;
  width: 250px;
  position: fixed;
  top: 0;
  left: 0;
  background-color: #111;
  padding-top: 20px;
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: 0.3s;
}

.sidebar ul {
  margin: 40px;
  padding: 0;
}

.sidebar ul li {
  list-style: none;
}

.sidebar a {
  padding: 10px;
  text-decoration: none;
  font-size: 16px;
  color: white;
  display: block;
}

/* Estilos para el enlace activo en la barra lateral */
.sidebar a.active {
  color: #00ff00;
}

.sidebar.closed {
  transform: translateX(-400px);
}

.sidebar button {
  margin: 10px;
  cursor: pointer;
}

.content.closed {
  margin-left: 0;
}

.content {
  margin-left: 260px;
  padding: 16px;
  transition: 0.3s;
}

.section {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.scroll-indicator {
  height: 5px;
  width: 0;
  background-color: #00ff00;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1;
}

.DarkModeBtn {
  margin: 10px;
}

#toggleSidebar {
  position: fixed;
  margin: 20px;
  z-index: 100;
  padding: 5px;
  cursor: pointer;
}
</style>
