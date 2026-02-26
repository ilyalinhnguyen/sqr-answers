# Revision Questions — Answers

Answers to all revision questions from Adequacy Criteria, Input Domain Testing, Random Testing, and Exploratory Testing & OP.

---

# Part 1: Adequacy Criteria (L04)

## Q1: Coverage Categories
| Category | Focus |
|----------|-------|
| A. White Box | 2. Code structure |
| B. Black Box | 1. Input space |
| C. Mutation | 4. Fault detection |
| D. Requirements | 3. Specification |

## Q2: Coverage Formula
$$\text{Coverage} = \frac{\text{Executed}}{\text{Total}} \times 100\% = \frac{45}{60} \times 100\% = 0.75 \times 100\% = \mathbf{75\%}$$

## Q3: Two Uses of Coverage
1. **Generator:** Create tests to satisfy the criterion (e.g., write tests until 80% branch coverage)
2. **Measure:** Evaluate existing tests (e.g., report current coverage percentage)

## Q4: Statement Coverage Weakness
When `condition=True`, x=4, so `y = z/x` runs without error. When `condition=False`, x stays 0 and causes division by zero. 100% statement coverage misses the False branch where the bug occurs.

## Q5: Branch vs Statement
- **Branch coverage:** 2 tests (one for True, one for False)
- **Statement coverage:** 1 test
- Branch needs roughly 2× the number of tests for decisions.

## Q6: Compound Predicate Problem
For `if (A && B)`, branch coverage only tests (T,T) and (F,any). The combination **A=true, B=false** is never tested. This misses faults where both conditions are evaluated and the logic is wrong (e.g., AND vs OR).

## Q7: Cyclomatic Complexity
$$V(G) = E - N + 2 = 10 - 8 + 2 = \mathbf{4}$$
(where E = edges, N = nodes)

## Q8: Alternative Formula
V(G) = D + 1 = 5 + 1 = **6** (where D = number of decision points)

## Q9: Basis Path vs All Paths
Basis path coverage grows linearly (D+1); all-path grows exponentially (2^D). For many decisions, all-path is infeasible.

| Decisions | All Paths | Basis Paths |
|-----------|-----------|-------------|
| 4 | 2⁴ = **16** | 4+1 = **5** |
| 10 | 2¹⁰ = **1,024** | 10+1 = **11** |

## Q10: Unfeasible Paths
An unfeasible path is one that is structurally possible in the CFG but cannot be executed because of semantic constraints (e.g., two consecutive `if (x > 0)` blocks with the same x; the path where the first is true and the second is false is impossible).

## Q11: Condition Coverage Test Count
For `if (A && B)` (2 conditions):

| Coverage Type | Calculation | Tests Required |
|---------------|-------------|----------------|
| Basic Condition | Each condition T/F once → 2 | **2** |
| Multiple Condition | 2^n = 2² | **4** |
| MC/DC | n+1 = 2+1 | **3** |

## Q12: MC/DC Requirements
1. Every **decision** takes both true and false
2. Every **condition** takes both true and false
3. Each condition **independently** affects the decision (changing only that condition changes the outcome)

## Q13: MC/DC vs Multiple Condition Test Count
- MC/DC: n+1 = 5+1 = **6** tests
- Multiple Condition: 2^n = 2⁵ = **32** tests
- MC/DC uses far fewer tests (6 vs 32).

## Q14: MC/DC Independence Pairs for (A && B && C)
| Test | A | B | C | Result | Independence Pair |
|------|---|---|---|--------|-------------------|
| T1 | T | T | T | T | Baseline |
| T2 | F | T | T | F | A |
| T3 | T | F | T | F | B |
| T4 | T | T | F | F | C |

T1↔T2 shows A; T1↔T3 shows B; T1↔T4 shows C.

## Q15: MC/DC Standards
| Standard | Domain |
|----------|--------|
| DO-178C | Aerospace |
| ISO 26262 | Automotive |
| IEC 62304 | Medical |

