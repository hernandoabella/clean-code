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
      <div>
        <div class="logo">🧹✨Clean Code🧼🧽</div>
      </div>

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
      <div>
        <img src="/cleancode.jpg" alt="clean-code-image" />
      </div>
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
      <p>
        Meaningful variable names and proper use of constants contribute to code
        that is easier to understand, maintain, and collaborate on. Consistent
        naming conventions help create a more cohesive and readable codebase.
      </p>
      <h3>Meaningful Variable Names</h3>
      <p>
        Choosing meaningful and descriptive variable names is essential for code
        clarity and maintainability:
      </p>
      <h3>Descriptive Naming:</h3>
      <p>Use names that clearly convey the purpose of the variable.</p>
      <pre>
        <code class="language-python"># Unclear variable name
x = 10

# Descriptive variable name
num_of_items = 10</code>
      </pre>
      <h3>Avoiding Ambiguity:</h3>
      <p>
        Ensure variable names are unambiguous and leave little room for
        misinterpretation.
      </p>
      <pre>
        <code class="language-python">// Unclear variable name
int result = calculate();

// Descriptive variable name
int totalSum = calculateTotal();</code>
      </pre>
      <h3>Consistency:</h3>
      <p>
        Strive for consistency in naming conventions throughout the project.
      </p>
      <pre>
        <code class="language-python">// Variables using different naming styles
let userName = "John";
let user_age = 25;

// Consistent naming styles
let userName = "John";
let userAge = 25;</code>
      </pre>

      <h3>Proper Use of Constants</h3>
      <p>Constants provide a way to represent fixed values with clear names:</p>
      <h3>Naming Convention:</h3>
      <p>
        Use uppercase letters and underscores to distinguish constants from
        variables.
      </p>
      <pre>
        <code class="language-python">// Unclear constant name
const int value = 100;

// Proper constant naming
const int MAX_VALUE = 100;</code>
      </pre>
      <h3>Logical Grouping:</h3>
      <p>Organize related constants together to enhance code organization.</p>
      <pre>
        <code class="language-python"># Unclear organization of constants
const int WIDTH = 800;
const int HEIGHT = 600;

# Organized constants
const int SCREEN_WIDTH = 800;
const int SCREEN_HEIGHT = 600;</code>
      </pre>
      <h3>Avoiding Magic Numbers:</h3>
      <p>
        Replace magic numbers with named constants to improve code readability.
      </p>
      <pre>
        <code class="language-python">// Magic number without context
double result = calculateArea(5);

