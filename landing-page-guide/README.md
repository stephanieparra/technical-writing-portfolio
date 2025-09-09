# 🍩 How to Build a Simple, Aesthetic HTML Landing Page with an Accessibility Foundation

I love HTML for its simplicity and accessible nature -  both as a friendly gateway into development and for its semantic clarity that supports assistive technologies like screen readers and keyboard navigation.  

This project walks through building a simple landing page while integrating accessibility best practices, with the goal of helping new developers learn core concepts while also practicing inclusive design. Along the way, I used AI to iterate on the code and improve accessibility features.

See [Web AIM's accessiblity tag cheatsheet](https://webaim.org/resources/htmlcheatsheet/) and [Mozilla's MDN page on accessibility](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Accessibility/HTML) to learn more.

## 🛠️ Prerequisites
- Basic knowledge of HTML, CSS, and JavaScript
- Familiarity with VSCode or another code editor
- Optional: understanding of p5.js for aesthetic/interactive elements

## 🧰 Tools
- VSCode or any code editor
- Git/GitHub for version control
- Browser to test your page
- AI assistant (e.g., ChatGPT) for accessibility review

## 📝 Step 1: HTML Structure (Initial Version - No Accessibility Improvements Yet)

This is a snippet of the HTML I initially wrote based on my design ideas. The focus was on creating a simple, aesthetic, and culturally relevant (to me) landing page featuring some info on **Pan Dulce Mexicano**. You can see the full html on my Github repo [here](https://github.com/stephanieparra/landing-page-project/blob/main/index.html).  

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>An ✨Aesthetic✨ Guide to Pan Dulce Mexicano</title>
    <link rel="stylesheet" href="src/styles.css" />
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.6.0/p5.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.6.0/addons/p5.sound.min.js"></script>
  </head>
  <body>
    <h1>An ✨Aesthetic✨ Guide to Pan Dulce Mexicano</h1>
    <h2><em>with menially-researched beverage pairings</em></h2>
    <div class="container">
      <ul>
        <li>
          <img src="conchas.jpg" alt="Pink conchas" />
          <p><strong>Conchas:</strong> Classic Mexican sweet bread...</p>
        </li>
        <!-- Additional pastries here -->
      </ul>
    </div>
    <button>✨What's the best pan dulce?✨</button>
    <div id="canvas-container"></div>
    <script src="src/app.js"></script>
    <script src="src/sketch.js"></script>
  </body>
</html>
```

#### Notes on the initial version:

I used:
- Semantic HTML but not everything is optimized. I still use <div> which doesn't describe anything for a screen reader.
- Basic alt text for images.
- Button for interactivity that will open a prompt when clicked (it's natively keyboard-accessible as well).

## 🤖 Step 2: Accessibility Review with AI

After writing my initial HTML, I used AI (ChatGPT) to review for accessibility improvements. This step shows how I iterated on my HTML using AI to improve accessibility. Documenting my workflow highlights not just the final code, but how I solved problems and made the page more inclusive and moreso up to coding AND accessibility standards!

### Example AI Prompts
##### 1. Check accessibility issues in HTML Prompt
```
"Check this HTML snippet for accessibility issues and suggest improvements:"
[Paste your HTML code snippet here]
```

##### 2. Generate descriptive alt text for images
```
"Suggest alt text for this image: 'pink conchas on a white plate with colorful sugar shells'"
```

#### Changes made based on AI suggestions:

- Updated alt text for all images
- Verified heading hierarchy
- Reviewed semantic HTML structure for lists and sections
- Ensured interactive elements (like the button) are accessible

#### Button Accessibility: ARIA Considerations

For the “✨What's the best pan dulce?✨” button:

- Visible text is already descriptive, so no ARIA label is strictly required
- However, added **aria-label** to clarify action for screen readers:
```
<button aria-label="Prompt user to enter their favorite pan dulce">
  ✨What's the best pan dulce?✨
</button>
```
- The **aria-labelledby**, another ARIA option, wasn’t necessary because the label does not exist elsewhere in the DOM.

**Why this matters**: By choosing the appropriate ARIA attribute, I ensured the button is screen-reader friendly, keeping the page simple, usable, and accessible.

## 🎨 3. Add CSS for Aesthetic Styling

With structure and accessibility in place, the next step is to style the landing page. I wanted to make the theme very pastel and "kawaii," so I created a background image in Canva with graphics that fit the vibe I wanted to create. I hosted the background image on Amazon Web Services and rendered a url I could use in the CSS.

Here are some highlights from the `styles.css` file below. See the full css file [here.](https://github.com/stephanieparra/landing-page-project/blob/main/src/styles.css)

```css
h1 {
  text-align: center;
  color: #59366a;
  font-family: monospace;
  font-size: 48px;
  margin-top: 120px;
}

body {
  background-image: url("https://s3.amazonaws.com/shecodesio-production/uploads/files/000/018/031/original/coffeecloud-pg-two-purple-background-pan-dulce.png?1633053303");
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: center;
}

img {
  display: block;
  margin: 0 auto;
  margin-bottom: 45px;
  border-radius: 100px;
  border: 4px dotted #9171d3;
  height: 200px;
  width: 200px;
}

button {
  font-family: monospace;
  background: #9171d3;
  color: #f1e5e5;
  font-size: 20px;
  padding: 20px 20px;
  border-radius: 4px;
  border: 2px solid #daf9ff;
  box-shadow: 9px 9px #000;
  transition: all 200ms ease-in-out;
}
```

#### 💡 Tips & Tricks for Styling

 - Use a font that adds to your aesthetic! I used monospace for a pixel-y, retro look.
 - Add hover effects (like scaling images or adjusting opacity) for interactivity without extra JavaScript.
 - Balance strong backgrounds with high-contrast text for readability. Knowing that my paragraph text wouldn't stand out on the background image I made in Canva, I created a "box" with CSS properties so that my paragraph can sit on a contrasting background.

## 👾 4. Add JavaScript Button Interaction

To make the page interactive, I added a button at the bottom of the page that prompts users for their favorite pan dulce. When users click the button, it triggers a click event and a prompt appears.

```
function best() {
  let name = prompt("What is your name?");
  let panDulce = prompt("What is the best pan dulce?");

  if (panDulce === "conchas") {
    alert("Yes " + name + ", you are so right! Conchas ARE the best pan dulce! 💕");
  } else {
    alert("Sorry " + name + ", conchas are the best pan dulce! I don't make the rules. 🤷🏻‍♀️");
  }
}

let button = document.querySelector("button");
button.addEventListener("click", best);
```

This shows how a single button can bring in user input and conditional logic, even on a simple beginner-friendly landing page.

## 🌸 5. Add p5.js Interaction

For an extra touch, I used p5.js to create a mouse-follower effect with an image of a marranito pan dulce. This adds a cute and playful element that makes the page feel a little more dynamic. There's a snippet below but you can see the full p5.js code [here.](https://github.com/stephanieparra/landing-page-project/blob/main/src/sketch.js)

```
let mouseFollower;

function setup() {
  let canvas = createCanvas(windowWidth, windowHeight);
  canvas.parent("canvas-container");
  canvas.style("z-index", "-1");

  mouseFollower = createImg("images/pd (2).png");
  mouseFollower.size(65, 65);
  mouseFollower.style("pointer-events", "none");
  mouseFollower.style("z-index", "9999");
}

function draw() {
  mouseFollower.position(mouseX, mouseY);
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```

##### 💡 Why p5.js?

- It’s beginner-friendly but powerful for visuals and creative coding.
- Encourages experimentation with interactivity.
- Makes static HTML pages feel alive and a little more fun to use, no?

## ✅ 6. Final Touches: Accessibility + Aesthetics

- Confirmed all images have alt text.
- Ensured semantic tags (headings, sections, paragraphs) were used.
- Used AI to cross-check for accessibility gaps (e.g., aria-label suggestions).
- Balanced a retro, early-computer/internet, design with readability and inclusivity.

## 🤔 7. Reflection

This project demonstrates:

- How to structure and style a landing page with HTML + CSS.
- How to add simple interactivity with JavaScript.
- How to use AI to improve accessibility.
- How to sprinkle in creative coding with p5.js just for fun (as coding should be fun too)!


## 🚀 8. Considerations & Future Improvements

While this project demonstrates the essentials of building, styling, using AI to improve accessibility, and adding some interactive elements to a landing page, there are several areas where it could be extended:

- **Responsiveness:** Currently the layout looks best on desktop with some responsiveness for certain screen sizes. Adding media queries would improve the mobile/tablet experience.  
- **Accessibility Testing:** While AI provided suggestions, running the site through tools like Lighthouse, WAVE, or axe-core could surface more issues.  
- **Performance:** Images could be optimized for faster load times.  
- **Internationalization (i18n):** Since pan dulce is culturally specific, translations or multilingual support could make the page more inclusive.  
- **Additional Interactivity:** Expanding the JavaScript beyond a single button (e.g., quizzes, random pan dulce suggestions) would increase engagement.  
- **Styling Consistency:** Using a CSS framework or design system might make scaling easier if the page grew into a larger site.  