## Q16: Mutation Score
$$\text{Mutation Score} = \frac{\text{Killed}}{\text{Total} - \text{Equivalent}} = \frac{72}{100-10} = \frac{72}{90} = 0.8 = 80\\%$$

## Q17: Mutation Operators (5 categories)
1. **Arithmetic (AOR):** `a + b` → `a - b`
2. **Relational (ROR):** `x < 5` → `x <= 5`
3. **Logical (LCR):** `A && B` → `A || B`
4. **Constant:** `x = 0` → `x = 1`
5. **Statement:** Delete a statement (e.g., remove `x++`)

## Q18: Pairwise Testing
- Exhaustive: 4 params × 3 values each = 3⁴ = **81** combinations
- Pairwise: typically ~**9–15** tests (covers all pairs)
- Sufficient because ~90% of faults are triggered by 1–2 way interactions (NIST research).

## Q19: N-Switch Coverage
- **0-switch:** All states (few tests)
- **1-switch:** All single transitions (moderate tests)
- **2-switch:** All pairs of consecutive transitions (many tests)

## Q20: Coverage Limitations
| Coverage Measures | Does NOT Measure |
|-------------------|------------------|
| Code executed | Oracle correctness |
| Paths traversed | Missing code |
| Conditions tested | Requirements coverage |

## Q21: Size Confounding
Inozemtseva & Holmes: Correlation drops to **~0** when controlling for **test suite size**. About **69–82%** of the coverage–effectiveness correlation is explained by test suite size.

## Q22: Assertions vs Coverage
Zhang & Mesbah: **Assertion quantity** (correlation ~0.927–0.973) has a stronger correlation with effectiveness than coverage. Assertions measure verification; coverage measures exploration.

## Q23: Coverage Criteria Effectiveness (Hemmati)
- Statement coverage: **10%** of faults
- Data-flow coverage: **85%** of faults

## Q24: Coverage Anti-Patterns
1. **Tests designed for coverage** → weak suites
2. **Using coverage as shipping gate** → threshold gaming (e.g., clustering at 85%)
3. **Ignoring low coverage** → missing process signals

## Q25: Coverage Level Selection
| Context | Criterion |
|---------|-----------|
| A. Minimum bar | 2. Statement |
| B. Default for unit tests | 3. Branch |
| C. Safety-critical (DO-178C A) | 1. MC/DC |
| D. Complex control flow | 4. Basis Path |

## Q26: Coverage Targets
| Coverage | Min | Target |
|----------|-----|--------|
| Statement | 70% | 80% |
| Branch | 75% | 85% |
| Mutation | 60% | 80% |

## Q27: Tool Matching
| Tool | Language |
|------|----------|
| A. JaCoCo | 2. Java |
| B. Coverage.py | 1. Python |
| C. LLVM-cov | 4. C/C++ |
| D. c8 | 3. JavaScript |

## Q28: Oracle Problem
The **oracle problem** is the difficulty of deciding the correct output for a given input. Mitigations: assertions, specifications, differential testing, crash detection, reference implementations.

## Q29: Branch Coverage and Mutation Relation
Neither fully subsumes the other. Branch coverage focuses on control flow; mutation tests fault detection. A suite can have high branch coverage but low mutation score (weak assertions), or the reverse.

## Q30: Branch vs Statement (Practical)
Branch coverage requires both outcomes of each decision. Example: `if (x > 0) x = 1; y = 1/x;` — one test with x=1 gives 100% statement coverage but misses the division-by-zero path when x=0; branch coverage would require a test with x≤0.

## Q31: MC/DC for ((A || B) && C)
a) Multiple Condition: 2^n = 2³ = **8** tests  
b) Minimal MC/DC: n+1 = 3+1 = **4** tests, e.g. (T,T,T), (F,T,T), (T,F,T), (T,T,F)  
c) Independence pairs: A via (T,T,T) vs (F,T,T); B via (T,T,T) vs (T,F,T); C via (T,T,T) vs (T,T,F)