// Named constant providing context
final double SIDE_LENGTH = 5;
double result = calculateArea(SIDE_LENGTH);</code>
      </pre>
    </div>

    <div id="section7" class="section">
      <h1>Code Duplication</h1>
      <p>
        Applying the DRY principle and employing refactoring techniques help
        create a codebase that is more maintainable, extensible, and less prone
        to errors. Regularly reviewing and addressing duplication enhances
        overall code quality.
      </p>
      <h3>DRY Principle (Don't Repeat Yourself)</h3>
      <p>
        The DRY principle emphasizes the importance of avoiding redundant code
        by promoting code reusability:
      </p>
      <h3>Identifying Redundancy:</h3>
      <p>
        Recognize duplicated code segments that perform similar or identical
        tasks.
      </p>
      <pre>
        <code class="language-python"># Duplicated code
def calculate_area_of_square(side_length):
    return side_length * side_length

def calculate_volume_of_cube(side_length):
    return side_length * side_length * side_length</code>
      </pre>
      <h3>Extracting Common Functionality:</h3>
      <p>Create reusable functions or methods to encapsulate common logic.</p>
      <pre>
        <code class="language-python">// DRY principle applied
public double calculateArea(double sideLength) {
    return sideLength * sideLength;
}

public double calculateVolume(double sideLength) {
    return sideLength * sideLength * sideLength;</code>
      </pre>
      <h3>Utilizing Functions:</h3>
      <p>Maximize the use of existing functions to avoid duplicating logic.</p>
      <pre>
        <code class="language-python">// Duplicated logic
let total = calculateSum(array1) + calculateSum(array2);

// Reusing existing function
let total = calculateSum(array1.concat(array2));</code>
      </pre>

      <h3>Refactoring Techniques</h3>
      <p>
        Refactoring involves restructuring existing code to improve its
        readability, maintainability, and performance:
      </p>
      <h3>Extract Method/Function:</h3>
      <p>Break down large methods into smaller, more focused ones.</p>
      <pre>
        <code class="language-python"># Original method
def process_data(data):
    # Code...
    # More code...
    # Even more code...

# Refactored using extracted functions
def process_data(data):
    process_part1(data)
    process_part2(data)
    
def process_part1(data):
    # Code...
    
def process_part2(data):
    # More code...</code>
      </pre>
      <h3>Template Method Pattern:</h3>
      <p>
        Identify common patterns and create template methods for shared
        functionality.
      </p>
      <pre>
        <code class="language-csharp">// Without template method pattern
public void processOrder(Order order) {
    validateOrder(order);
    calculateTotal(order);
    applyDiscounts(order);
    generateInvoice(order);
}

// Using template method pattern
public void processOrder(Order order) {
    processOrderTemplate(order);
}

public abstract void processOrderTemplate(Order order);</code>
      </pre>

      <h3>Code Reviews:</h3>
      <p>
        Regularly conduct code reviews to identify and address duplicated code
        collaboratively.
      </p>
      <pre>
        <code class="language-csharp">// Identifying duplicated code during a code review
// ...

// Collaborative refactoring to eliminate duplication
// ...</code>
      </pre>
      <h3>Automated Tools:</h3>
      <p>
        Utilize code analysis tools and IDE features to detect and suggest
        refactorings for duplicated code.
      </p>

      <ul>
        <li>
          <a href="https://www.jetbrains.com/resharper/"
            >JetBrains ReSharper:</a
          >
          ReSharper provides a set of refactorings that analyze the selected
          code to provide insights and then update the existing code based on
          those insights. It includes a wide range of refactoring options such
          as extracting superclass, introducing parameters, changing signatures,
          and more.
        </li>
        <li>
          <a
            href="https://marketplace.visualstudio.com/items?itemName=SteveCadwallader.CodeMaid"
            >CodeMaid:</a
          >
          CodeMaid is a Visual Studio extension that supports languages such as
          C#, C++, F#, JSON, JavaScript, TypeScript, XML, HTML, PHP, PowerShell,
          VB, and R. It can remove random white space from your code, which
          helps to improve code readability and maintainability.
        </li>
        <li>
          <a href="https://pmd.github.io/pmd/pmd_userdocs_cpd"
            >PMD/CPD (Copy/Paste Detector):</a
          >
          PMD is a source code analyzer that can find duplicated code blocks. It
          supports multiple languages and can be run via command-line, Ant task,
          or Maven plugin. It is useful for finding duplicated code and
          suggesting refactorings to eliminate those duplications.
        </li>
        <li>
          <a href="https://refactoring.guru/">Refactoring Guru:</a> Refactoring
          Guru provides information and guidance on various refactoring
          techniques. It explains how to identify and eliminate duplicate code,
          as well as how to refactor code to make it more efficient and
          maintainable.
        </li>
      </ul>
    </div>

    <div id="section8" class="section">
      <h1>Error Handling</h1>
      <p>
        Properly handling exceptions, logging relevant information, and
        utilizing debugging tools contribute to a more resilient and
        maintainable codebase. Regularly reviewing and refining error-handling
        strategies enhances the overall reliability of the software.
      </p>
      <h2>Proper Exception Handling</h2>
      <p>
        Proper exception handling is crucial for writing robust and reliable
        code:
      </p>
      <h3>Catch Specific Exceptions:</h3>
      <p>
        Catch specific exceptions rather than using broad catch-all statements.
      </p>
      <pre>
        <code class="language-csharp">// Without template method pattern
public void processOrder(Order order) {
    validateOrder(order);
    calculateTotal(order);
    applyDiscounts(order);
    generateInvoice(order);
}

// Using template method pattern
public void processOrder(Order order) {
    processOrderTemplate(order);
}

public abstract void processOrderTemplate(Order order);</code>
      </pre>
      <h3>Graceful Degradation:</h3>
      <p>
        Provide meaningful error messages and gracefully degrade when an
        exception occurs.
      </p>
      <pre>
        <code class="language-python"># Inadequate error message
try:
    # Code...
except ValueError:
    print("Error occurred.")

# Improved error message
try:
    # Code...
except ValueError as e:
    print(f"Error: {e}")</code>
      </pre>
      <h3>Logging Exceptions:</h3>
      <p>Log exceptions to aid in debugging and issue resolution.</p>
      <pre>
        <code class="language-csharp">// Logging exception without details
try {
    // Code...
} catch (error) {
    console.error("An error occurred.");
}

// Logging exception with details
try {
    // Code...
} catch (error) {
    console.error(`An error occurred: ${error.message}`);
}</code>
      </pre>

      <h2>Logging and Debugging</h2>
      <p>
        Effective logging and debugging practices help identify and resolve
        issues:
      </p>

      <h3>Logging Levels:</h3>
      <p>
        Use different logging levels (e.g., debug, info, error) to provide
        varying levels of detail.
      </p>
      <pre>
        <code class="language-csharp">// Logging at different levels
log.Debug("Debug information.");
log.Info("Informational message.");
log.Error("Error occurred: " + exception.Message);</code>
      </pre>

      <h3>Contextual Logging:</h3>
      <p>
        Include relevant context information in log messages for better
        understanding.
      </p>
      <pre>
        <code class="language-csharp">// Contextual logging
logger.error(`Error processing order ${orderId}: ${error.message}`);</code>
      </pre>

      <h3>Debugging Tools:</h3>
      <p>
        Utilize debugging tools provided by integrated development environments
        (IDEs) or dedicated debugging tools.
      </p>
      <pre>
        <code class="language-python"># Setting breakpoints for debugging
def calculate_total(price, quantity):
    # Code...
    result = price * quantity  # Set breakpoint here
    # More code...
    return result</code>
      </pre>
      <h3>Unit Testing:</h3>
      <p>
        Implement comprehensive unit tests to identify and fix issues early in
        the development process.
      </p>
      <pre>
        <code class="language-python">// Unit test for exception handling
@Test(expected = IOException.class)
public void testFileReadException() throws IOException {
    // Code that should throw an IOException
}</code>
      </pre>
    </div>

    <div id="section9" class="section">
      <h1>Testing</h1>
      <p>
        Writing testable code enhances the efficiency of the testing process and
        contributes to the overall reliability of the software. It encourages
        good software design practices, making it easier to identify and address
        issues throughout the development lifecycle.
      </p>
      <h3>Importance of Unit Testing</h3>
      <p>
        Unit testing plays a crucial role in ensuring the reliability and
        maintainability of software:
      </p>
      <h3>Early Issue Detection:</h3>
      <p>
        Unit tests identify issues at an early stage of development, preventing
        the propagation of bugs to later stages.
      </p>
      <h3>Code Confidence:</h3>
      <p>
        Successful unit tests provide developers with confidence that their code
        functions as intended.
      </p>
      <h3>Regression Prevention:</h3>
      <p>
        Unit tests act as a safety net, preventing the introduction of new bugs
        during code modifications.
      </p>
      <h3>Documentation:</h3>
      <p>
        Unit tests serve as living documentation, illustrating how specific
        components of the code are expected to behave.
      </p>
      <pre>
        <code class="language-python">// Example of a simple JUnit test
@Test
public void testAddition() {
    Calculator calculator = new Calculator();
    int result = calculator.add(2, 3);
    assertEquals(5, result);
}</code>
      </pre>
      <h3>Writing Testable Code</h3>
      <p>
        Crafting code that is easily testable contributes to effective and
        efficient testing practices:
      </p>
      <h3>Separation of Concerns:</h3>
      <p>
        Design code with clear separation of concerns, making individual units
        isolated and easier to test.
      </p>
      <pre>
        <code class="language-python"># Difficult to test without separation
def process_and_store_data(data):
    # Code...
    # More code...
    store_data(data)

# Easier to test with separation
def process_data(data):
    # Code...
    # More code...
    return processed_data

def store_data(data):
    # Code...</code>
      </pre>

      <h3>Dependency Injection:</h3>
      <p>
        Use dependency injection to inject dependencies into units, facilitating
        easier substitution with mock objects during testing.
      </p>
      <pre>
        <code class="language-python">// Without dependency injection
class OrderService {
    private database: Database;

    constructor() {
        this.database = new Database();
    }
}

// With dependency injection
class OrderService {
    private database: Database;

    constructor(database: Database) {
        this.database = database;
    }
}</code>
      </pre>
      <h3>Avoiding Global State:</h3>
      <p>
        Minimize reliance on global state, which can make testing complex and
        unpredictable.
      </p>
      <pre>
        <code class="language-python">// Code with global state
public class GlobalState {
    public static int counter = 0;
}

// Code avoiding global state
public class Counter {
    private int count = 0;
    
    public int getCount() {
        return count;
    }
    
    public void increment() {
        count++;
    }</code>
      </pre>

      <h3>Test Framework Integration:</h3>
      <p>
        Write tests using a testing framework suitable for the programming
        language, such as JUnit for Java or pytest for Python.
      </p>
      <pre>
        <code class="language-csharp">// Example of a JUnit test
@Test
public void testMultiplication() {
    Calculator calculator = new Calculator();
    int result = calculator.multiply(2, 3);
    assertEquals(6, result);
}</code>
      </pre>
    </div>

    <div id="section10" class="section">
      <h1>Version Control and Branching</h1>
      <p>
        Adhering to version control best practices and effective branching
        strategies promotes collaboration, facilitates code reviews, and ensures
        a smooth and organized development workflow. These practices contribute
        to a more stable and manageable codebase over time.
      </p>
      <h3>Best Practices for Version Control</h3>
      <p>
        Following best practices for version control ensures collaboration,
        traceability, and a streamlined development process:
      </p>

      <h3>Frequent Commits:</h3>
      <p>
        Make small, frequent commits to track changes effectively and provide a
        detailed history of the project's evolution.
      </p>
      <pre>
        <code class="language-bash"># Frequent commits with meaningful messages
git commit -m "Implement feature A"
git commit -m "Fix issue in feature B"</code>
      </pre>

      <h3>Descriptive Commit Messages:</h3>
      <p>
        Write clear and concise commit messages that explain the purpose and
        context of the changes.
      </p>

      <pre>
        <code class="language-bash"># Unclear commit message
git commit -m "Update code"

# Descriptive commit message
git commit -m "Add user authentication feature"</code>
      </pre>

      <h3>Branch Naming Conventions:</h3>
      <p>
        Adopt consistent branch naming conventions to easily identify the
        purpose of each branch.
      </p>

      <pre>
        <code class="language-bash"># Non-descriptive branch name
git branch feature

# Descriptive branch name
git branch feature-user-authentication</code>
      </pre>

      <h3>Pull Requests/Merge Requests:</h3>
      <p>
        Use pull requests (or merge requests) for code review and integration,
        allowing collaborators to provide feedback before changes are merged.
      </p>
      <pre>
        <code class="language-bash"># Creating a pull request
git checkout -b feature-user-authentication
git commit -m "Implement user authentication"
git push origin feature-user-authentication</code>
      </pre>

      <h3>Effective Branching Strategies</h3>
      <p>
        Employing effective branching strategies facilitates parallel
        development and release management:
      </p>
      <h3>Feature Branches:</h3>
      <p>
        Create feature branches for the development of specific features or
        enhancements.
      </p>
      <pre>
        <code class="language-bash"># Creating a release branch
git checkout -b release-1.0</code>
      </pre>

      <h3>Hotfix Branches:</h3>
      <p>
        Address critical issues in production by creating hotfix branches,
        fixing the issue, and merging the changes back into the main and release
        branches.
      </p>
      <pre>
        <code class="language-bash"># Creating a hotfix branch
git checkout -b hotfix-security-issue</code>
      </pre>
      <h3>Main/Branch:</h3>
      <p>
        Keep the main (or master) branch stable and deployable at all times.
        Integrate features through pull requests to maintain a clean and
        reliable main branch.
      </p>
      <pre>
        <code class="language-bash"># Merging a feature into main
git checkout main
git merge feature-user-authentication</code>
      </pre>
      <h3>Long-Term Branches:</h3>
      <p>
        Utilize long-term branches for ongoing development efforts or
        maintenance of older releases.
      </p>
      <pre>
        <code class="language-bash"># Creating a long-term support branch
git checkout -b lts-branch</code>
      </pre>
    </div>

    <div id="section11" class="section">
      <h1>Code Reviews</h1>
      <p>
        Effective code reviews promote a collaborative and learning-oriented
        environment within a development team. Providing constructive feedback
        ensures that developers can learn from the review process and
        continuously improve their coding practices.
      </p>

      <h2>Conducting and Participating in Code Reviews</h2>
      <p>
        Effective code reviews contribute to code quality, knowledge sharing,
        and collaboration within a development team:
      </p>
      <ul>
        <li>
          <b>Early Involvement:</b> Initiate code reviews early in the
          development process to catch issues and provide feedback promptly.
        </li>
        <li>
          <b>Use of Code Review Tools:</b> Leverage code review tools or
          platforms to facilitate the review process and provide a centralized
          location for discussions.
        </li>
        <li>
          <b>Clear Objectives:</b> Clearly define the objectives of the code
          review, whether it's ensuring code quality, identifying bugs, or
          verifying adherence to coding standards.
        </li>
        <li>
          <b>Balanced Timing:</b> Avoid excessively long code review sessions.
          Aim for a balance that allows thorough examination without causing
          delays.
        </li>
        <li>
          <b>Consistent Standards:</b> Establish and follow consistent code
          review standards within the team to maintain a cohesive approach.
        </li>
        <li>
          <b>Constructive Tone:</b> Use a constructive and positive tone in
          comments. Focus on improving the code rather than criticizing the
          developer.
        </li>
      </ul>
      <pre>
        <code class="language-python"># Constructive comment
# Consider using a more descriptive variable name for clarity</code>
      </pre>
      <h3>Focus on High-Impact Issues:</h3>
      <p>
        Prioritize feedback on critical issues such as security vulnerabilities,
        logic errors, and maintainability concerns.
      </p>
      <h3>Providing Constructive Feedback</h3>
      <p>
        When providing feedback during a code review, aim for constructive and
        actionable suggestions:
      </p>
      <p>
        <b>Be Specific:</b> Clearly articulate the issue or improvement,
        providing specific examples when possible.
      </p>
      <pre>
        <code class="language-csharp">// Vague feedback
// This function is confusing; please fix it.

// Specific feedback
// Consider renaming the function to better reflect its purpose, such as 'calculateTotal'.</code>
      </pre>
      <h3>Suggest Alternatives:</h3>
      <p>
        If pointing out a problem, suggest alternative solutions or approaches
        to guide the developer.
      </p>
      <pre>
        <code class="language-csharp">// Identifying an issue without suggestions
// This loop is inefficient; please optimize it.

// Providing feedback with alternatives
// Consider using a HashSet to improve lookup performance in this loop.</code>
      </pre>

      <h3>Explain the Reasoning:</h3>
      <p>
        Clarify the rationale behind your feedback, especially if it involves
        adherence to coding standards or best practices.
      </p>
      <pre>
        <code class="language-csharp"># Providing feedback without explanation
# Use consistent indentation in this block.

# Explaining the reasoning
# To maintain code consistency, please use four spaces for indentation in this block.</code>
      </pre>

      <h3>Acknowledge Positive Aspects:</h3>
      <p>
        Recognize and acknowledge positive aspects of the code to foster a
        positive and collaborative atmosphere.
      </p>
      <h3>Encourage Discussion:</h3>
      <p>
        Encourage open communication and a two-way dialogue during the code
        review process.
      </p>

      <pre>
        <code class="language-csharp">// Encouraging discussion
// I have some concerns about the approach in this section. Can we discuss it further in our next meeting?</code>
      </pre>
      <h3>Prioritize Issues:</h3>
      <p>
        If there are multiple feedback points, prioritize them to guide the
        developer on which aspects to address first.
      </p>
      <pre>
        <code class="language-csharp"># Prioritizing feedback
# Address the critical security issue first, and then we can look into optimizing the performance.</code>
      </pre>
    </div>

    <div id="section12" class="section">
      <h1>Continuos Integration</h1>
      <p>
        Continuous integration and continuous delivery practices contribute to a
        more efficient and reliable software development lifecycle.
      </p>
      <p>
        Automated builds, tests, and deployments ensure that code changes are
        thoroughly validated and seamlessly delivered to production
        environments.
      </p>
      <h3>Automated Builds and Tests</h3>
      <p>
        Automated builds and tests are fundamental components of continuous
        integration, ensuring code quality and reliability:
      </p>
      <h3>Build Automation:</h3>
      <p>
        Automate the process of compiling and building the codebase to identify
        compilation errors and ensure consistency.
      </p>
      <pre>
        <code class="language-csharp"># Example of build automation script
# Execute build commands
make build

# Run automated tests
make test</code>
      </pre>
      <h3>Unit Tests:</h3>
      <p>
        Implement a suite of automated unit tests to verify the correctness of
        individual components or functions.
      </p>

      <pre>
        <code class="language-csharp">// Example of a JUnit test
@Test
public void testAddition() {
    Calculator calculator = new Calculator();
    int result = calculator.add(2, 3);
    assertEquals(5, result);</code>
      </pre>
      <h3>Integration Tests:</h3>
      <p>
        Include automated integration tests to validate the interaction between
        different components or services.
      </p>
      <pre>
        <code class="language-csharp"># Example of integration test using pytest
def test_integration():
    result = perform_integration_operation()
    assert result == expected_result</code>
      </pre>

      <h3>Continuous Testing:</h3>
      <p>
        Integrate automated tests into the CI pipeline to run tests
        automatically upon code changes.
      </p>
      <pre>
        <code class="language-csharp"># Example CI configuration (e.g., using GitHub Actions)
name: Continuous Integration

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Repository
      uses: actions/checkout@v2

    - name: Build and Test
      run: |
        make build
        make test</code>
      </pre>

      <h3>CI/CD Best Practices</h3>
      <p>
        Adopting best practices for continuous integration and continuous
        delivery (CI/CD) enhances development and deployment processes:
      </p>
      <h3>Automated Deployment:</h3>
      <p>
        Automate the deployment process to streamline the release of software
        updates.
      </p>

      <pre>
        <code class="language-csharp"># Example CI/CD configuration for deployment
name: Continuous Delivery

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Repository
      uses: actions/checkout@v2

    - name: Deploy to Production
      run: |
        make deploy</code>
      </pre>
      <h3>Immutable Infrastructure:</h3>
      <p>
        Treat infrastructure as code, enabling the recreation of environments
        with consistent configurations.
      </p>

      <pre>
        <code class="language-csharp"># Example Terraform script for infrastructure
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}</code>
      </pre>
      <h3>Rollback Mechanism:</h3>
      <p>
        Implement a rollback mechanism to quickly revert to a stable state in
        case of deployment issues.
      </p>
      <pre>
        <code class="language-csharp"># Example CI/CD configuration with rollback
on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Deploy to Production
      run: |
        make deploy || make rollback</code>
      </pre>
      <h3>Pipeline as Code:</h3>
      <p>
        Define CI/CD pipelines as code to version control the pipeline
        configuration.
      </p>
      <pre>
        <code class="language-csharp"># Example CI/CD pipeline definition
pipelines:
  default:
    - step:
        name: Build and Test
        script:
          - make build
          - make test</code>
      </pre>
      <h3>Environment Promotion:</h3>
      <p>
        Promote code through different environments (e.g., development, staging,
        production) with consistency.
      </p>
      <pre>
        <code class="language-csharp"># Example CI/CD pipeline for environment promotion
on:
  push:
    branches:
      - main

jobs:
  deploy_dev:
    runs-on: ubuntu-latest
    steps:
    - name: Deploy to Development
      run: make deploy_dev

  deploy_prod:
    runs-on: ubuntu-latest
    steps:
    - name: Deploy to Production
      run: make deploy_prod</code>
      </pre>
    </div>

    <div id="section13" class="section">
      <h1>Performance</h1>
      <p>
        Writing efficient code involves a combination of algorithmic choices,
        data structure selection, and coding practices. Regularly assessing and
        optimizing code for performance ensures that the software can scale and
        respond effectively to user demands.
      </p>

      <h3>Considerations Identifying and Optimizing Bottlenecks</h3>
      <p>
        Identifying and optimizing performance bottlenecks is crucial for
        creating efficient software:
      </p>
      <h3>Profiling Tools:</h3>
      <p>
        Use profiling tools to analyze the runtime behavior of the application
        and identify performance bottlenecks.
      </p>

      <pre>
        <code class="language-csharp"># Example of profiling with Python's cProfile
python -m cProfile my_script.py</code>
      </pre>
      <h3>Code Reviews:</h3>
      <p>
        Conduct code reviews with a performance focus, identifying potential
        bottlenecks and discussing optimization strategies.
      </p>
      <pre>
        <code class="language-csharp">// Code review comment addressing potential bottleneck
// Consider optimizing this loop for better performance.</code>
      </pre>
      <h3>Monitoring and Logging:</h3>
      <p>
        Implement monitoring and logging to collect performance metrics in
        production, allowing the identification of runtime issues.
      </p>
      <pre>
        <code class="language-csharp">// Example of logging performance metrics
Logger.log("Processing time: " + elapsedTime + " milliseconds");</code>
      </pre>
      <h3>Load Testing:</h3>
      <p>
        Conduct load testing to simulate real-world usage scenarios and identify
        how the application performs under various conditions.
      </p>
      <pre>
        <code class="language-csharp"># Example of load testing with Apache JMeter
jmeter -n -t my_test_plan.jmx -l results.jtl</code>
      </pre>

      <h3>Writing Efficient Code</h3>
      <p>
        Writing code with efficiency in mind contributes to improved
        performance:
      </p>
      <h3>Algorithmic Efficiency:</h3>
      <p>
        Choose algorithms with optimal time and space complexity for the problem
        at hand.
      </p>
      <pre>
        <code class="language-python"># Example of inefficient algorithm
def find_element(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1</code>
      </pre>
      <h3>Data Structures:</h3>
      <p>
        Select appropriate data structures to enhance the efficiency of common
        operations.
      </p>
      <pre>
        <code class="language-csharp">...</code>
      </pre>
      <h3>Caching:</h3>
      <p>
        Utilize caching mechanisms to store and reuse previously computed
        results, reducing redundant calculations.
      </p>
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

  <div class="right-sidebar">
    <h2>Useful links</h2>
    <ul>
      <li>link 1</li>
      <li>link 2</li>
      <li>link 3</li>
      <li>link 4</li>
      <li>link 5</li>
    </ul>
  </div>
  <footer>footer</footer>
  <div class="scroll-indicator"></div>
</template>
