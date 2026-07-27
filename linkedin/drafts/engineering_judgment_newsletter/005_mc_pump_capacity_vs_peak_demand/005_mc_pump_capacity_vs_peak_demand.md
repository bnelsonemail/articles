# A Worked Monte Carlo Example for Infrastructure

Last week, I wrote about Monte Carlo simulation and why I believe it's a tool more engineers should know about.

The basic idea is relatively simple: instead of performing a calculation once using a single set of assumed values, Monte Carlo simulation performs the calculation thousands of times while allowing uncertain inputs to vary.

But the value becomes much clearer when we apply it to an engineering problem.

So let's work through a simple water system example.

## The Scenario

Imagine a utility evaluating an existing water system.

Development within the service area has increased demand, and the utility wants to know whether its existing pumping and storage infrastructure still provides adequate capacity during peak conditions.

Through collected data from their SCADA, the system has an estimated peak demand of **4,000 gpm** and approximately **4,500 gpm** of available pumping capacity.

At first glance, the calculation looks reassuring:

**4,500 gpm pumping capacity - 4,000 gpm peak demand = 500 gpm available capacity**

If those were fixed values, our analysis could almost end there.

The pumps can meet peak demand with 500 gpm to spare.

But there's a problem.

**Neither number is really fixed.**

And that is where Monte Carlo simulation becomes useful.

## What Do We Actually Know?

The 4,000 gpm peak demand is an estimate.

Actual peak demand varies. Customer usage changes from day to day. Weather affects consumption. Seasonal patterns matter. Development continues. Even our estimate of the design condition contains uncertainty.

The same is true on the supply side.

We may describe the pumping system as having 4,500 gpm of available capacity, but actual capacity can vary with system pressure, operating conditions, equipment performance, and other factors.

So instead of asking:

> **Can 4,500 gpm meet a demand of 4,000 gpm?**

perhaps the better question is:

> **Given the uncertainty in both values, how often might demand actually exceed available pumping capacity?**

That's a question a single deterministic calculation can't answer.

## Representing the Uncertainty

To use Monte Carlo simulation, we need some way to describe the possible values of our uncertain variables.

For this simplified example, we'll assume both follow normal distributions.

For peak demand:

**Mean = 4,000 gpm**  
**Standard deviation = 400 gpm**

For available pumping capacity:

**Mean = 4,500 gpm**  
**Standard deviation = 300 gpm**

The mean represents the value around which we expect each variable to be centered.

The standard deviation represents how much variability we're allowing around that value.

These values are intentionally simplified for this example. In an actual engineering analysis, selecting the distributions may be one of the most important parts of the entire process.

Historical data can also be evaluated to determine whether a normal distribution is appropriate and to estimate the actual variability in each parameter. If the data doesn't reasonably follow a normal distribution, another distribution may provide a better representation. The distribution should fit the data. We shouldn't make the data fit the distribution simply because a normal distribution is convenient.

**Monte Carlo doesn't remove the need for engineering judgment when selecting our assumptions. It makes the consequences of those assumptions easier to explore.**

## Running the Simulation

Now we can perform the experiment.

For each simulation, we generate one possible peak demand and one possible pumping capacity.

Then we ask a simple question:

**Is pumping capacity less than peak demand?**

If it is, pumping alone would be insufficient for that simulated condition.

Then we repeat the process.

Not ten times.

Not a hundred times.

In this case, **100,000 times**.

The Python required to do this is surprisingly small:

> INSERT CODE HERE

The result:

> **Probability: 15.8%**

The seed is included so that the simulation is reproducible. Someone running the same example can reproduce the same result rather than getting a slightly different random sample each time.  But this article is not a lesson in Python. The code is simply the tool we're using to perform the analysis.

But the code isn't really the interesting part.

The interesting part is what just happened to our original engineering conclusion.

## Our 500 gpm Margin Isn't the Whole Story

Our deterministic calculation gave us:

**4,500 - 4,000 = 500 gpm**

On paper, we have excess pumping capacity.

Nothing about that calculation is wrong.

But Monte Carlo tells us something the calculation doesn't.

When we allow both demand and pumping capacity to vary according to our assumptions, demand exceeds available pumping capacity in approximately **16% of the simulated conditions**.