## Q32: Critical Analysis
95% coverage does not imply thorough testing. Research shows: coverage–effectiveness correlation drops when controlling for size; assertion count matters more than coverage; statement coverage detects ~10% of faults. Coverage measures exploration, not correctness or oracle quality.

---

# Part 2: Input Domain Testing (L05)

## Q1: Core Definitions
| Term | Definition |
|------|------------|
| A. Test Case | 3. Input + expected output + oracle |
| B. Test Suite | 4. Collection of test cases |
| C. Oracle | 1. Mechanism to determine correct output |
| D. Test Input | 2. Values provided to system |

## Q2: Positive Test Bias
Testers tend to use inputs they expect to work. It reduces coverage of invalid inputs and edge cases; negative testing must be planned explicitly.

## Q3: Black-Box vs White-Box
Use **black-box** testing: test against the specification (API behavior) without source code. Suitable for payment gateway APIs defined by contracts and expected responses.

## Q4: Partition Requirements
1. **Complete:** Every input belongs to some partition  
2. **Disjoint:** No input belongs to more than one partition

## Q5: Weak vs Strong EP
- Weak EP: max(classes per variable) = max(4, 3, 5) = **5** tests  
- Strong EP: product of all classes = 4 × 3 × 5 = **60** tests

## Q6: Email Equivalence Classes
Examples: invalid format, missing @, multiple @, domain without TLD, valid short, valid long, empty, special characters only, whitespace, SQL-injection-like input.

## Q7: Partition Heuristics
| Heuristic | Example |
|-----------|---------|
| A. Range-based | 2. Age groups (0–12, 13–19, 20–64, 65+) |
| B. Enumeration | 1. US regions (Northeast, South, Midwest, West) |
| C. Error types | 3. Input causing "File not found" |

## Q8: Boundary Fault Types
| Bug | Type |
|-----|------|
| A | Closure bug (wrong operator) |
| B | Boundary shift (constant off) |
| C | Missing boundary |

## Q9: ON/OFF Points for x >= 100
a) ON point: **100**  
b) OFF point: **99** (just below)  
c) Boundary is **closed** (≥)

## Q10: BVA Test Count (3 variables)
With k = 3:
- Basic BVA: 4k + 1 = 4×3 + 1 = **13** tests  
- Robust BVA: 6k + 1 = 6×3 + 1 = **19** tests

## Q11: Closed vs Open Intervals (1 < x < 100)
For open interval: ON points at **2** and **99** (just inside); OFF points at **1** and **100** (on the boundary, outside valid range).

## Q12: BVA Limitations
1. Assumes case-like processing (no complex loops)  
2. Coincidental correctness  
3. ε-limits vary across platforms; OFF points can be ambiguous

## Q13: Decision Table Components
1. **Conditions** — input variables  
2. **Condition values** — Y/N or enumerated  
3. **Rules** — columns (combinations)  
4. **Actions** — outputs for each rule  

## Q14: Rule Count (3 binary conditions)
Number of rules = product of condition values = 2 × 2 × 2 = 2³ = **8** rules before consolidation

## Q15: Checksum Verification
Checksum: sum of "covers" per consolidated rule must equal original rule count.
$$2 + 3 + 1 + 4 + 2 = 12 \quad \checkmark$$
Matches original 12 rules → consolidation is correct.

