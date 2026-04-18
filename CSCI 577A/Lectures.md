# 1/12 Lecture 1

Exam - 25%, Inclass quiz 10%, 7% assignment , 43% software project, 10% research paper review, 5% peer review

Team Charter

### **Course Overview & Logistics**

**Instructors**

- **Dr. Matti (Matty):** Focuses on practical application, project management, and economics .
  - *Background:* PhD from UCLA (Compilers), Industry experience (Samsung, Google, Microsoft), former CTO, currently Executive VP at a boutique consultancy (Quant GPC Research) doing technical due diligence for investors .
- **Dr. Jay:** Focuses on theory ("the boring part"), architecture, and design .
  - *Background:* PhD from USC, Industry experience (Kakao - user identity platform), currently a litigation consultant (patent infringement, copyright) and software advisor .

**Course Structure**

- **Format:** Two-pronged approach. Matti teaches practical/project tracks; Jay teaches theory (last 60 years of research) .
- **Schedule:** Monday 6:00–9:20 PM .
- **Communication:** All questions to Brightspace; email for personal/sensitive matters . Office hours by appointment via Zoom .

**Resources & Policies**

- **Textbook:** Written by Dr. Matti (approx. $38). Required for weekly reading and two quizzes .
- **AI Policy:** Generative AI (e.g., ChatGPT, Cursor) is **encouraged** and expected for coding and assignments, but output must be verified .
- **Late Policy:** Heavy penalty calculated exponentially: $(Days Late)^2$ deduction .

------

### **Grading & Evaluation**

**Assignments (Weekly)**

- **Frequency:** 9 assignments total; 7 are required (1% each) .
- **Format:** 8 questions, 1 case study, 1 research topic .
- **First Assignment:** Optional (due to add/drop period), covers first two chapters .

**Exams**

- **Written Exam:** March 23rd (Tentative). 6–8 PM. Essay/discussion style (approx. 10 questions) .
- **Quizzes:** Two in-class quizzes based on the textbook .

**Team Tasks**

- **Team Presentation:** Critique a notable research paper (act as a committee reviewer) .
- **Peer Review:** Evaluates team members (prevents "free-riding") .
- **Project:** Main deliverable (detailed below) .

------

### **The Semester Project ("The Startup")**

**Concept**

- **Team Size:** 10 students per team .
- **Role-Play:** Students are a startup; Dr. Matti is the investor. Teams must pitch ideas to get "funding" (grades) .
- **Goal:** Build an **MVP** (Minimum Viable Product). You do not need a fully featured product, but a working MVP is required .

**Timeline & Deliverables**

1. **Team Formation:** Immediate. Create a "Team Charter" assigning roles (e.g., CEO, Product Manager) .
2. **The Pitch:** Elevator pitch (3–4 minutes) to the investor at a specific station .
3. **Demo 1 (POC):** Focus on UI/UX (Figma), Proof of Concept, and product validation data .
4. **Demo 2 (Quality):** Focus on software quality, scalability, modularity, and infrastructure (e.g., EC2, APIs) .
5. **D-Day (Final Demo):** Presentation of the MVP to the class .
   - *Incentive:* Teams volunteering to present in earlier weeks (Week 1 or 2 of demos) receive extra credit (10% or 5%) .

------

### **Lecture Topic: What is Software Engineering?**

**Definition & Scope**

- **Definition:** "Multi-person construction of multi-version programs" (1975) .
- **Scope:** Development of systems complex enough to require teams of engineers .
  - *Exclusions:* Single developer projects, simple apps with short lifespans, or one-off "throwaway" code are generally not "software engineering" .
- **Goal:** Production of quality software, delivered on time, within budget, satisfying user needs .

