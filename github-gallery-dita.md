# GitHub Gallery Project Technical Documentation

## Overview

**Project:** GitHub Gallery  
**Author:** Stephanie Parra  
**Technologies:** HTML, CSS, JavaScript, GitHub API  
**Purpose:** Display GitHub user profile and repositories in a searchable gallery with an additional mock AI workflow component for enhanced user experience.

**Goal / Learning Objective:**  
This project demonstrates how to fetch data from the GitHub API, dynamically render user information and repositories, and provide a responsive, interactive experience. Additionally, it illustrates a mock AI workflow to show how AI could enhance repository descriptions for beginner developers.

#### You can see the full repo [here.](https://github.com/stephanieparra/github-repo-gallery)
#### DITA Version

For a structured, professional DITA-style version of this documentation:

- [View DITA XML](./github-gallery/github-gallery.dita.xml)  

---

## System Requirements

- Modern web browser (Chrome, Firefox, Safari, Edge)  
- Internet connection to fetch data from GitHub API  

---

## Installation

1. Clone the repository:  
```bash
git clone https://github.com/stephanieparra/github-repo-gallery.git
```

2. After cloning, navigate into the project directory via your own terminal:
```bash
cd github-repo-gallery
```

3. Open index.html in a browser (or via Live Server if using a text editor like VSCode).
> Tip: Live Server allows real-time updates while editing the code.

## Usage

1. The app automatically fetches the GitHub profile for stephanieparra.
2. User profile information (avatar, bio, location, number of public repos) is displayed at the top.
3. A list of repositories is displayed in a searchable gallery.
4. Click on a repository name to view detailed information:
    - Description
    - Default branch
    - Languages used
    - Link to GitHub repo
5. Use the search input to dynamically filter repositories by name.
> Tip: Use lowercase for search queries to match repository names.
---
## API Integration
#### GitHub API
- Fetch user info: https://api.github.com/users/stephanieparra
- Fetch repos: https://api.github.com/users/stephanieparra/repos?sort=updated&per_page=100
- Fetch repo languages: repo.languages_url

#### AI Workflow (Mock)
**Goal:** Demonstrate how AI could enhance user experience by generating repository descriptions.
**Trigger:** When repositories are rendered.
**Inputs:** Repository name.

**Process (Mocked):**
1. Create a paragraph element (`<p>`) for the AI description.
2. Populate with mock AI text.
3. Append to the repository item in the DOM.

**Code Example:**
```
// Mock AI description //
    const aiDescription = document.createElement("p");
    aiDescription.classList.add("ai-description");
// Mock text //
    aiDescription.innerText = `Mock AI-generated fact about this repo: Imagine that beginner developers can use this repo ${repo.name} to learn faster by exploring examples of how either JS, Bootstrap, React, or p5.js work in the project!`;
    repoItem.appendChild(aiDescription);
    repoList.append(repoItem);
  }
};
```

**Output**:
The AI-generated text appears below each repository name in the gallery, giving beginner developers a concise, engaging explanation of how the repo can help them learn.
> Note: This is a mock workflow. It demonstrates AI concept integration without calling an actual API.

## Mermaid Flowchart
```
flowchart TD
    A[User enters GitHub username] --> B[Fetch user profile via GitHub API]
    B --> C[Display profile info]
    C --> D[Fetch repositories via GitHub API]
    D --> E[Display repository list]
    E --> F[User clicks on a repository]
    F --> G[Fetch repository details & languages]
    G --> H[Display repository details]
    H --> I[Simulate API call to AI LLM]
    I --> J[Receive AI-generated description/fun fact]
    J --> K[Append description to repository detail view]
```
---
## Rationale / Benefits

- **Enhanced learning**: Beginners can immediately understand the educational value of each repository.

- **Dynamic content potential**: Enterprises could replace the mock workflow with real AI integration to generate descriptions for hundreds of repos automatically.

- **Scalable UX improvement**: Instead of hardcoding explanations, AI-generated content could adapt based on repo metadata, user preferences, or historical usage patterns.

- **Engagement**: Makes the gallery more interactive and informative, which can improve adoption and understanding for new developers exploring example projects.
> Tip: Highlight the AI descriptions visually using CSS for improved readability.
---
## Troubleshooting
- Ensure you have an active internet connection for fetching GitHub data.
- If the gallery is empty, check that the GitHub username is correct.
- If the AI mock description does not appear, ensure the aiDescription code is included **after** each repo is appended.
> Note: Missing AI descriptions are normal if the mock workflow code is commented out.
---
## Tips & Best Practices
- Future integration: Replace mock workflow with real OpenAI API for dynamic content.
- Use semantic HTML for accessibility.
- Test responsiveness on multiple devices.
- Keep repository gallery performance in mind if integrating AI for all items.
---
## Conclusion
The GitHub Gallery project combines:
- **API Integration**: Fetch and display live data
- **Dynamic UI Rendering**: Interactive repository gallery
- **Searchable Interface**: Filter repositories in real-time
- **Mock AI Workflow**: Conceptual demonstration of AI-enhanced learning

>This project illustrates both **technical skills** and **conceptual thinking** for creating beginner-friendly, engaging, and interactive documentation-ready applications.



