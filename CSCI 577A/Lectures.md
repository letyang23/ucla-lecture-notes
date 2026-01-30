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
