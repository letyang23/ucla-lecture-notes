# PageRank (PR) - Quick Cheat Sheet

## Base Formula:

$$
PR(A) = (1 - d) + d \left(\frac{PR(B)}{C(B)} + \frac{PR(C)}{C(C)} + \dots \right)
$$

- **d**: Damping factor (~0.85 generally)
- **C(X)**: Number of outgoing links from X

------

## Important facts:

- Initial PR guess **doesn't matter**, converges eventually.
- After convergence, the average PR = 1.0 for the entire graph.
- Each page initially gets a PR of at least **0.15** (assuming d=0.85).
- PR converges faster with mid-range damping value (0.85 ideal).
- Too high d → slow convergence; Too low d → oscillations.

------

## Convergence & Calculation Methods:

- Can use previous step PR values (correct way)
- Using current values (instead of previous step values) still converges.

------

## Effect of Structure on PageRank:

| Graph Structure                            | PR Distribution Observation     |
| ------------------------------------------ | ------------------------------- |
| Single page/no in-links ("Sink")           | Gets minimum PR (e.g., 0.15).   |
| Simple hierarchy / no external outlinks    | Concentrates PR upward          |
| Lots of internal links/fully meshed        | Equalizes PR distribution       |
| Linking internally protects & retains PR   | Internal links helpful          |
| External links without reciprocal incoming | Decrease average PR             |
| External back-links to home                | Increase PageRank significantly |
| Loop Structure                             | Equal distribution of PR        |

- PR amplifies with good site structure (Hierarchical & internal links).

------

## PageRank Misuse (spam/cheating):

- **Link farms**: Sites artificially created solely to boost page PR.
- Google's countermeasure: set offending page's PR to very low.

------

## Suggestions for Increasing Good PR:

- Internal linking helps retain PR (especially crucial if using external links).
- Use hierarchical structuring for key pages.
- Pages linking outward: more internal linking helps preserve PR.
- Pages without outward links: internal structure less critical for PR (focus usability).
- Add site map linking from each page to boost internal linking & usability.

------

## Important Considerations for SEO and Google:

- PR is just **one** of many Google ranking signals.
- CONTENT IS STILL MOST IMPORTANT:
  - Anchor text, page titles, headings critically affect rank.
- PageRank alone guarantees nothing—keyword relevance & on-page SEO equally vital.