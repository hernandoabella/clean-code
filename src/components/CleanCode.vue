<script setup>
import { onMounted, ref } from "vue";

const isDarkMode = ref(false);

onMounted(() => {
  const storedDarkMode = localStorage.getItem("darkMode");
  if (storedDarkMode === "enabled") {
    toggleDarkMode(true);
  }

  window.addEventListener("scroll", scrollIndicator);

  const darkModeToggle = document.getElementById("darkModeToggle");
  darkModeToggle.addEventListener("click", () => toggleDarkMode());

  const darkModeIcon = document.getElementById("darkModeIcon");

  const navLinks = document.querySelectorAll(".nav-link");
  navLinks.forEach((link) => {
    link.addEventListener("click", (event) => {
      event.preventDefault();
      const targetId = link.getAttribute("data-target");
      const targetSection = document.getElementById(targetId);
      scrollToSection(targetSection);
    });
  });

  const toggleSidebarButton = document.getElementById("toggleSidebar");
  toggleSidebarButton.addEventListener("click", toggleSidebar);
});

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
  let winScroll = document.body.scrollTop || document.documentElement.scrollTop;
  let height =
    document.documentElement.scrollHeight -
    document.documentElement.clientHeight;

  const navLinks = document.querySelectorAll(".nav-link");
  navLinks.forEach((link) => {
    const targetId = link.getAttribute("data-target");
    const targetSection = document.getElementById(targetId);

    if (
      targetSection.offsetTop <= winScroll &&
      targetSection.offsetTop + targetSection.offsetHeight > winScroll
    ) {
      link.classList.add("active");
    } else {
      link.classList.remove("active");
    }
  });

  let scrolled = (winScroll / height) * 100;
  document.querySelector(".scroll-indicator").style.width = scrolled + "%";
}

function scrollToSection(targetSection) {
  window.scrollTo({
    top: targetSection.offsetTop,
    behavior: "smooth",
  });
}

function toggleSidebar() {
  const sidebar = document.querySelector(".sidebar");
  const content = document.querySelector(".content");
  sidebar.classList.toggle("closed");
  content.classList.toggle("closed");
}
</script>

<template>
  <button id="toggleSidebar"><i class="fa-solid fa-bars"></i></button>
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
    </ul>
   
  </div>

  <div class="content">
    <div id="section1" class="section">
      <h1>Introduction</h1>
      <p>Contenido de la sección 1...</p>
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

     <button class="DarkModeBtn" id="darkModeToggle">
      <i id="darkModeIcon" class="fas fa-moon"></i>
    </button>

  </div>

  <div class="scroll-indicator"></div>
  
</template>