## Q16: Beizer 8-Step Order
1. List actions  
2. List conditions with values  
3. Calculate number of rules  
4. Fill columns with combinations  
5. Specify expected outputs per rule  
6. Consolidate (don't-cares)  
7. Verify checksum  
8. Develop test cases (one per rule)

## Q17: When to Use Decision Tables
| Scenario | Good Fit? |
|----------|-----------|
| A. Tax calculation | Yes |
| B. Performance testing | No |
| C. Access control (role, dept, time) | Yes |
| D. Continuous output | No |

## Q18: NIST 90% Finding
~**90%** of software failures are triggered by 1–2 way parameter interactions (Kuhn et al.).

## Q19: Pairwise Test Reduction
34 binary switches:
- All combinations: 2³⁴ = **17,179,869,184** tests  
- Pairwise (2-way): ~**29** tests (covers all pairs of parameter values)

## Q20: Interaction Strength Selection
| Context | Strength |
|---------|----------|
| A. General UI | 2-way (Pairwise) |
| B. Medical device | 4–6 way |
| C. Financial system | 3-way |

## Q21: Combinatorial Testing Limitations
1. Still needs good partitioning (EP/BVA) first  
2. Timing/sequence issues not covered  
3. Masking can hide faults; tool-generated tests need oracles  

## Q22: Technique Matching
| Scenario | Technique |
|----------|-----------|
| A. Numeric range 1–100 | BVA (Boundary Value Analysis) |
| B. 20 configuration options | Pairwise/Combinatorial |
| C. ATM with multiple conditions | Decision Tables |
| D. User types (admin, manager, user, guest) | Equivalence Partitioning |

## Q23: Integration Order
1. Equivalence partitioning  
2. Boundary value analysis  
3. Decision tables (if logic is complex)  
4. Pairwise/combinatorial (if many parameters)

## Q24: EP and BVA Relationship
EP groups inputs into classes; BVA adds tests at boundaries within those classes. Example: EP for age 18–65; BVA adds tests at 17, 18, 65, 66. BVA complements EP, not replaces it.

## Q25: Decision Table (Login)
a) 8 rules (2^3) for Username valid, Password valid, Account active  
b) Consolidate with don't-cares where appropriate  
c) Checksum: sum of “covers” must equal 8  

## Q26: Pairwise for Medical Device
Risky. NIST shows ~90% of faults are 1–2 way, but 10% need higher interaction strength. For safety-critical systems, 4–6 way is recommended; pairwise alone may miss important interactions.

---

# Part 3: Random Testing (L06)

## Q1: What Makes Random Testing "Random" (Hamlet 1984)
1. **Defined input distribution** (e.g., operational profile or uniform)  
2. **Statistical independence** of test selections  
3. **Oracle** to decide pass/fail  

## Q2: Random vs Partition Testing
Random is weaker when: domain structure matters, failure regions are small and localized, or we need systematic coverage of known equivalence classes or boundaries.

## Q3: Statistical Confidence
$$C = 1 - (1-F)^N$$
Example: N=10,000, F=10⁻⁵:
$$C = 1 - (1 - 0.00001)^{10000} \approx 1 - 0.905 \approx 9.5\%$$ “No failures” gives a confidence bound, not proof of zero defects.

## Q4: Reliability Calculation
$$N = \frac{\ln(1-C)}{\ln(1-F)}$$
For C = 0.95, F = 10⁻⁴ = 0.0001:
$$N = \frac{\ln(0.05)}{\ln(0.9999)} = \frac{-2.996}{-0.000100005} \approx \mathbf{29{,}956} \text{ tests}$$

## Q5: Randoop Plateau Effect
Error-finding rate drops from ~5/hour to near zero after ~12 hours. Causes: easy bugs found first; remaining bugs need rare input combinations.

## Q6: Hamlet’s “Only Random Testing Will Do”
1. **Large or unstructured input space** — no tractable partitions  
2. **Reliability certification** — probabilistic guarantees from random testing  

## Q7: Oracle and Effectiveness
Oracle limits what can be found: crash detection (low overhead), sanitizers (medium), properties (medium), differential (higher). Stronger oracles allow more effective random testing.

## Q8: Fuzz vs Random Testing
Fuzzing: malformed/unexpected inputs, focus on security/crashes, oracles like crashes/sanitizers. Choose fuzzing for security, robustness, or crash-oriented testing; general random testing for broader functional behavior when oracles exist.

## Q9: Three Generations of Fuzzing
- **Blackbox:** Random bytes, no program feedback (e.g., Miller’s `cat /dev/urandom | prog`)  
- **Whitebox:** Symbolic execution and constraint solving (e.g., SAGE)  
- **Greybox:** Coverage feedback + evolutionary mutation (e.g., AFL, libFuzzer). Greybox “won” due to good throughput/insight ratio.  

