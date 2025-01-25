# Homework 1

1. Consider the G-S algorithm for n men and n women. What is the maximum number of times a man may be rejected as a function of n? Give an example where this happens. (5pts)

   **Answer:**

   The maximum number of times a man may be rejected is $n-1$ times in the G-S algorithms.

   Example:

   Suppose all men share the same preference list: $w_1 > w_2 > w_3 > ... > w_n$

   and all women share the same preference list: $m_2>m_3>m_4 >...>m_n>m_1$

   Then man $$m_1$$ proposes to $$w_1$$ first and gets rejected (when $$m_2$$ also proposes to her), then to $$w_2,$$ and so on, being rejected by each of the first $$n-1$$ women. He is finally accepted by $$w_n$$ , sums up to $$n-1$$ rejections.

   

2. Determine whether the following statement is true or false. If it is true, give a short explanation. If it is false, give a counterexample. (5pts) 

   For all n ≥ 2, there exists a set of preferences for n men and n women such that in the stable matching returned by the G-S algorithm when men are proposing, every man is matched with their most preferred woman.

   **Answer:**

   The statement is true, because we could construct a preference set where each man's first choice be the woman with the same index, and vice versa.

   For example, label the men $$m_1, m_2, \dots, m_n$$ and the women $$w_1, w_2, \dots, w_n$$. Suppose each man $$m_i$$ ranks woman $$w_i$$ as his top choice, and each woman $$w_i$$ ranks man $$m_i$$ as her top choice. (They can rank the rest in any order.)  

   In this scenario, when the men propose in the Gale–Shapley algorithm:

   Each man $$M_i$$ first proposes to his top choice $$W_i$$. And each woman $$W_i$$ receives exactly one proposal from her top choice $$M_i$$. Since every woman prefers her proposer over being unmatched, she accepts.

   As a result, every man is matched with his top choice. This construction works for all $$n \ge 2$$.



3. Solve Kleinberg and Tardos, Chapter 1, Exercise 3.

   There are many other settings in which we can ask questions related to some type of “stability” principle. Here’s one, involving competition between two enterprises.

   Suppose we have two television networks, whom we’ll call A and B. There are n prime-time programming slots, and each network has n TV shows. Each network wants to devise a schedule—an assignment of each show to a distinct slot- so as to attract as much market share as possible. 

   Here is the way we determine how well the two networks perform relative to each other, given their schedules. Each show has a fixed rating, which is based on the number of people who watched it last year; we’ll assume that no two shows have exactly the same rating. A network wins a given time slot if the show that it schedules for the time slot has a larger rating than the show the other network schedules for that time slot. The goal of each network is to win as many time slots as possible.

   Suppose in the opening week of the fall season, Network A reveals a schedule S and Network B reveals a schedule T. On the basis of this pair of schedules, each network wins certain time slots, according to the rule above. We’ll say that the pair of schedules (S, T) is stable if neither network can unilaterally change its own schedule and win more time slots. That is, there is no schedule S' such that Network A wins more slots with the pair (S', T) than it did with the pair (S, T); and symmetrically, there is no schedule T' such that Network B wins more slots with the pair (S, T') than it did with the pair (S, T).

   The analogue of Gale and Shapley’s question for this kind of stability is the following: For every set of TV shows and ratings, is there always a stable pair of schedules? Resolve this question by doing one of the following two things:

   (a) give an algorithm that, for any set of TV shows and associated ratings, produces a stable pair of schedules; or

   (b) give an example of a set of TV shows and associated ratings for which there is no stable pair of schedules.

   **Answer:**

   False. There does not always exists a stable pair of schedules.

   There does *not* always exist a stable pair of schedules. In other words, one can find ratings for two sets of shows (Network A’s shows and Network B’s shows) such that *no* assignment of shows to time slots by A and B is stable. Here is a counterexample for the case $$n=3$$:

   - **Network A’s shows**:  
     - $$A_1 = 10,\, A_2 = 2,\, A_3 = 1.$$
   - **Network B’s shows**:  
     - $$B_1 = 9,\, B_2 = 3,\, B_3 = 0.$$

   A show with a higher rating always beats a show with a lower rating if they are placed in the same slot. Whenever one network picks a schedule, the other network can re-arrange its shows to win more time slots than before, so no pair of schedules is stable.

   For example, if:
   - A schedules its shows in order $$(A_1, A_2, A_3)$$ across the three slots, and  
   - B schedules its shows in order $$(B_1, B_2, B_3),$$

   then A wins 2 slots and B wins 1 slot. However, B can unilaterally change its schedule to $$(B_3, B_1, B_2)$$ and end up winning 2 slots instead. But with that new schedule for B, A can then re-arrange *its* shows and win 2 slots again. One can check all possible permutations in a similar fashion and see that each time one network can improve its outcome by unilaterally deviating from the pair of schedules. Thus, no choice of schedules by A and B remains stable.

   Because we can exhibit such a counterexample, the answer is that there is *not* necessarily a stable pair of schedules for every possible set of shows and ratings.