**The "Nature" of Software (Why it's hard)**

- **Malleable:** It is abstract and easily changeable (unlike physical bridges) .
- **Human Intensive:** Heavily reliant on people and sociology .
- **Intangible:** You cannot touch or smell it; hard to visualize .
- **Complex:** Problems are unprecedentedly complex and depend on hardware .

**Core Axioms & Laws**

1. **Maintenance > Development:** Maintenance costs usually exceed development costs. You must design for the next 10–20 years .
2. **Brooks’s Law:** "Adding manpower to a late software project makes it later" (from *The Mythical Man-Month*) .
3. **Quick $\neq$ Good:** Higher upfront cost (better design) often reduces downstream costs .

**Development Processes**

- **Waterfall:** Requirements $\rightarrow$ Design $\rightarrow$ Implementation $\rightarrow$ Integration $\rightarrow$ Validation. (Often criticized, but sometimes the best model depending on context) .
- **Others mentioned:** Spiral Model, Agile, V-Shaped .
- **Note:** Every organization eventually customizes their own process (e.g., Google's version of Agile vs. Spotify's) .

------

### **Software Qualities (Terminology)**

**Categorization**

- **External Qualities:** Visible to the user (e.g., Reliability, Efficiency, Usability) .
- **Internal Qualities:** Concerns for developers (e.g., Verifiability, Maintainability, Extensibility) .
- **Product vs. Process:**
  - *Product:* Artifacts like code (e.g., Performance, Understandability) .
  - *Process:* The activity itself (e.g., Productivity, Timeliness) .

**Key Definitions**

- **Correctness:** Does it satisfy the requirements specification? (The ideal quality) .
- **Reliability:** Statistical probability that software operates as expected over a period of time .
- **Robustness:** Reasonable behavior in **unforeseen** circumstances (scenarios not in requirements, like aliens on Mars) .
- **Usability:** Ability for end users to easily use the software (subjective) .
- **Understandability:** Ability for developers to understand artifacts (crucial for maintenance; e.g., code comments) .
- **Verifiability:** Ease of establishing properties via formal analysis or testing .
- **Performance:** Efficiency given specific resources .
- **Evolvability:** Ability to add/modify functionality .
- **Reusability:** Constructing new software from existing pieces to lower costs .
- **Interoperability:** Ability to cooperate with other systems .
- **Scalability:** Growing in size while maintaining properties (critical for internet systems) .
- **Heterogeneity:** Composing systems from pieces in multiple languages/platforms .
- **Portability:** Executing in new environments with reasonable effort (e.g., Java on JVM) .

------

### **Case Studies: Infamous Software Failures**

- **AT&T (1990):** A single line of buggy code in an upgrade caused a ripple effect, shutting down the landline network .
- **Ariane 5 Rocket (1996):** Exploded due to a conversion error (64-bit velocity to 16-bit) causing an overflow .
- **Casino Slot Machine:** A variable was "signed" instead of "unsigned," causing a negative balance to flip to millions of dollars owed to the player .
- **Y2K (Year 2000):** Systems stored years as 2 digits, risking confusion between 1900 and 2000. Required massive maintenance costs .
- **Skype (2007):** Windows Update restarted many machines simultaneously, crashing Skype's peer-to-peer architecture .
- **Southwest Airlines (2022):** Archaic infrastructure collapsed during the holidays, causing massive cancellations .
- **CrowdStrike (2024):** A small update issue caused a meltdown in Windows systems globally (e.g., airports showing blue screens) .
- **Cloudflare (2025):** Infrastructure outage illustrating the "ripple effect" of modern internet dependencies .

### **Next Steps for Students**

- **Immediate:** Form a team of 10 and find a partner you trust .
- **Assignments:** Read Chapters 1 & 2. Complete the first assignment (Optional but recommended) .
- **Next Class:** No lecture next week (Holiday). See you in two weeks .



# 1/26 Lecture 2

### CSCI 577a Lecture Cheatsheet: Software Process Models & Agile

**Date:** January 26, 2026

**Instructor:** Dr. Jae

**Focus:** Software Process Models (ICSM, Waterfall, V-Model), Value-Based SE, and Agile Methodologies (Scrum, XP).

---

### **I. Logistics & Announcements**

- **Next Week (Feb 2):** Lecture by Dr. Matti focusing on **Project Pitching**.
- **Two Weeks (Feb 9):**
  - **Quiz 1:** Will take place at the **beginning of class (6:00 PM – 6:30 PM)**.
  - **Format:** On Brightspace, likely multiple choice, requires a digital device (laptop/tablet/phone).
  - **Content:** Covers the **textbook**, not just the lecture slides.
- **Written Exam (March):**
  - Tentatively 2 hours long with ~10 problems.
  - Requires writing descriptions/discussions (4–6 pages).
  - **Open note/Open book**, but **no digital devices** allowed.

---

### **II. Software Process Concepts**

* **Code and Fix:** The "pre-model" approach. Casual, free-form, lack of structure. Typical for hobbyists or indie game developers .
* **Software Process:** A set of related activities, methods, practices, and rules to develop, operate, maintain, and improve software.
  * Includes supporting processes like Configuration Management, QA, and Peer Reviews.
* **Software Development Life Cycle (SDLC):** A conceptual representation of stages a system passes through from inception to retirement.
* **SDLC Models:** Frameworks defining how SDLC stages are organized (e.g., Waterfall, Agile, Spiral). They are like "ready-made clothing"—you must customize them to fit your specific project context (steakhouse vs. baseball game) .

---

### **III. Traditional & Iterative Models**

#### **1. Waterfall Model**

* **Flow:** Requirements $\rightarrow$ Design $\rightarrow$  Implementation $\rightarrow$ Verification $\rightarrow$ Maintenance.
* **Characteristics:** Front-loaded elaboration. You never go back (rigid).
* **Usage:** Still the most commonly used methodology according to some surveys, often due to legacy or specific constraints.

#### **2. V-Model (and variants)**

* **Concept:** An extension of Waterfall where every development stage has a corresponding verification/testing phase .
* **Mechanism:** Allows going back if verification fails, but still a poor fit for highly evolutionary development.
* **Variations:**
  * **Double V:** Adds a third dimension (3D) for concurrent development.
  * **V with Multiple Deliveries:** Multiple V-cycles running concurrently.

#### **3. Rational Unified Process (RUP)**

* **Origins:** Created by Rational Software (acquired by IBM).
* **Best Practices:** Develop iteratively, manage requirements, use component-based architectures, model visually (UML), verify quality, and control changes.
* **OpenUP:** An open-source, lean version of RUP.

---

### **IV. The Spiral Lineage & ICSM**

* **History:** Developed by Dr. Barry Boehm (USC legend).
  * **Spiral (1988):** Risk-driven, multiple rounds (Feasibility $\rightarrow$ Concepts $\rightarrow$ Requirements).
  * **Win-Win Spiral (1994):** Based on Theory W (Stakeholder Win-Win).
  * **Anchor Point (1996):** Defined specific milestones.
  * **MBASE (1999):** Integrated product, process, and property models.
  * **ICSM (2010):** The "end game" model suitable for rapidly changing environments.


#### **Incremental Commitment Spiral Model (ICSM)**

* **Core Philosophy:** Promotes continuous risk evaluation. At each point, you decide to commit, go back, or stop based on evidence.
* **The 4 Principles of ICSM:**
  1. **Stakeholder Value-Based Guidance:** Based on **Theory W** (Enterprise Success Theorem). You succeed *if and only if* you make winners of your success-critical stakeholders .
     * *Scenario:* If developers win but users lose (bad product), everyone eventually loses.
  2. **Incremental Commitment & Accountability:** Opposes "Total Commitment" (Roulette) in favor of staged commitment (Poker/Blackjack).
  3. **Concurrent Multi-Discipline Engineering:** Activities (scoping, requirements, coding) happen in parallel but with varying intensity levels over time.
  4. **Evidence & Risk-Based Decisions:** Go/No-Go decisions are based on validated evidence (e.g., feasibility evidence description), not just a calendar schedule.

#### **Case Study: Bank of America MasterNet Failure**

* **Context:** Bank of America wanted a new Trust Management System (TMS) in the 80s.
* **The Mistake (Total Commitment):** Committed **$22 Million** and a **9-month** timeline upfront to a contractor (Premier Systems) without validating scalability.
* **The Outcome:** After 50+ months and $80 Million, the project was abandoned. 3.5 million lines of requirements (feature creep) and zero working demos.
* **Why it failed (ICSM perspective):**
  * Violated **Principle 1:** Ignored maintainers/operators (only listened to customer wishlists).
  * Violated **Principle 2:** Total commitment removed developer motivation (paid regardless of success).
  * Violated **Principle 4:** No evidence of scalability or feasibility collected before the big check was written.

---

### **V. Value-Based Software Engineering (VBSE)**

* **Definition:** Integrating value considerations into all engineering decisions to reconcile stakeholder objectives.
* **Theory W (Win-Win):**
  * **Theorem:** Enterprise success depends on making winners of success-critical stakeholders.
  * **Process:** Identify stakeholders $\rightarrow$ Identify win conditions $\rightarrow$ Negotiate Win-Win $\rightarrow$ Control progress.
* **Importance:** Software is intangible and volatile; value trade-offs (cost vs. quality vs. schedule) determine the outcome.

---

### **VI. Agile Methodologies**

- **Definition:** An umbrella term for a guiding philosophy (Manifesto) and set of principles.
- **The Agile Manifesto (2001):** 
  - Individuals and interactions **over** processes and tools.
  - Working software **over** comprehensive documentation.
  - Customer collaboration **over** contract negotiation.
  - Responding to change **over** following a plan.
  - *Note:* The instructor calls the manifesto "overly dramatic" and extreme; modern Agile has converged with models like ICSM (adding back some documentation and process for scale).

#### **1. Scrum**

- **Focus:** How a team organizes and manages work.
- **Roles:**
  - **Product Owner:** Champion of the product/business value.
  - **Scrum Master:** Champion of the process (facilitator).
  - **Development Team:** Champion of technical implementation.
- **Artifacts:**
  - **Product Backlog:** List of desired requirements/features.
  - **Sprint Backlog:** Tasks selected for the current sprint.
  - **Increment:** The deliverable of a sprint (must meet Definition of Done).
- **Events:** Sprint Planning, Daily Scrum, Sprint Review (demo), Sprint Retrospective (process improvement) .

#### **2. Extreme Programming (XP)**

- **Focus:** Pushes core **engineering practices** to the extreme.
- **Practices:** Frequent releases, shorter timeboxes, frequent communication, expecting change.
- **Drawbacks:** Requires unstable requirements, strong engineering discipline, and **high customer availability** (which is rare).

#### **3. Lean & Kanban**

- **Origins:** Toyota Production System (TPS).
- **Key Concepts:**
  - **Muda/Mura/Muri:** Types of waste (non-value added tasks, unevenness, overburdening).
  - **Kanban (Signboard):** Visualize workflow and **Limit Work In Progress (WIP)** to prevent bottlenecks (like traffic on the 405 freeway).

#### **4. Scaling Agile**

- Vanilla Agile (Scrum) struggles with scalability (large complex systems).
- **Solutions:** SAFe (Scaled Agile Framework), LeSS (Large-Scale Scrum), Nexus, Disciplined Agile. These add process layers back in to handle coordination.

---

### **VII. Anti-Patterns**

#### **General SE Anti-Patterns**

- **Brooks’s Law:** Adding manpower to a late software project makes it later (due to coordination overhead).
- **Feature Creep:** Uncontrolled growth of project scope after requirements are set.
- **Gold Plating:** Continuing work past the point of value (over-engineering).
- **God Object:** Putting too many functions/responsibilities into a single class/part of the design.
- **Dead Code:** Code that exists but is unreachable or purpose unknown.
- **Premature Optimization:** Optimizing for efficiency too early, often wasting effort.

#### **Agile-Specific Anti-Patterns**

* **Agile Theater:** "Doing" Agile (motions/ceremonies) without "Being" Agile (understanding the values).
* **ScrumBut:** "We do Scrum, *but*..." (making exceptions like skipping retrospectives or huge user stories).
* **Agile on the Fly:** Assuming Agile means "no planning" or purely ad-hoc work .

---

### **VIII. Industry Usage Statistics**
* **Small Projects (<50 people):** Tend to use **Iterative/Agile** models.
* **Large Projects (>10,000 people/High Budget):** Tend to use **Traditional** models (Waterfall/Hybrid).
* **Critical Projects:** Surprisingly, over half of "high criticality" projects use Agile.



# 2/9 Lecture 3

## Part 1: Analysis and Planning

The primary goal of software analysis and planning is to prevent project failure, which includes missing budgets, deadlines, or system requirements.

### Risk Analysis

Risk is the possibility of loss or injury involving uncertainties; it is not yet a problem.

- **Risk Exposure Calculation:** Risk exposure equals the probability of loss multiplied by the size of the loss.
- **Opportunity Exposure:** Risks can sometimes be turned into opportunities, where exposure is calculated by the probability of gaining something multiplied by the size of the gain.
- **Continuous Assessment:** Assessing risk helps determine "how much is enough" for tasks like testing or documentation, and helps you proactively tailor your processes.
- **Day-One Temptations to Avoid:** Do not assume it is too early to think about risks, do not rush to code before assessing risks, and do not ignore that risks exist out of optimism.

### Risk Management Strategies

- **Buying Information:** Spending a small amount early (e.g., prototyping) to gain information and reduce risk exposure.
- **Avoidance:** Choosing alternatives to completely bypass the risk.
- **Transfer:** Shifting the risk to another party, such as making the customer establish a risk reserve.
- **Reduction:** Taking immediate action to minimize potential impacts, like schedule delays.
- **Acceptance:** Absorbing the risk and potentially turning it into a competitive advantage.

### Cost Estimation

Cost estimation is a difficult but essential prediction of the effort and elapsed time needed for a project.

- **The Cone of Uncertainty:** Estimates are highly inaccurate at the beginning of a project and become more accurate as the project progresses and uncertainties decrease.
- **Top-Down Approach:** Uses historical data from similar projects for high-level, fast budgeting, but misses unique project details.
- **Bottom-Up Approach:** Breaks the project into individual tasks, offering high accuracy for well-defined scopes (like a sprint), but is highly time-consuming.
- **COCOMO II:** A statistical, black-box model created by Dr. Boehm relying on empirical data and regression analysis.
- **COCOMO Inputs:** Requires size metrics (traditionally thousands of source lines of code, or KSLOC) and scale/cost drivers (e.g., team cohesion, precedentedness) to calculate person-months of effort.
- **AI Considerations:** Writing code has become significantly cheaper with AI, meaning traditional size metrics like KSLOC may need to be heavily discounted today.

### Technical Debt

Technical debt is the accrued consequence of postponing difficult fixes, coined by Ward Cunningham.

- **The Debt Metaphor:** Shipping first-time code is like taking on debt; it speeds up development but counts as "interest" if not paid back promptly with a rewrite.
- **Major Causes:** Business pressures, conspiracy of optimism, and ignoring edge/rainy-day cases.
- **Categories:** Debt can be deliberate or inadvertent, and reckless or prudent.
- **Resolution Methods:** Solutions include the "Big Bang" (stopping new features to fix debt), establishing a dedicated fixing team, following the Boy Scout rule (fixing little and often), or integrating automated tools like SonarQube into the CI/CD pipeline.

------

## Part 2: Software Architecture

Software architecture encapsulates the set of principal design decisions about a system, serving as its construction blueprint.

### Core Architectural Concepts

- **Fundamental Truths:** Every application has at least one architecture, and architecture is not merely a single phase of development.
- **Temporal Aspect:** At any given point in time, a system has only one architecture, but this architecture changes over time as new design decisions are made.
- **Architectural Elements:** Architectures are made of components (processing/data elements), connectors (regulating interactions), and configurations/topology (specific associations between the two).

### Style, Patterns, and Models

- **Architectural Style:** A named collection of design decisions providing specific benefits, such as Client-Server or Peer-to-Peer.
- **Architectural Pattern:** Similar to a style, but applied more specifically to recurring design problems at a smaller scope.
- **Software Models:** Artifacts (like UML diagrams or natural language descriptions) that capture and document architectural design decisions.

### Architectural Analysis

- **Purpose:** Discovering important system properties early to reduce risk and verify completeness, consistency, compatibility, and correctness.
- **Analysis Types:** Includes static analysis, dynamic analysis, and scenario-driven analysis.

------

## Part 3: Prototyping and Testing

Both practices are essential to reduce risks, seek feedback, and validate assumptions before making expensive mistakes.

### Prototyping Basics

- **Definition:** An early sample, model, or release of a product built to buy information inexpensively and gather accurate requirements.
- **Throwaway Prototyping:** Built simply to learn information and then discarded.
- **Evolutionary Prototyping:** Building a robust prototype and refining it until it becomes the final product.
- **Horizontal Prototyping:** A broad view with no underlying depth, such as a static UI mockup built in Figma.
- **Vertical Prototyping:** A deep elaboration of a single subsystem or complex algorithm to ensure functionality.

### Testing Fundamentals

Testing is the process of operating a system under specified conditions to identify bugs or differences between existing and required conditions.

- **Verification:** Answering "Are we building the product right?" (matches intended design) .
- **Validation:** Answering "Are we building the right product?" (matches user needs) .
- **Exhaustive vs. Random:** Exhaustive testing (testing every possible input combination) is impossible in commercial systems, while random testing might miss critical areas.
- **Good Test Cases:** A strong test prioritizes high-impact areas and has a high probability of finding an undiscovered fault without needing to examine the whole codebase.

### Testing Methods and Levels

- **Black-Box Testing:** Testing to the specification without looking at the code.
- **Equivalence Partitioning:** Dividing input data into valid and invalid partitions and testing representative values from each.
- **Boundary Conditions:** Testing the edges of equivalence partitions, as errors heavily cluster around boundaries.
- **White-Box Testing:** Testing internal code structures, checking metrics like statement coverage, branch coverage, and basic condition coverage to spot unused logic or "dead code".
- **Testing Levels:** Ranges from micro to macro: Unit testing, Integration testing, System testing, Acceptance testing, and post-maintenance Regression testing.

### Quality of Service (QoS)

- **Non-Functional Requirements:** Represented by the "ilities" (usability, reliability, portability, etc.).
- **Testability:** QoS requirements are notoriously hard to test unless they are explicitly quantified.
- **Writing Better Requirements:** Requirements must be Specific, Measurable, Attainable, Realizable, and Traceable to be effectively tested.

------

## Part 4: DevOps

DevOps is a set of practices combining development and operations to reduce the time between committing a code change and placing it into production, while ensuring high quality.

### Continuous Delivery Pipeline Stages

- **Continuous Exploration:** Researching, architecting, and synthesizing new ideas and features.
- **Continuous Integration:** Developing the solution, automated building, testing end-to-end, and avoiding massive merge conflicts by merging code frequently.
- **Continuous Deployment:** Releasing verified solutions continuously to the production environment.
- **Release on Demand:** Decoupling deployments from actual user releases, stabilizing the solution, measuring business value, and reacting.

### Deployment and Monitoring Strategies

- **Feature Toggles:** Kill switches that allow code to be deployed but kept inactive until manually flipped.
- **Dark Launches:** Releasing features to a specific subset of users to test stability before a full release.
- **Blue-Green Deployment:** Maintaining two separate environments to achieve near-zero downtime during releases.
- **Telemetry and Intelligence:** Using full-stack monitoring and log collection systems to analyze user behavior and measure business hypotheses.
- **Recovery:** Version control and the ability to trigger a quick revert are essential fail-safes during deployment.



# 3/2 Lecture 4

**Date**: March 2, 2026

**Instructor**: Dr. Jay

------

### **1. Exam Logistics & Preparation**

- **Format**: The written exam will be 2 hours long and consist of 10 descriptive (written) questions. Expect to write 4 to 5 pages.
- **Rules**: Open note and open book, but **analog only**—no electronics allowed.
- **Preparation**: Create a physical cheat sheet. Printing slides multiple to a page (e.g., 8 per page) is recommended to save paper . The exam covers the *lectures*; the textbook is primarily for quizzes .
- **DEN (Remote) Students**: The exam will appear on Brightspace at exactly 6:00 PM PT . Students write answers on blank paper and get an extra 30 minutes to scan and upload their work . Local DEN students may take the exam in person if they coordinate with the instructor ahead of time .

------

### **2. Software Maintenance**

- **Definition**: The modification of a software product after delivery to correct faults, improve performance, or adapt the product to a modified environment .
- **The "Iron Law" of Maintenance**: Useful software systems will spend twice as much on software maintenance as they did for development. Maintenance can account for up to 90% of software lifecycle costs, significantly higher than hardware (12-84%) .
- **Types of Maintenance** :
  1. **Preventive**: Detecting and correcting latent faults *before* they manifest.
  2. **Corrective**: Reactive modification to fix discovered faults.
  3. **Perfective**: Improving performance or maintainability proactively.
  4. **Adaptive**: Modifying the system to cope with a changing environment.
- **COTS (Commercial Off-The-Shelf) Products**: Using third-party libraries, SaaS, and open-source APIs saves initial costs but is a "maintenance headache" because developers have no control over updates, security vulnerabilities, or broken interfaces .
- **Maintenance in the AI Era**: AI tools boost throughput but reduce delivery stability, causing developers to rewrite ("churn") code much faster . AI-generated code frequently violates the "DRY" (Don't Repeat Yourself) principle and lacks architectural awareness due to limited context windows .

------

### **3. Software Engineering Best Practices**

- **The Triple Constraint**: In project management, you have Time, Cost, and Scope. You can only pick two . For example, if you are strictly bound by time and fall behind, you must reduce the scope or increase the budget .
- **Rational Unified Process (RUP) 6 Best Practices** :
  1. Develop software iteratively.
  2. Manage requirements (crucial today, as bad inputs to LLMs yield worse code).
  3. Use component-based architectures (separation of concerns).
  4. Visually model software.
  5. Verify software quality.
  6. Control changes to avoid feature creep.
- **AI-Era Survival Skills**: Treat AI output as a draft. Adopt a **Verification-First** engineering approach where your test suite acts as your safety net and "oracle" . Human peer review for AI code is non-negotiable. Integrate static analysis and linters into CI/CD pipelines to automatically block flawed AI code from being merged .

------

### **4. Classic & New Mistakes**

- **People Mistakes**: Adding people to a late project, failing to deal with problem employees, or ignoring user input .
- **Process Mistakes**: Making overly optimistic schedules.
- **Product Mistakes**: "Gold Plating" (working past the point of adding value), Feature Creep (uncontrolled expansion of scope), and Developer Gold Plating (adopting shiny new technologies instead of boring, stable ones) .
- **Technology Mistakes**: "Silver Bullet Syndrome" (expecting a new tech to solve all essential problems) and switching tools mid-project .
- **Modern AI Mistakes**: Blind trust in AI outputs without review (the modern equivalent of "cowboy programming"). Studies show developers using AI write *less* secure code but remain overconfident in its security.

------

### **5. Laws of Software Engineering**

- **Bernoulli’s Principle**: Work of smaller teams proceeds faster than that of larger teams (especially true today with AI amplification) .
- **Boehm’s Law**: Errors are most frequent during requirements/design and are exponentially more expensive to fix the later they are caught .
- **Brooks’s Law**: Adding people to a late software project makes it later.
- **Conway’s Law**: A piece of software will reflect the organizational structure that produced it (e.g., three sub-teams will naturally produce a three-component architecture) .
- **Crosby’s Law**: "Quality is free." Spending effort early on quality prevents massive rework costs later .
- **Humphrey’s Law**: Users do not know what they want a system to do until they actually see it working (hence the need for prototypes) .
- **Goodhart’s Law**: When a measure becomes a target, it ceases to be a good measure. If you target "number of PRs merged," developers will game the system by splitting work into tiny, meaningless PRs .
- **Knuth's Principle**: Premature optimization is the root of all evil.
- **Parkinson’s Law**: Work expands to fill the time available for its completion.
- **Pareto Principle (80/20 Rule)**: >80% of software bugs are found in <20% of the software modules.
- **The 90-90 Rule**: The first 90% of the code takes 90% of the development time; the remaining 10% of the code takes the *other* 90% of the time .

------

### **6. Software Engineering Ethics**

- **Context**: Software engineers hold immense power over public harm/good, security, and privacy, especially with the rise of autonomous AI systems making nanosecond decisions .
- **Rawls' Theory of Justice**: Utilize a "veil of ignorance"—deliberately step outside your race, class, gender, and status to design a system that protects the least advantaged stakeholders .
- **The Publicity Test**: Before shipping a feature, ask yourself if you could defend your ethical determination with honor before an informed public or press .
- **AI Ethics Challenges**:
  - Bias and amplification (e.g., AI resume screeners showing bias).
  - The Accountability Gap: If AI generates harmful code, the human engineer is still fully responsible.
  - Unresolved IP and copyright issues stemming from LLMs trained on open-source code.

------

### **7. The History & Future of SE**

- **1950s:** Software was treated like hardware.

- **1960s:** The "Cowboy era" of handcrafting code .

- **1970s:** Formal Waterfall processes.

- **1980s:** Object-oriented programming and the realization that there is "no silver bullet" to fix essential complexity .

- **2000s:** The rise of Agile.

- **The Future (2026+)**: Legacy systems (like COBOL programs from the 1970s) never go away and require continuous upkeep . AI will allow engineers to build systems that are 10 times more complex with the same manpower, placing a premium on human architectural/system-level thinking rather than raw coding speed .

  

  