## Q10: Miller’s Persistent Bug Classes
Same bug classes (crashes, hangs) persisted 1990–2006 (e.g., ~25–33% UNIX, ~21% Windows NT, ~73% macOS GUI). Shows many systems still have basic robustness problems.

## Q11: Directed Greybox Fuzzing
Directed greybox fuzzing steers inputs toward a target (e.g., Heartbleed bug site). AFLGo uses distance to target. Symbolic execution is slower; directed fuzzing finds Heartbleed in ~20 minutes vs 24+ hours for symbolic execution.

## Q12: Crash Count vs Bug Count (Klees 2018)
57,142 “unique” crashes corresponded to **9** actual bugs — many crashes are duplicates. Implications: use clustering/deduplication and clear bug definitions when evaluating fuzzers.

## Q13: Multiple Fuzzers
Different fuzzers stress different behaviors (grammars, coverage metrics, heuristics). Combining them increases diversity and finds ~50% more bugs than any single tool.

## Q14: QuickCheck Bug Distribution
Bugs were roughly equally in implementations, specifications, and generators. Shows PBT exposes spec and generator bugs, not only implementation bugs.

## Q15: Hypothesis Byte-Stream
One representation for all types; shrinking is generic. Avoids custom shrinkers per type and simplifies PBT implementation.

## Q16: JQF Improvement
JQF (Zest) adds **coverage-guided** generation to PBT. ~**1,000×** improvement over plain random PBT by driving exploration toward new code paths (e.g., Trie bug in 5K vs 7M+ executions).

## Q17: PBT Property Challenge
Specifying correct, useful properties is hard. Many practitioners don’t know what invariants to test; differential and round-trip properties help.

## Q18: PBT vs Fuzzing Time Budgets
PBT: short runs (50ms–30s), many executions. Fuzzing: long campaigns (hours/days). PBT fits unit/CI; fuzzing fits dedicated security campaigns.

## Q19: Coupling Effect
Simple mutations (e.g., single operator change) are coupled with more complex ones: tests that kill all simple mutants typically kill most complex ones. Justifies focusing on simple mutations.

## Q20: Equivalent Mutant Problem
Equivalent mutants behave like the original (undecidable to detect automatically). They inflate the mutant set and depress the mutation score. 10–40% of mutants can be equivalent.

## Q21: Small vs Large LLMs for Mutant Detection
UniXCoder (110M) outperforms GPT-4 (55.90% vs 86.58% F1) because it is fine-tuned on code and mutant structures. General-purpose LLMs lack that specialization.

## Q22: Crossfire Phenomenon
One test can kill many mutants. New tests should target surviving mutants, not add more “crossfire” tests.

## Q23: Mutation Score Target
100% is often unreasonable (equivalent mutants, infeasible paths). **85%** is a practical target; higher returns diminish and cost grows.

## Q24: Mutation vs PBT
Mutation: evaluates test suite quality via fault detection. PBT: generates inputs and checks properties. Complementary: PBT creates tests; mutation evaluates them.

## Q25: Branch Coverage and Mutation
Neither subsumes the other. Branch coverage measures path exercise; mutation measures fault detection. High branch coverage with weak assertions can yield low mutation score.

## Q26: Random vs Partition
Neither is universally better. Partition excels with structured domains and known failure regions; random excels with large/unstructured spaces and when reliability bounds are needed. Ntafos: ~20% more random tests can erase partition’s advantage.

## Q27: Fuzz Testing Definition
Fuzzing feeds malformed/unexpected input to find security defects, crashes, or hangs. Differs from general random testing in input style (malformed), focus (security/robustness), and oracles (crash/sanitizers).

## Q28: Oracle Problem
Without an oracle we cannot decide correctness. For random testing, generation is cheap; oracle automation is the main bottleneck.

## Q29: Oracle Evolution
- Random: explicit reference/gold oracle  
- Fuzz: crash/sanitizer oracles  
- PBT: property oracles  
- Mutation: existing test suite as oracle  

## Q30: Single Technique Selection
Depends on project: security → fuzzing; spec clarity → PBT; test quality assessment → mutation; reliability certification → random with probabilistic guarantees.