4. Solve Kleinberg and Tardos, Chapter 1, Exercise 4.

   Gale and Shapley published their paper on the Stable Matching Problem in 1962; but a version of their algorithm had already been in use for ten years by the National Resident Matching Program, for the problem of assigning medical residents to hospitals. 

   Basically, the situation was the following. There were m hospitals, each with a certain number of available positions for hiring residents. There were n medical students graduating in a given year, each interested in joining one of the hospitals. Each hospital had a ranking of the students in order of preference, and each student had a ranking of the hospitals in order of preference. We will assume that there were more students graduating than there were slots available in the m hospitals.

   The interest, naturally, was in finding a way of assigning each student to at most one hospital, in such a way that all available positions in all hospitals were filled. (Since we are assuming a surplus of students, there would be some students who do not get assigned to any hospital.) We say that an assignment of students to hospitals is stable if neither of the following situations arises.

   - First type of instability: There are students s and s', and a hospital h, so that
     - s is assigned to h, and
     - s' is assigned to no hospital, and
     - h prefers s' to s. 
   - Second type of instability: There are students s and s', and hospitals h and h', so that
     - s is assigned to h, and
     - s' is assigned to h', and
     - h prefers s' to s, and
     - s' prefers h to h'. 

   So we basically have the Stable Matching Problem, except that (i) hospitals generally want more than one resident, and (ii) there is a surplus of medical students. 

   Show that there is always a stable assignment of students to hospitals, and give an algorithm to find one.

   **Answer:**

   1. Initialize all students as “free” and all hospitals as having all their slots empty.
   2. While there is a free student (who still has at least one hospital on their list):
      - The student proposes to the most-preferred hospital on their list to which they have not yet proposed.
      - The hospital tentatively accepts the student if:
        1. It still has space available, or
        2. It is currently holding its capacity of students but *prefers* the new proposer over its least-preferred currently held student.
      - If the hospital is already full and prefers the newly proposed student to its worst current tentative match, it rejects its worst current match (who becomes free) and tentatively accepts the new student.
      - Any student who gets rejected remains free (and tries the next hospital on their list in a future step).
   3. End condition: Once no free student can make a new proposal (i.e., all have either been matched or exhausted their lists), the algorithm terminates.

   This resulting assignment is **stable**, in the sense that:
   - No hospital will want to replace one of its tentatively matched students with an unmatched student they prefer (first type of instability), and
   - No hospital–student pair will both prefer each other to their current matches (second type of instability).

   Why it is stable:
   - If there were a hospital $$h$$ and an unmatched student $$s'$$ with $$h$$ preferring $$s'$$ to one of its current students, $$s'$$ would have proposed to $$h$$ before proposing to less-preferred hospitals (or going unmatched). But if $$h$$ is at capacity, it only rejects (or replaces) a student if it finds someone it prefers more. Hence $$h$$ must prefer all its final matches to $$s'$$.
   - Similarly, if there were two matched students $$s, s'$$ and two hospitals $$h, h'$$ with $$s$$ at $$h$$ and $$s'$$ at $$h'$$ such that $$h$$ prefers $$s'$$ and $$s'$$ prefers $$h$$, that would mean $$s'$$ must have proposed to $$h$$ before ever proposing to $$h'$$. Since $$h$$ ended with $$s$$ instead of $$s'$$, that means $$h$$ either had no space or found $$s$$ to be more preferable than $$s'$$. So $$h$$ would not want to switch.

   Thus, this algorithm always finds a stable assignment.



