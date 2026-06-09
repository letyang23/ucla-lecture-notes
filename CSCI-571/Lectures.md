## Course Logistics & Policies

| **Component**    | **Weight** | **Details**                                                  |
| ---------------- | ---------- | ------------------------------------------------------------ |
| **Homework (4)** | 40%        | Submit via Brightspace. 10% penalty per day late (score becomes 0 after 10 days). No makeup projects. |
| **Midterm Exam** | 30%        | Held on a Wednesday, halfway through the 6-week session. Open notes/cheat sheet. |
| **Final Exam**   | 30%        | Held on the last Tuesday (June 30th). Open notes/cheat sheet. |

- **Platform Hubs:** `bytes.usc.edu` is used for slides, lectures, and homework descriptions. Brightspace is used exclusively for video recordings, assignment submissions, and grading.
- **Communication:** Use Piazza for all class questions. The professor has limited 1-on-1 office hours due to teaching load.
- **Attendance:** Mandatory. Random roll calls are taken using a JavaScript script. If your name is called and you are present, you get 0 points (neutral). If absent, you get a -5 point penalty. Two absences equal a -10 point penalty.
- **Academic Integrity:** Zero tolerance for cheating. Modifying a Gradescope submission after the exam timer ends or blindly submitting AI-generated code will result in an automatic 'F' and a formal report to the Office of Academic Integrity.
- **Remote Location Policy:** International students must be physically present (within 100 miles of campus). Taking the course remotely from a foreign country while enrolled as a full-time on-campus student is an immigration violation.

## The Core Web "Triangle"

The fundamental structure of the web remains reliant on three open standards maintained by the W3C (World Wide Web Consortium):

- **HTML (Content):** The structural foundation. It takes plain text and tags it to define headers, paragraphs, and links. HTML is making a massive comeback as a way to define "skills" for AI agents.
- **CSS (Styling):** Defines the visual appearance. It dictates fonts, colors, and layout properties, separating design from the structural content.
- **JavaScript (Interactivity):** The engine of the dynamic web. It reads and modifies the HTML/CSS on the fly, enabling UI manipulation, calculations, and animations.

## The AI Revolution in Web Development

The web is transitioning away from manual coding and traditional human-browser interaction toward an agent-driven model.

- **Agent Architecture:** At its core, an AI agent is an infinite loop (`while True:`) equipped with a "tools array." It calls tools (like web search, databases, file execution) to solve problems.
- **The Agent Harness:** A crucial memory/caching layer surrounding the agent. It stores context and previous tool outcomes so the agent learns from success and failure instead of repeating mistakes.
- **Generative Full-Stack Development:** Tools like Google Firebase and AI Studio can now generate entire full-stack applications (front-end, database, back-end code, and payment processing) purely from a single text prompt.
- **The Death of the Link:** Traditional search engines rely on PageRank to display blue links. Generative AI summarizes information directly, meaning future web traffic will be driven by AI agents fetching content via headless browsers rather than humans clicking links.
- **Career Strategy:** AI will shrink standard engineering teams. To survive and thrive, engineers must learn how to integrate AI tools (like AWS Bedrock) and build complex deployment projects to stand out.

## Key Technologies & Frameworks

- **JSON (JavaScript Object Notation):** A standard text format for APIs. It is currently the primary language used to communicate with AI models and agents.
- **Node.js:** A runtime environment that allows JavaScript to run on the back-end server, unifying the web stack under one language.
- **React vs. Dart:** React (and React Native) uses JSX components to build UIs but can suffer from cross-platform bugs. Google's Dart was designed to replace it, guaranteeing pixel-perfect UI rendering on any device (phones, laptops, car dashboards).
- **WebAssembly (Wasm):** Allows languages like C, C++, and Rust to be compiled into a format that runs natively and instantly in the browser.
- **Responsive Web Design (RWD):** The practice of writing a single HTML codebase that dynamically adjusts its layout to fit any screen size (desktop, tablet, mobile).
- **Microservices:** Breaking down large, monolithic applications into hundreds of small, isolated services that communicate with each other over a network.

## Browser Mechanics & Infrastructure

- **Rendering Engines:** The core of a web browser (e.g., Chromium, Gecko). It parses HTML, CSS, and JS and translates them into the interactive pixels you see on screen.
- **Headless Browsers:** Rendering engines that run without a visual graphical interface (e.g., Puppeteer). They are used heavily by AI agents to invisibly "read" web pages.
- **Caching:** Browsers store local copies of web resources to reduce redundant server requests. To force the browser to fetch fresh content (useful when looking for newly posted homework), hold `Shift` and click `Reload`.
- **Developer Tools:** Accessed via `Ctrl/Cmd + Shift + I`. Used to inspect DOM elements, trace network requests, debug JavaScript, and view cookies.
- **Content Delivery Network (CDN):** Geographically distributed copies of your server. CDNs ensure that users globally can load your site quickly by fetching data from a server physically close to them.

## Cloud Deployment & Hosting

- **Serverless Architecture:** Running code in the cloud (like AWS Lambda or Google Cloud Functions) without managing the underlying server infrastructure. You only write the function (e.g., calculate a square root), and the cloud handles the execution.
- **AWS Bedrock:** Amazon's foundation service for deploying Large Language Models (LLMs) at scale. You can emulate these massive AWS services locally on your machine for free using sandbox containers before deploying to the real cloud.
- **Portfolio Hosting:** Use `github.io` (GitHub Pages) to host lightweight, static portfolio websites for free to impress employers. Use platforms like Vercel or Firebase for heavier, dynamic applications.