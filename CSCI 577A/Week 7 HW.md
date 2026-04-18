# Chapter 13  SPACE Framework Homework

**Assignment 8** Scenario: A team has high deployment frequency but rising defect rates. Which SPACE tradeoff might be occurring?

**Answer**

This scenario illustrates a classic tradeoff between the Efficiency and Flow dimension and the Performance dimension within the SPACE framework.

- High Deployment Frequency (Efficiency and Flow): The team is successfully optimizing for speed. They have minimized delays and are moving code rapidly through the pipeline into production, which is a key indicator of high efficiency and flow.
- Rising Defect Rates (Performance): The team is experiencing a decline in outcomes and software quality. Performance in the SPACE framework emphasizes the actual value and reliability of the software delivered, not just the speed at which it is pushed.

The Tradeoff Occurring: According to the textbook (specifically Section 7.4), the team is likely aggressively maximizing speed and system flow without paying adequate attention to quality controls. By pushing code too quickly without thorough testing, code reviews, or stable integration practices, they are negatively impacting the "Performance" dimension by introducing more defects and increasing the change failure rate in production. The framework highlights that while speed is important, it must be balanced with the quality of the outcome.



# Chapter 14 – AI/ML in Software Quality – Homework

**Assignment 5** Analytical: Compare traditional automation vs AI-driven testing.

##### Answer

Traditional test automation and AI-driven testing represent two fundamentally different approaches to software quality assurance. Traditional automation is highly deterministic, whereas AI-driven testing introduces adaptability and continuous learning.

Here is a breakdown of their primary differences:

| **Feature**            | **Traditional Automation**                                   | **AI-Driven Testing**                                        |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Foundational Logic** | Operates on strict, hard-coded logic and explicit instructions provided by an engineer. | Learns from historical data (defect logs, test reports, user flows) to make intelligent decisions without explicit programming. |
| **Adaptability**       | Rigid and highly brittle. Scripts frequently break when minor UI or API changes occur, requiring constant manual maintenance. | Highly adaptive. Models can recognize perceptual changes versus actual breakage and adjust to evolving codebases dynamically. |
| **Test Generation**    | Test cases must be manually written from scratch.            | Can auto-generate or suggest test cases by inferring patterns from user journeys, logs, and API traffic. |
| **Scope & Coverage**   | Only tests the exact paths and scenarios that developers explicitly script. | Capable of broader coverage by exploring untested paths, predicting high-risk areas, and identifying edge cases human testers might miss. |

Ultimately, while traditional automation is excellent for strictly repetitive and unchanging tasks, AI-driven testing is necessary for the fast-paced, iterative environments of Agile and DevOps where applications constantly evolve.



###### AI Usage Disclosure 

In the completion of this assignment, I used AI tool (Google Gemini) to help in synthesizing the provided course readings and structuring the final responses.