5. Consider a stable marriage problem where the set of men is given by $$M = \{m_1, m_2, \dots, m_n\}$$ and the set of women is $$W = \{w_1, w_2, \dots, w_n\}$$. Consider their preference lists to have the following properties:

   - $$\forall w_i \in W$$: $$w_i$$ prefers $$m_i$$ over $$m_j$$		 $$\forall j > i$$
   - $$\forall m_i \in M$$: $$m_i$$ prefers $$w_i$$ over $$w_j$$ 		$$\forall j > i$$

   Prove that a unique stable matching exists for this problem.

   Note: The $$\forall$$ symbol means "for all".

   **Answer:**

   We claim that the only stable matching is $$\{(m_i, w_i) \mid 1 \le i \le n\}$$.

   1. **It is stable.** 
      Suppose there were a blocking pair $$(m_x, w_y)$$. Then they would each prefer one another to their current partners. Consider the two cases:

      - **Case $$x < y$$.** 
        Since $$\forall j > i,\; m_i \text{ prefers } w_i \text{ to } w_j,$$ 
        man $$m_x$$ prefers $$w_x$$ over $$w_y$$. 
        So $$m_x$$ would not want to deviate with $$w_y$$.

      - **Case $$x > y$$.** 
        Since $$\forall j > i,\; w_i \text{ prefers } m_i \text{ to } m_j,$$ 
        woman $$w_y$$ prefers $$m_y$$ over $$m_x$$. 
        So $$w_y$$ would not want to deviate with $$m_x$$.

      Thus no pair $$(m_x, w_y)$$ can block the proposed matching.

   2. **It is the unique stable matching.** 
      Run the Gale–Shapley algorithm where men propose:
      
      - Each man $$m_i$$ will propose to $$w_i$$ first (since she is his most preferred).  
      - Woman $$w_i$$, when faced with any man $$m_k$$ such that $$k > i$$, prefers $$m_i$$ to $$m_k$$. Thus she will never “upgrade” from $$m_i$$ to such $$m_k$$.  
      - Through standard Gale–Shapley dynamics, no other man will dislodge $$m_i$$ from $$w_i$$.  
      
      Therefore, each $$m_i$$ ends up matched to $$w_i$$. By Gale–Shapley theory, this outcome is stable—and no other stable outcome can exist. Hence $$\{(m_i, w_i)\}$$ is *uniquely* stable.



6. State True/False: An instance of the stable marriage problem has a unique stable matching if and only if the version of the Gale-Shapely algorithm where the male proposes and the version where the female proposes both yield the exact same matching. (10pts)

   **Answer: True**

   If there is a unique stable matching, it must simultaneously be the man-optimal and woman-optimal stable matching (since no other stable pairings exist). Thus, both the male-proposing and female-proposing Gale-Shapley (G-S) algorithms will produce this unique matching.

   The male-proposing G-S yields the man-optimal stable matching, and the female-proposing G-S yields the woman-optimal stable matching. If these two matchings are identical, there can be no other stable matchings (as optimality for one group implies pessimality for the other, and they coincide). Hence, the stable matching is unique.

   In conclusion, if these two matchings turn out to be identical, it follows that this unique matching is the only stable matching possible for that instance of the problem. 