<script setup>
import { onMounted, ref } from "vue";

const isDarkMode = ref(false);

onMounted(() => {
  initializeDarkMode();
  initializeScroll();
  initializeNavLinks();
  initializeSidebar();
});

function initializeDarkMode() {
  const storedDarkMode = localStorage.getItem("darkMode");
  if (storedDarkMode === "enabled") {
    toggleDarkMode(true);
  }

  const darkModeToggle = document.getElementById("darkModeToggle");
  darkModeToggle.addEventListener("click", () => toggleDarkMode());
}

function initializeScroll() {
  window.addEventListener("scroll", scrollIndicator);
}

function initializeNavLinks() {
  const navLinks = document.querySelectorAll(".nav-link");
  navLinks.forEach((link) => {
    link.addEventListener("click", (event) => {
      event.preventDefault();
      const targetId = link.getAttribute("data-target");
      const targetSection = document.getElementById(targetId);
      scrollToSection(targetSection);
    });
  });
}

function initializeSidebar() {
  const toggleSidebarButton = document.getElementById("toggleSidebar");
  toggleSidebarButton.addEventListener("click", toggleSidebar);
}

function toggleDarkMode(forceToggle) {
  document.body.classList.toggle("dark-mode", forceToggle ?? !isDarkMode.value);
  isDarkMode.value = !isDarkMode.value;

  const iconClassToAdd = isDarkMode.value ? "fa-sun" : "fa-moon";
  const iconClassToRemove = isDarkMode.value ? "fa-moon" : "fa-sun";

  const darkModeIcon = document.getElementById("darkModeIcon");
  darkModeIcon.classList.remove(iconClassToRemove);
  darkModeIcon.classList.add(iconClassToAdd);

  localStorage.setItem("darkMode", isDarkMode.value ? "enabled" : "disabled");
}

function scrollIndicator() {
  const sections = document.querySelectorAll(".section");
  const winScroll = window.scrollY || window.pageYOffset;
  const height = document.documentElement.scrollHeight - window.innerHeight;

  let activeSection = null;

  sections.forEach((section) => {
    const sectionTop = section.offsetTop - getHeaderHeight() - getMargin();
    const sectionBottom = sectionTop + section.offsetHeight;

    if (winScroll >= sectionTop && winScroll < sectionBottom) {
      activeSection = section;
    }
  });

  updateNavLinksActiveState(activeSection);

  // Resto de la función scrollIndicator
  let scrolled = (winScroll / height) * 100;
  document.querySelector(".scroll-indicator").style.width = scrolled + "%";
}

function scrollToSection(targetSection) {
  window.scrollTo({
    top: targetSection.offsetTop - getHeaderHeight() - getMargin(),
    behavior: 'smooth',
  });
}

function toggleSidebar() {
  const sidebar = document.querySelector(".sidebar");
  const content = document.querySelector(".content");
  sidebar.classList.toggle("closed");
  content.classList.toggle("closed");
}

function getHeaderHeight() {
  return document.querySelector('header').offsetHeight;
}

function getMargin() {
  return 30; // Puedes ajustar este valor según sea necesario
}

function updateNavLinksActiveState(activeSection) {
  const navLinks = document.querySelectorAll(".nav-link");
  navLinks.forEach((link) => {
    const targetId = link.getAttribute("data-target");
    const targetSection = document.getElementById(targetId);

    if (targetSection === activeSection) {
      link.classList.add("active");
    } else {
      link.classList.remove("active");
    }
  });
}
</script>


<template>
  <header>
    <div class="header-container">
      <div>
        <button id="toggleSidebar" @click="toggleSidebarMobile">
          <i class="fa-solid fa-bars"></i>
        </button>
      </div>
      <div class="logo">Clean Code</div>
      <div class="header-right-elements">
        <div>
          <a
            href="https://github.com/hernandoabella/clean-code"
            target="_blank"
            class="github"
            ><i class="fa-brands fa-github"></i
          ></a>
        </div>
        <div>
          <button class="DarkModeBtn" id="darkModeToggle">
            <i id="darkModeIcon" class="fas fa-moon"></i>
          </button>
        </div>
      </div>
    </div>
  </header>

  <div class="sidebar">
    <ul>
      <li>
        <a href="#section1" class="nav-link active" data-target="section1"
          >Introduction</a
        >
      </li>
      <li>
        <a href="#section2" class="nav-link" data-target="section2"
          >Naming Conventions
        </a>
      </li>
      <li>
        <a href="#section3" class="nav-link" data-target="section3"
          >Code Formatting
        </a>
      </li>
      <li>
        <a href="#section4" class="nav-link" data-target="section4"
          >Comments and Documentation
        </a>
      </li>
      <li>
        <a href="#section5" class="nav-link" data-target="section5"
          >Functions and Methods
        </a>
      </li>
      <li>
        <a href="#section6" class="nav-link" data-target="section6"
          >Variables and Constants
        </a>
      </li>
      <li>
        <a href="#section7" class="nav-link" data-target="section7"
          >Code Duplication
        </a>
      </li>
      <li>
        <a href="#section8" class="nav-link" data-target="section8"
          >Error Handling
        </a>
      </li>
      <li>
        <a href="#section9" class="nav-link" data-target="section9">Testing </a>
      </li>
      <li>
        <a href="#section10" class="nav-link" data-target="section10"
          >Version Control and Branching
        </a>
      </li>
      <li>
        <a href="#section11" class="nav-link" data-target="section11"
          >Code Reviews
        </a>
      </li>
      <li>
        <a href="#section12" class="nav-link" data-target="section12"
          >Continuous Integration
        </a>
      </li>
      <li>
        <a href="#section13" class="nav-link" data-target="section13"
          >Performance
        </a>
      </li>
      <li>
        <a href="#section14" class="nav-link" data-target="section14"
          >Security
        </a>
      </li>
      <li>
        <a href="#section15" class="nav-link" data-target="section15"
          >Tools and Linters
        </a>
      </li>
      <li>
        <a href="#section15" class="nav-link" data-target="section15"
          >Conclusion
        </a>
      </li>
    </ul>
  </div>

  <div class="content">
    <div id="section1" class="section">
      <h1>Sección 1</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section2" class="section">
      <h1>Sección 2</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section3" class="section">
      <h1>Sección 3</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section4" class="section">
      <h1>Sección 4</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section5" class="section">
      <h1>Sección 5</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section6" class="section">
      <h1>Sección 6</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section7" class="section">
      <h1>Sección 7</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section8" class="section">
      <h1>Sección 8</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section9" class="section">
      <h1>Sección 9</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section10" class="section">
      <h1>Sección 10</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section11" class="section">
      <h1>Sección 11</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section12" class="section">
      <h1>Sección 12</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section13" class="section">
      <h1>Sección 13</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section14" class="section">
      <h1>Sección 14</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section15" class="section">
      <h1>Sección 15</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section16" class="section">
      <h1>Sección 16</h1>
      <p>Contenido de la sección 2...</p>
    </div>
  </div>

  <div class="scroll-indicator"></div>
</template>