## Q31: Bug Classes vs Tool Progress
Same bug classes lasted 16 years (industry adoption lag). Meanwhile, LLMs improve equivalent-mutant detection. Suggests tools improve faster than product robustness in many domains.

## Q32: JSON Parser Strategy (Practical)
- Random: uniform sampling of JSON structures  
- Fuzz: malformed/corrupt inputs (AFL, libFuzzer)  
- PBT: round-trip (parse→serialize→parse), structural invariants  
- Mutation: assess test suite quality  

## Q33: JQF Significance
JQF combines PBT generators with coverage-guided fuzzing, giving structure (PBT) and exploration (fuzzing). Resolves PBT’s blind exploration and fuzzing’s weak structure for complex inputs.

## Q34: Pesticide Paradox
Repeated similar tests stop finding new bugs. Mitigation: diversify techniques (random, fuzz, PBT, mutation), vary inputs and oracles.

---

# Part 4: Exploratory Testing & OP (L07)

## Q1: ET vs OP Fundamental Difference
**ET:** Qualitative, human-driven, simultaneous learning/design/execution.  
**OP:** Quantitative, usage-driven, tests allocated by operational probabilities.

## Q2: Scripted + Exploratory = Coverage
Scripted tests give structured coverage and regression; ET finds unexpected/edge-case defects. Together they cover both planned and unplanned scenarios.

## Q3: ET vs Ad-Hoc
ET uses charters, heuristics, sessions, and debriefing. Ad-hoc lacks structure, documentation, and accountability.

## Q4: Coupon Example
Tester with charter on coupon pricing found: double coupon, negative price, subtotal < 0, dual coupons. Scripted tests did not anticipate these scenarios; ET’s real-time exploration did.

## Q5: Charter Definition
A charter defines scope and goal. Template: **Explore** [target] **using** [resources] **to discover** [information].

## Q6: Hendrickson’s Heuristics (3 examples)
1. **None, Some, All** — empty, partial, full sets (e.g., permissions)  
2. **Too Big, Too Small, Just Right** — size extremes (e.g., file uploads)  
3. **Beginning, Middle, End** — position (e.g., edit at start vs end of line)  

## Q7: Session-Based Test Management
Structured ET with: **Charter, Time Box** (60–120 min), **Reviewable Result**, **Debriefing**. Improves accountability and repeatability.

## Q8: Whittaker’s Five Districts
- **Business:** Core features (Guidebook, Money tours)  
- **Historical:** Legacy features (Bad Neighborhood, Museum)  
- **Entertainment:** Unusual inputs (Obsessive-Compulsive, Antisocial)  
- **Tourist:** First-time use (Collector’s, Supermodel)  
- **Hotel:** Background (All-Nighter, TOGOF)  

## Q9: Five Levels of Exploration
1. **Freestyle:** Only the system  
2. **High:** Charter with goals  
3. **Medium:** Charter + starting points  
4. **Low:** Detailed activities  
5. **Fully scripted:** Steps + expected results  

## Q10: ET Effectiveness Evidence
- Similar defect counts to scripted; ET often **4–6×** more efficient (effort)  
- ~380% more usability defects; ~2× fewer false positives  
- Equal time: ET finds ~4.6× more defects  
- ~88% industry adoption  

## Q11: Defending ET to Management
ET is structured (charters, SBTM, heuristics) and supported by studies showing comparable or higher defect counts with less effort. Not ad-hoc; it has process and documentation.

## Q12: ET Coverage Paradox
ET achieves lower structural coverage but similar defect counts because it targets high-risk areas, human intuition, and unexpected interactions, not just code paths.

## Q13: Operational Profile
Set of operations with occurrence probabilities. Example: Add call 50%, Query 20%, Edit 15%, Remove 15%; sum = 1.0.

## Q14: Function vs Operation vs Run
- **Function:** User/requirements view  
- **Operation:** Design/development view  
- **Run:** Single execution of an operation  

