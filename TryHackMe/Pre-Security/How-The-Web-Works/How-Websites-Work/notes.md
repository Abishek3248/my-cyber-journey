# How Websites Work

## Introduction
- When you visit a website, your browser (like Chrome or Safari) sends a request to a web server asking for information about the page. The server responds with data that your browser uses to display the page. A web server is essentially a dedicated computer somewhere on the internet that handles these requests.
**Websites consist of two major components:**
  - Front End (Client-Side): How your browser renders and displays the website.
  - Back End (Server-Side): The server processes requests and returns the necessary data.
- While there are many other processes involved in a browser-server interaction, the key takeaway is: your browser makes a request, and the server responds with the data needed to render the website.


## HTML

### Concepts Learned
- HTML structures content on a website using elements like headings, paragraphs, and images.
- Small mistakes, such as missing file extensions, can break functionality (e.g., images not displaying).
- Comments (<!-- -->) can be used to annotate HTML code without affecting the output.
- You can add new content, like images, by properly specifying the src attribute in the <img> tag.

### Explanation
- The <html> element wraps the entire webpage.
- The <head> section contains metadata like the page <title>.
- The <body> contains visible content:
- <h1> for main headings.
- <p> for paragraphs.
- <img src="path"> to display images.
- File paths and extensions in <img> tags must be correct for the image to display.
- Comments allow you to leave notes in the code that are not rendered in the browser.

### Notes
**Original Code (with missing extension):**
<img src='img/cat-2.'>
- Issue: Missing .jpg extension → image did not display.
**Corrected Code (added proper extension and dog image):**
<img src='img/cat-1.jpg'>
<img src='img/cat-2.jpg'>
<img src='img/dog-1.png'>
- Fix: Added correct .jpg for second cat image.
- Added a dog image to demonstrate adding new content.
- Running the code in the interactive lab showed the images on the webpage as expected.


## JavaScript

### Concepts Learned
- JavaScript makes webpages interactive, whereas HTML only structures content.
- JS can dynamically update page content, styles, and animations in real-time.
- Elements can have events (e.g., onclick, onhover) that trigger JavaScript functions.
- JS can be included inline with <script> tags or loaded from external files using the src attribute.
- DOM manipulation allows changing content of HTML elements via document.getElementById().

### Explanation
**Inline Update:**
document.getElementById("demo").innerHTML = "Hack the Planet";
Updates the content of the element with id demo.
**Event Handling:**
<button onclick='document.getElementById("demo").innerHTML = "Button Clicked";'>Click Me!</button>
Changes content when the button is clicked. Events can also be defined inside <script> tags instead of directly on elements.
**Script Inclusion:**
<script src="/path/to/javascript_file.js"></script>
Loads an external JS file.

### Notes
**Example Code Used in Lab:**
<div id="demo">Hi there!</div>
<button onclick='document.getElementById("demo").innerHTML = "Button Clicked"'>Click Me!</button>
<script type="text/javascript">
   document.getElementById("demo").innerHTML="Hack The Planet"
</script>
- The <div> initially displayed "Hi there!"
- JS script changed it to "Hack The Planet".
- Button click changes text to "Button Clicked".
- Learned how to manipulate element content and add interactivity via buttons and events.



