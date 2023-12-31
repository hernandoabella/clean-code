<script setup>
import { onMounted, ref } from 'vue';

const isDarkMode = ref(false);

onMounted(() => {
  const storedDarkMode = localStorage.getItem('darkMode');
  if (storedDarkMode === 'enabled') {
    toggleDarkMode(true);
  }

  window.addEventListener('scroll', scrollIndicator);

  const darkModeToggle = document.getElementById('darkModeToggle');
  darkModeToggle.addEventListener('click', () => toggleDarkMode());

  const darkModeIcon = document.getElementById('darkModeIcon');

  const navLinks = document.querySelectorAll('.nav-link');
  navLinks.forEach(link => {
    link.addEventListener('click', event => {
      event.preventDefault();
      const targetId = link.getAttribute('data-target');
      const targetSection = document.getElementById(targetId);
      scrollToSection(targetSection);
    });
  });

  const toggleSidebarButton = document.getElementById('toggleSidebar');
  toggleSidebarButton.addEventListener('click', toggleSidebar);
});

function toggleDarkMode(forceToggle) {
  document.body.classList.toggle('dark-mode', forceToggle ?? !isDarkMode.value);
  isDarkMode.value = !isDarkMode.value;

  const iconClassToAdd = isDarkMode.value ? 'fa-sun' : 'fa-moon';
  const iconClassToRemove = isDarkMode.value ? 'fa-moon' : 'fa-sun';

  const darkModeIcon = document.getElementById('darkModeIcon');
  darkModeIcon.classList.remove(iconClassToRemove);
  darkModeIcon.classList.add(iconClassToAdd);

  localStorage.setItem('darkMode', isDarkMode.value ? 'enabled' : 'disabled');
}

function scrollIndicator() {
  let winScroll = document.body.scrollTop || document.documentElement.scrollTop;
  let height = document.documentElement.scrollHeight - document.documentElement.clientHeight;

  const navLinks = document.querySelectorAll('.nav-link');
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

function scrollToSection(targetSection) {
  window.scrollTo({
    top: targetSection.offsetTop,
    behavior: 'smooth',
  });
}

function toggleSidebar() {
  const sidebar = document.querySelector('.sidebar');
  const content = document.querySelector('.content');
  sidebar.classList.toggle('closed');
  content.classList.toggle('closed');
}
</script>

<template>
  <button id="toggleSidebar"><i class="fa-solid fa-bars"></i></button>
  <div class="sidebar">
    <ul>
      <li>
        <a href="#section1" class="nav-link active" data-target="section1">Sección 1</a>
      </li>
      <li>
        <a href="#section2" class="nav-link" data-target="section2">Sección 2</a>
      </li>
    </ul>
    <button class="DarkModeBtn" id="darkModeToggle">
      <i id="darkModeIcon" class="fas fa-moon"></i>
    </button>
  </div>

  <div class="content">
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