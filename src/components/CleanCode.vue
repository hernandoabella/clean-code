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
        principles that extend beyond mere aesthetics.
      </p>

      <p>
        Understanding the purpose and benefits of writing clean code is crucial
        for developers committed to producing high-quality software.
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
      <h1>Code Formatting</h1>
      <p>
        Adhering to consistent indentation and following line length and
        formatting guidelines results in a codebase that is not only visually
        appealing but also easier to understand and maintain.
      </p>
      <p>
        These practices contribute to a more collaborative and efficient
        development process.
      </p>
      <h3>Consistent Indentation</h3>
      <p>
        Consistent indentation enhances code readability and maintainability.
        It's essential to follow a standardized indentation style throughout the
        codebase.
      </p>
      <h3>For example:</h3>
      <pre>
        <code class="language-python"># Inconsistent indentation
def calculate_total(price, quantity):
total = price * quantity
return total

# Consistent indentation (four spaces)
def calculate_total(price, quantity):
    total = price * quantity
    return total</code>
      </pre>

      <h3>Line Length and Formatting Guidelines</h3>
      <p>
        Setting guidelines for line length and code formatting contributes to a
        visually cohesive and easy-to-follow codebase.
      </p>
      <h2>Consider the following practices:</h2>
      <h3>Maximum Line Length:</h3>
      <p>
        Define a maximum line length to prevent excessively long lines. This
        enhances code readability, especially when viewing code side by side.
      </p>
      <h3>For example:</h3>

      <pre>
        <code class="language-python">// Exceeds maximum line length
String message = "This is a long message that goes beyond the recommended line length, and it might make the code harder to read and maintain.";

// Adhering to maximum line length
String message =
        "This is a long message that adheres to the recommended line length, enhancing code readability.";</code>
      </pre>

      <h3>Consistent Formatting:</h3>
      <p>
        Establish consistent formatting rules for elements such as braces,
        parentheses, and operators. This promotes a uniform appearance across
        the codebase.
      </p>
      <h3>For example:</h3>
      <pre>
        <code class="language-python">// Inconsistent formatting of braces
if (condition)
{
    // code
} else {
    // code
}

// Consistent formatting of braces
if (condition) {
    // code
} else {
    // code
}</code>
      </pre>
      <h3>Vertical Alignment:</h3>
      <p>
        Align similar elements vertically to improve code aesthetics. This can
        include aligning assignments or parameters for better readability.
      </p>
      <h3>For example:</h3>
      <pre>
        <code class="language-python"># Inconsistent vertical alignment
variable1 = 10
variable2 = 20
variable3 = 30

# Consistent vertical alignment
variable1   = 10
variable2   = 20
variable3   = 30</code>
      </pre>
    </div>

    <div id="section4" class="section">
      <h1>Comments and Documentation</h1>
      <p>
        Balancing the use of comments with writing self-explanatory code is key
        to creating maintainable and understandable software. Documenting APIs
        and functions ensures that users, including future developers, can
        effectively utilize the codebase.
      </p>
      <h3>When to Use Comments</h3>
      <p>
        Comments should be used judiciously to provide additional context or
        clarification when the code alone may not be self-explanatory. Key
        scenarios for using comments include:
      </p>
      <h3>Complex Algorithms:</h3>
      <p>
        Explain intricate algorithms or non-trivial logic to aid understanding.
      </p>
      <pre>
        <code class="language-python">// Use binary search to find the element efficiently</code>
      </pre>
      <h3>Workarounds or Hacks:</h3>
      <p>
        Clarify temporary solutions or workarounds with comments, and include
        plans for future improvements.
      </p>
      <pre>
        <code class="language-python"># Temporary fix until issue #123 is resolved</code>
      </pre>
      <h3>Edge Cases:</h3>
      <p>Highlight considerations for edge cases or exceptional scenarios.</p>
      <pre>
        <code class="language-python">// Handle edge case where array length is 0</code>
      </pre>
      <h3>Writing Self-Explanatory Code</h3>
      <p>
        Prioritize writing code that is inherently clear and self-explanatory
        without relying heavily on comments.
      </p>
      <p>Techniques for achieving self-explanatory code include:</p>
      <h3>Descriptive Naming:</h3>
      <p>
        Use meaningful and descriptive names for variables, functions, and
        classes.
      </p>
      <pre>
        <code class="language-python">// Non-descriptive variable
int x = 5;

// Descriptive variable name
int numberOfStudents = 5;</code>
      </pre>
      <h3>Modularization:</h3>
      <p>
        Break down complex tasks into smaller, modular functions with clear
        purposes.
      </p>
      <pre>
        <code class="language-python"># Non-modularized code
result = process_data(data)

# Modularized code
result = calculate_statistics(data)</code>
      </pre>
      <h3>Consistent Coding Style:</h3>
      <p>
        Adhere to a consistent coding style, making the codebase predictable and
        easy to follow.
      </p>
      <pre>
        <code class="language-python">// Inconsistent coding style
if (condition) return true;

