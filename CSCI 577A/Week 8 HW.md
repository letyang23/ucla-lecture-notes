# Chapter 15 – Google’s Quality Approach – Homework

**Question 5**
Analytical: Why does Google minimize End-to-End tests?

**Answer:**

Google strategically minimizes End-to-End (E2E) tests due to three primary factors:

- **High Complexity:** They are difficult to set up and manage because they test the entire system from the user interface down to backend services and databases.
- **Longer Execution Times:** Because they validate complete workflows across the system, they run much slower than isolated tests, which delays feedback to developers.
- **Higher Maintenance Costs:** They are more prone to breaking when minor changes are made (flakiness), requiring constant upkeep.

Instead of relying heavily on E2E tests, Google uses a "Testing Pyramid" approach. They build a massive foundation of fast, cheap unit and integration tests, reserving E2E tests (which make up only about 5% of their test suite) strictly for validating critical user journeys.



# Chapter 16 – Microsoft Quality Management – Homework

**Question 4**

Short Answer: Explain shift-left testing.

**Answer:**

Based on the textbook, shift-left testing is the practice of moving quality assurance and testing activities earlier (to the "left") in the software development lifecycle.

Key aspects of this approach include:

- **Early Detection:** The primary goal is to catch defects as early as possible in the development process, which makes them significantly cheaper and easier to fix compared to finding them right before release.
- **Developer-Owned Quality:** It shifts the responsibility of quality away from a separate, isolated QA team and makes it a shared responsibility.
- **Empowerment:** Developers are given the tools, frameworks, and responsibility to thoroughly test their own code (such as writing unit tests and doing peer code reviews) from the very beginning of the project.



###### AI Usage Disclosure 

In the completion of this assignment, I used AI tool (Google Gemini) to help in synthesizing the provided course readings and structuring the final responses.