## Q15: Operational Modes (3 examples)
- **Time:** Peak, Prime, Off  
- **User type:** Customer, Admin, System  
- **Capability:** Full, Degraded, Maintenance  

## Q16: Profile Probabilities Sum to 1.0
Profiles model usage; probabilities must sum to 1.0. Otherwise allocation is inconsistent and usage model is invalid.

## Q17: 6-Step OP Procedure (University Enrollment)
1. Operational modes (e.g., enrollment, add/drop, advising)  
2. Initiators (student, admin, system)  
3. Representation (tabular or graphical)  
4. List operations (enroll, drop, view schedule, etc.)  
5. Occurrence rates  
6. Probabilities = rate / total rate  

## Q18: Tabular vs Graphical
- **Tabular:** Many operations, precise values  
- **Graphical:** Hierarchical, for presentation and overview  

## Q19: OP Calculation
$$P(\text{op}) = \frac{\text{Rate(op)}}{\text{Total Rate}}$$

Total = 4,000 + 2,500 + 3,000 + 500 = **10,000**

| Endpoint | Rate | P(op) |
|----------|------|-------|
| GET /users | 4,000 | 4,000/10,000 = **0.40** |
| POST /orders | 2,500 | 2,500/10,000 = **0.25** |
| GET /products | 3,000 | 3,000/10,000 = **0.30** |
| PUT /users | 500 | 500/10,000 = **0.05** |
| **Sum** | 10,000 | **1.00** ✓ |  

## Q20: AT&T and HP Results
- **AT&T:** ~10× fewer customer problems; test cycle ~halved  
- **HP:** ≥50% test time and cost reduction  

## Q21: Operational Coverage
$$\text{OpCov} = \sum_i \frac{\text{covered}_i}{\text{total}_i} \times \text{usage}_i$$

Example:
| Method | Covered/Total | Usage | Contribution |
|--------|---------------|-------|--------------|
| login() | 3/4 | 0.50 | 0.75×0.50 = 0.375 |
| search() | 2/6 | 0.30 | 0.333×0.30 = 0.100 |
| checkout() | 4/4 | 0.15 | 1.00×0.15 = 0.150 |
| adminPanel() | 0/6 | 0.05 | 0×0.05 = 0 |
| **Operational** | | | 0.375 + 0.100 + 0.150 + 0 = **62.5%** |
| **Traditional** | (3+2+4+0)/20 = 9/20 | | **45%** |

## Q22: Android Cloud Profiles
Cloud Profiles from telemetry for top apps. ~7.88% of methods on average; no automated tool exceeds ~70% profile coverage; ~30% of user-relevant behavior needs human exploration.

## Q23: Saturation Handoff
OP drives quantitative coverage until saturation (~70%). ET then addresses the remaining, often human-driven 30%, guided by OP priorities.

## Q24: Two-Phase Strategy
**Phase 1:** OP-based tests until saturation (~70%).  
**Phase 2:** ET on high-priority areas; convert findings to scripted tests. OP first because it quantifies what matters most.

## Q25: Startup Decision
Depends on data. With usage data → OP. With little data and need for discovery → ET. ET is cheaper to start; OP needs usage or estimates.

## Q26: Accountability
- **SBTM:** Charter, time box, debriefing, reviewable artifacts  
- **OP:** Probabilities, coverage metrics, allocation by usage  

## Q27: Banking App Strategy
- Build OP from usage (login, transfer, balance, etc.)  
- OP-weighted tests for high-traffic flows  
- ET charters: security, edge cases, failure modes  
- Tours: Money, Security, Error handling  

## Q28: Operational vs Traditional Coverage
Operational coverage weights by usage; traditional treats all code equally. Operational gives a better signal for user-facing reliability.

## Q29: Cloud Profiles Validation
Profiles differ from developer assumptions; Monkey often beats model-based tools. Indicates we cannot assume how users use the system; real usage data is essential.

## Q30: Lecture Summary
ET = learn + design + execute; OP = usage-based allocation. Use OP first for quantitative coverage; add ET for qualitative discovery; combine both for effective testing.
