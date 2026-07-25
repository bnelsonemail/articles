# Recommended Article Sequence

1. Next week: A Worked Monte Carlo Example for Infrastructure
  * Keep it relatively simple.
  * Define an engineering problem.
  * Identify the uncertain variable(s).
  * Choose and explain the distributions.
  * Run the simulation.
  * Interpret the result as an engineer, not merely as a statistician.
  * Most importantly, show why MC tells us something a single deterministic calculation doesn't.
2. Then: The Design Storm Isn't a Constant
  * Introduce changing hazard distributions and nonstationarity.
  * This builds directly on the discussion you responded to today.
3. Then: Infrastructure Capacity Isn't Constant Either
  * Introduce the other half of the problem.
  * Aging, settlement, deterioration, corrosion, erosion, changing operating conditions, etc.
4. Then: When Changing Loads Meet Aging Infrastructure
  * Bring the two distributions together:
$$
P_f(t) = P[L(t) > C(t)]
$$
  * This is where your MC knowledge starts evolving naturally into reliability analysis.
5. Later: From Probability of Failure to Risk
  * Add consequence.
  * Move toward risk-based asset management and prioritization.
