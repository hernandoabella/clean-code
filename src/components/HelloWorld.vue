<script setup>
import { onMounted, ref } from 'vue';

// Define a reactive variable for dark mode
const isDarkMode = ref(false);

// Run the JavaScript logic after the component is mounted
onMounted(() => {
  // Check the local storage for dark mode preference
  const storedDarkMode = localStorage.getItem('darkMode');
  if (storedDarkMode === 'enabled') {
    document.body.classList.add('dark-mode');
    isDarkMode.value = true;
  }

  window.onscroll = function () {
    scrollIndicator();
  };

  const darkModeToggle = document.getElementById('darkModeToggle');
  darkModeToggle.addEventListener('click', toggleDarkMode);

  const darkModeIcon = document.getElementById('darkModeIcon');

  function toggleDarkMode() {
    document.body.classList.toggle('dark-mode');
    isDarkMode.value = !isDarkMode.value;

    // Change the icon class when toggling dark mode
    if (isDarkMode.value) {
      darkModeIcon.classList.remove('fa-moon');
      darkModeIcon.classList.add('fa-sun');
      localStorage.setItem('darkMode', 'enabled');
    } else {
      darkModeIcon.classList.remove('fa-sun');
      darkModeIcon.classList.add('fa-moon');
      localStorage.setItem('darkMode', 'disabled');
    }
  }

  // Get all navigation links
  const navLinks = document.querySelectorAll('.nav-link');

  // Assign click events to links to highlight the active section
  navLinks.forEach(link => {
    link.addEventListener('click', function (event) {
      event.preventDefault();
      const targetId = this.getAttribute('data-target');
      const targetSection = document.getElementById(targetId);
      scrollToSection(targetSection);
    });
  });

  // Function to highlight the active section while scrolling
  function scrollIndicator() {
    let winScroll = document.body.scrollTop || document.documentElement.scrollTop;
    let height = document.documentElement.scrollHeight - document.documentElement.clientHeight;

    navLinks.forEach(link => {
      const targetId = link.getAttribute('data-target');
      const targetSection = document.getElementById(targetId);

      if (targetSection.offsetTop <= winScroll && targetSection.offsetTop + targetSection.offsetHeight > winScroll) {
        link.classList.add('active');
      } else {
        link.classList.remove('active');
      }
    });

    let scrolled = (winScroll / height) * 100;
    document.querySelector('.scroll-indicator').style.width = scrolled + '%';
  }

  // Function to scroll to a section when clicking a link
  function scrollToSection(targetSection) {
    window.scrollTo({
      top: targetSection.offsetTop,
      behavior: 'smooth',
    });
  }

  // Function to toggle dark mode
  function toggleDarkMode() {
    document.body.classList.toggle('dark-mode');
    isDarkMode.value = !isDarkMode.value;

    // Save user preference in local storage
    if (isDarkMode.value) {
      localStorage.setItem('darkMode', 'enabled');
    } else {
      localStorage.setItem('darkMode', 'disabled');
    }
  }

  const toggleSidebarButton = document.getElementById('toggleSidebar');
  toggleSidebarButton.addEventListener('click', toggleSidebar);

  function toggleSidebar() {
    const sidebar = document.querySelector('.sidebar');
    const content = document.querySelector('.content');
    sidebar.classList.toggle('closed');
    content.classList.toggle('closed');
  }
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
