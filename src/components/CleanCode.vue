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
    behavior: "smooth",
  });
}

function toggleSidebar() {
  const sidebar = document.querySelector(".sidebar");
  const content = document.querySelector(".content");
  sidebar.classList.toggle("closed");
  content.classList.toggle("closed");
}

function getHeaderHeight() {
  return document.querySelector("header").offsetHeight;
}

function getMargin() {
  return 40;
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
        <a href="#section16" class="nav-link" data-target="section16"
          >Conclusion
        </a>
      </li>
    </ul>
  </div>

  <div class="content">
    <div id="section1" class="section">
      <h1>Introduction</h1>
      <p>
        Clean code is a fundamental aspect of software development, embodying
        principles that extend beyond mere aesthetics. Understanding the purpose
        and benefits of writing clean code is crucial for developers committed
        to producing high-quality software.
      </p>

      <h3>The primary purposes include:</h3>
      <p>
        The purpose of clean code serve as a model for creating software that is
        not only functional but also maintainable and understandable.
      </p>

      <ul>
        <li>
          <b>Readability:</b> Clean code is easy to read and comprehend,
          fostering collaboration among team members and simplifying the
          onboarding process for new developers.
        </li>
        <li>
          <b>Maintainability:</b> Well-organized and properly documented code
          facilitates easier maintenance and updates, reducing the likelihood of
          introducing bugs during modifications.
        </li>
        <li>
          <b>Scalability:</b> Clean code adapts to the evolving needs of a
          project, ensuring that as it grows, it remains flexible and scalable
          without sacrificing stability.
        </li>
      </ul>

      <h3>Benefits of Writing Clean Code</h3>
      <p>
        Writing clean code yields a variety of advantages, impacting both
        individual developers and the overall development process:
      </p>
      <ul>
        <li>
          <b>Reduced Bugs:</b> Clean code minimizes the chances of introducing
          errors and makes it easier to identify and fix bugs when they do
          occur.
        </li>
        <li>
          <b>Enhanced Collaboration:</b> Teams can collaborate more effectively
          when the code is clean and follows consistent conventions, leading to
          increased productivity.
        </li>
        <li>
          <b>Faster Development:</b> Reading and understanding clean code is
          quicker, allowing developers to work more efficiently and deliver
          features faster.
        </li>
        <li>
          <b>Code Longevity:</b> Clean code is more likely to stand the test of
          time, remaining relevant and adaptable to future changes in
          requirements.
        </li>
      </ul>
    </div>

    <div id="section2" class="section">
      <h1>Naming Conventions</h1>
      <p>
        Adhering to descriptive and consistent naming conventions fosters a
        codebase that is not only easy to understand but also enjoyable to work
        with. These principles lay the groundwork for effective communication
        within the development team and contribute to the overall
        maintainability of the software.
      </p>
      <h3>Descriptive and Meaningful Names</h3>
      <p>
        Choosing names that concisely convey the purpose and functionality of
        variables, functions, and classes is paramount. This promotes clarity
        and understanding within the codebase, enhancing readability and
        maintainability.
      </p>
      <p>Key considerations include:</p>
      <p>
        <b> Avoiding Ambiguity:</b> Names should be unambiguous, leaving little
        room for misinterpretation.
      </p>
      <h4>For example:</h4>
      <pre>
        <code class="language-python"># Unclear variable name
x = 10

# Improved, descriptive name
num_of_items = 10  
        </code>
      </pre>
      Context Awareness: Consider the broader context of the code when selecting
      names. Names should align with the purpose of the surrounding code. For
      example:
      <pre>
        <code class="language-python">// Unclear method name
public void process() {
    // ...
}

// Improved, context-aware name
public void processOrder() {
    // ...
} 
        </code>
      </pre>
      Consistency: Strive for consistency in naming conventions throughout the
      project. Consistent naming makes the codebase more predictable and
      user-friendly. For example:
      <pre>
        <code class="language-python">// Variables using different naming styles
let userName = "John";
let user_age = 25;

// Consistent naming styles
let userName = "John";
let userAge = 25;
        </code>
      </pre>
      Consistent Naming Styles Enforcing a consistent naming style across the
      entire codebase ensures a unified and cohesive development experience.
      Guidelines for maintaining consistent naming styles include: CamelCase or
      Snake_case: Choose a specific convention (e.g., CamelCase or snake_case)
      and adhere to it consistently. This applies to variables, functions, and
      other identifiers. For example:
      <pre>
        <code class="language-python"># Inconsistent naming styles
user_name = "Alice"
getUserName = function() {
    // ...
}

# Consistent snake_case style
user_name = "Alice"
get_user_name = function() {
    // ...
}
        </code>
      </pre>

      Use of Abbreviations: If abbreviations are necessary, establish
      conventions for their usage. Consistency in abbreviation styles avoids
      confusion. For example:
      <pre>
        <code class="language-python">// Inconsistent abbreviation styles
int num_of_elements = 10;
String employeeID = "E123";

// Consistent abbreviation style
int numOfElements = 10;
String employeeId = "E123";</code>
      </pre>
      Namespace Clarity: Ensure that names reflect their appropriate namespaces,
      preventing naming collisions and contributing to a more organized code
      structure. For example:

      <pre>
        <code class="language-python">// Unclear namespace in class name
public class DatabaseHandler {
    // ...
}

// Improved with namespace clarity
public class DataAccessHandler {
    // ...
}</code>
      </pre>

      Follow Language Conventions: Adhere to the naming conventions recommended
      by the programming language being used. Consistency with language-specific
      norms promotes code familiarity. For example:
      <pre>
        <code class="language-python">// Inconsistent naming with TypeScript conventions
let User_Name = "John";
function getUserInfo() {
    // ...
}

// Consistent with TypeScript conventions
let userName = "John";
function getUserInfo() {
    // ...
}</code>
      </pre>
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