// Consistent coding style
if (condition) {
    return true;
}</code>
      </pre>

      <h3>Documenting APIs and Functions</h3>
      <p>
        Comprehensive documentation is crucial for APIs and functions to guide
        users on their usage. Include the following information:
      </p>
      <h3>Function/Method Purpose:</h3>
      <p>
        Describe the overall purpose and functionality of the API or function.
      </p>
      <pre>
        <code class="language-python">/**
 * Retrieves the user details based on the provided user ID.
 * @param userId The unique identifier of the user.
 * @return User object containing user details.
 */</code>
      </pre>

      <h3>Parameters:</h3>
      <p>
        Document each parameter, specifying its type, purpose, and any
        constraints.
      </p>
      <pre>
        <code class="language-python">def calculate_discount(price, discount_percentage):
    """
    Calculates the discounted price based on the original price and discount percentage.
    :param price: The original price of the item.
    :param discount_percentage: The percentage of discount to be applied.
    :return: The discounted price.
    """</code>
      </pre>
      <h3>Return Values:</h3>
      <p>Clearly state the type and meaning of the return values.</p>
      <pre>
        <code class="language-python">/**
 * Validates the user input and returns a boolean indicating whether it is valid.
 * @param userInput The input provided by the user.
 * @return {boolean} True if the input is valid, false otherwise.
 */</code>
      </pre>
    </div>

    <div id="section5" class="section">
      <h1>Functions and Methods</h1>
      <p>
        Adhering to the Single Responsibility Principle ensures that functions
        and methods are focused and easier to understand, while minimizing side
        effects contributes to code that is more predictable and maintainable.
      </p>
      <h3>Single Responsibility Principle</h3>
      <p>
        Adhering to the Single Responsibility Principle (SRP) ensures that each
        function or method has a clear, singular purpose. This enhances code
        clarity and maintainability:
      </p>
      <h3>Clear Purpose:</h3>
      <p>Define functions to perform one specific task or responsibility.</p>
      <pre>
        <code class="language-python">// Violating SRP
public void processOrderAndSendEmail(Order order) {
    // Code to process order
    // Code to send email
}

// Adhering to SRP
public void processOrder(Order order) {
    // Code to process order
}

public void sendOrderConfirmationEmail(Order order) {
    // Code to send email
}</code>
      </pre>
      <h3>Modularization:</h3>
      <p>
        Break down complex tasks into smaller, focused functions, each
        responsible for a specific aspect.
      </p>
      <pre>
        <code class="language-python"># Violating SRP
def process_data(data):
    # Code to process data
    # Code to update database
    # Code to send notifications

# Adhering to SRP
def process_data(data):
    # Code to process data

def update_database(data):
    # Code to update database

def send_notifications(data):
    # Code to send notifications</code>
      </pre>
      <h3>Avoiding Side Effects</h3>
      <p>
        Functions and methods should avoid unintended side effects to enhance
        predictability and maintainability:
      </p>
      <h3>Pure Functions:</h3>
      <p>
        Strive for functions that produce the same output for the same input and
        have no side effects.
      </p>
      <pre>
        <code class="language-python">// Function with side effect
let total = 0;

function addToTotal(value) {
    total += value;
    return total;
}

// Pure function
function addNumbers(a, b) {
    return a + b;
}</code>
      </pre>
      <h3>Separation of Concerns:</h3>
      <p>
        Clearly separate functions that modify state from those that return
        values without side effects.
      </p>
      <pre>
        <code class="language-python">// Function with side effect
public void updateDatabaseRecord(int recordId, string newData) {
    // Code to update database
}

// Function without side effect
public string retrieveDataFromDatabase(int recordId) {
    // Code to retrieve data from database
    return data;
}</code>
      </pre>
      <h3>Optimal Function and Method Length</h3>
      <p>
        Striking a balance between function length and clarity is crucial for
        readability and maintainability:
      </p>
      <h3>Conciseness:</h3>
      <p>
        Keep functions and methods concise, focusing on a single responsibility.
        Aim for a few lines of code whenever possible.
      </p>
      <pre>
        <code class="language-python"># Long method violating optimal length
def process_data(data):
    # Code...
    # More code...
    # Even more code...

# Short, focused method adhering to optimal length
def process_data(data):
    # Code...</code>
      </pre>
      <h3>Meaningful Names:</h3>
      <p>
        If a function must be longer, ensure it remains understandable and
        well-organized. Use meaningful names for variables and sections of code.
      </p>
      <pre>
        <code class="language-python">// Long method with unclear structure
public void processCustomerOrder(Order order) {
    // Code...
    // More code...
    // Even more code...
}

// Longer method with clear structure
public void processCustomerOrder(Order order) {
    validateOrder(order);
    calculateTotal(order);
    applyDiscounts(order);
    generateInvoice(order);
}</code>
      </pre>
    </div>

    <div id="section6" class="section">
      <h1>Variables and Constants</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section7" class="section">
      <h1>Code Duplication</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section8" class="section">
      <h1>Error Handling</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section9" class="section">
      <h1>Testing</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section10" class="section">
      <h1>Version Control and Branching</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section11" class="section">
      <h1>Code Reviews</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section12" class="section">
      <h1>Continuos Integration</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section13" class="section">
      <h1>Performance</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section14" class="section">
      <h1>Security</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section15" class="section">
      <h1>Tools and Linters</h1>
      <p>Contenido de la sección 2...</p>
    </div>

    <div id="section16" class="section">
      <h1>Conclusion</h1>
      <p>Contenido de la sección 2...</p>
    </div>
  </div>

  <div class="scroll-indicator"></div>
</template>
