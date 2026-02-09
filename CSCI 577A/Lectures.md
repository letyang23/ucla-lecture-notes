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