That doesn't mean the water system fails 16% of the time.

It doesn't mean the pumps are undersized.

And it certainly doesn't mean we immediately recommend replacing them.

It means something much more specific:

> **Under the assumptions of our model, pumping alone may be insufficient to meet demand under roughly 16% of the simulated peak-demand conditions.**

Now we have an engineering question worth investigating.

## What Does 16% Mean to the Engineer?

This is where I think Monte Carlo becomes particularly useful.

A water system isn't necessarily designed for pumping capacity to meet every instantaneous demand condition by itself.

That's one reason we have storage.

If demand temporarily exceeds pumping capacity, elevated storage can make up the difference.

So our 16% result isn't necessarily a problem.

Instead, it changes the next questions we should ask.

* How large are the simulated deficits?
* How long do those conditions persist?
* How much usable storage is available?
* How quickly can the pumping system recover that storage after the peak passes?
* What happens if one pump is unavailable when the high-demand condition occurs?

A 50 gpm deficit and a 1,000 gpm deficit are very different engineering problems.

Storage can handle a short-duration peak much differently than a sustained deficit.

Suddenly we're no longer asking whether **4,500 is greater than 4,000**.

We're thinking about how the system actually behaves.

That's the value of the analysis.

## Why Not Just Use a Conservative Design Value?

Engineers already deal with uncertainty.

We use safety factors, conservative assumptions, redundancy requirements, design criteria, and worst-case conditions all the time.

Monte Carlo doesn't eliminate any of those.

It answers a different question.

A deterministic analysis might ask:

> **Does the system satisfy the selected design condition?**

Monte Carlo allows us to ask:

> **Across a range of plausible conditions, how frequently might our design criterion not be satisfied?**

Those approaches aren't competitors.

They're complementary.

The deterministic calculation gives us a design point.

The probabilistic analysis gives us information about what happens around that point.

## 100,000 Simulations Doesn't Mean 100,000 Times More Accurate

While working through this example, I experimented with simulation sizes ranging from 100 iterations to 10 million.

At relatively low simulation counts, the result moved around noticeably.

In this example, once I reached roughly 1,000 simulations, the whole-number result became relatively stable. Increasing the number of simulations beyond that mostly affected the decimal places.

That doesn't mean 1,000 simulations is universally sufficient. Convergence depends on the problem, particularly when estimating rare events or probabilities near the tails of a distribution.

Eventually, adding millions of additional simulations mostly gave me more decimal places. 

And that's worth discussing.

Suppose one simulation produces:

**15.83%**

Another might produce:

**15.79%**

Reporting those numbers to two decimal places creates an appearance of precision that the underlying engineering assumptions probably don't justify.

We assumed that peak demand has a mean of exactly 4,000 gpm and a standard deviation of exactly 400 gpm.

How certain are we about those numbers?

The simulation cannot be more accurate than the assumptions we put into it.

Running 10 million simulations can reduce **simulation noise**.

It cannot reduce **uncertainty in the underlying engineering assumptions**.

For this example, I'd be much more comfortable telling a decision-maker that pumping capacity may be insufficient under **about 16% of the simulated conditions** than proudly announcing 15.83% as though we've discovered a new physical constant.

## What Did Monte Carlo Actually Give Us?

This is the part I find most useful.

Our original calculation wasn't wrong.

**4,500 gpm is still greater than 4,000 gpm.**

Monte Carlo didn't overturn the engineering calculation.

It gave us another layer of information.

The deterministic analysis told us:

> **At our assumed design point, pumping capacity exceeds peak demand by 500 gpm.**

The Monte Carlo analysis told us:

> **When uncertainty in demand and pumping capacity is considered, that margin doesn't exist under every plausible condition.**

And that leads naturally to better engineering questions about storage, redundancy, operational flexibility, and system reliability.

That's why I don't see Monte Carlo simulation as a replacement for traditional engineering calculations.

I see it as a way to extend them.

Instead of treating every input as though it were known with certainty, we can begin asking what happens when the real world refuses to cooperate with the exact numbers in our spreadsheet.

Because it usually does.

**Engineering begins with calculations.**  
**Infrastructure analytics powers better decisions.**
