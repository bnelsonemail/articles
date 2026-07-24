# Monte Carlo Simulation: A Tool More Engineers Should Know About

I spent more than two decades working in engineering before I really encountered Monte Carlo simulation.

It wasn't something I remember learning in engineering school, and it wasn't a tool I regularly encountered while designing water and wastewater infrastructure.

I discovered it while expanding my knowledge of data analytics and statistics.

And once I understood what it was, my first thought was:

**Why don't more engineers know about this?**

Despite the somewhat unusual name, Monte Carlo simulation isn't an exotic vacation! Joking aside, it is not an AI technique or some new development in analytics. It's a well-established numerical method for analyzing uncertainty.

The basic idea is surprisingly simple.

In engineering, we often perform calculations using a set of assumed inputs.

A design flow might be 4.0 MGD.

A pump might have an expected service life of 25 years.

A water main might have an assumed useful life of 75 years.

Those values are useful, and sometimes necessary, for performing calculations and making decisions.

But the real world rarely gives us perfectly fixed numbers.

Future demand may be higher or lower than projected. Equipment performance changes over time. Assets deteriorate at different rates. Soil conditions, installation practices, operating pressures, material, age, and previous failures can all influence how infrastructure performs.

Traditional engineering calculations often ask:

**What happens if these assumptions are correct?**

Monte Carlo simulation allows us to ask a slightly different question:

**What range of outcomes could occur given the uncertainty in those assumptions?**

## Consider the Infrastructure Beneath Our Cities

Think about the miles of water mains, force mains, gravity sewers, and other buried infrastructure operated by a municipal utility.

Some of those assets may have been installed decades ago.

They are aging.

Eventually, many of them will need to be rehabilitated or replaced.

But utilities don't have unlimited capital.

If a utility has hundreds or thousands of miles of aging pipe and enough funding to replace only a small percentage each year, the real question isn't simply:

**Which pipes are old?**

The more important question is:

**Which pipes should we replace first?**

Age alone can't necessarily answer that.

Two water mains installed in the same year may have very different risk profiles.

One might have experienced several failures. Another may have never failed.

One may run beneath a residential street where a failure would be inconvenient but manageable. Another may serve a hospital, cross beneath an interstate, or provide critical transmission capacity to a large portion of the system.

Material, soil conditions, operating pressure, break history, diameter, critical customers, redundancy, repair cost, and consequence of failure can all matter.

And many of those factors contain uncertainty.

This is where methods such as Monte Carlo simulation become interesting.

## From One Prediction to Thousands of Possible Outcomes

Instead of assigning a single fixed value to every uncertain variable, Monte Carlo simulation allows those variables to be represented by probability distributions.

A computer then repeatedly samples from those distributions and performs the analysis.

Not once.

Potentially thousands or tens of thousands of times.

Each simulation represents one possible combination of uncertain inputs and the resulting outcome.

For an aging water main, those simulations might incorporate uncertainty associated with deterioration, future demand, failure frequency, repair cost, or other factors affecting the asset.

Instead of producing a simple conclusion such as:

**This pipe has 20 years of remaining service life.**

the analysis might provide something much more useful:

**The simulation estimates a 30% probability that this asset will experience a failure within the next five years.**

Instead of prioritizing replacement based primarily on age, utilities could evaluate the probability and consequences of different outcomes across thousands of assets.

That information could help answer a much more important capital planning question:
Now imagine performing that type of analysis across an entire utility system.


**Where can the next dollar of limited capital investment reduce the most risk?**

## From Replacement Schedules to Risk-Based Decisions

This changes the way we think about capital improvement planning.

A traditional replacement program might prioritize infrastructure based largely on age, condition, or historical failure.

Those are still valuable pieces of information.

But probabilistic analysis allows us to consider something more fundamental:

**What is the risk of leaving this asset in service?**

And risk isn't simply the probability that something will fail.

The consequences matter too.

A relatively high probability of failure on a small, redundant water main may represent less system risk than a lower probability of failure on a major transmission main serving critical customers.

Monte Carlo simulation can help engineers explore those uncertain outcomes and compare possible scenarios.

It doesn't create an unlimited capital budget.

Sadly, numerical methods have yet to solve that particular engineering problem.

But they can help utilities make more informed decisions about where limited capital should be invested.

## Where Could Engineers Use It?

The same concept can be applied to many of the uncertainties engineers deal with every day.

Monte Carlo simulation can help evaluate uncertainty associated with:

* Future water demand
* Construction costs
* Infrastructure deterioration
* Asset service life
* Equipment reliability
* Failure risk
* Energy consumption
* Population growth
* Capital improvement planning

The specific application changes, but the underlying idea remains the same.

Rather than pretending every input is known with certainty, we acknowledge that some variables are uncertain and evaluate how that uncertainty affects the possible outcomes.

## A Different Way of Thinking About Engineering Calculations

For me, this is what makes Monte Carlo simulation particularly interesting.

Engineering calculations traditionally produce an answer.

Monte Carlo simulation produces a **distribution of possible answers**.

That shift changes the kinds of questions we can ask.

Instead of asking only:

**What is the expected outcome?**

We can also ask:

**What range of outcomes should we reasonably expect?**

**How likely are we to exceed a critical threshold?**

**How uncertain are we about our prediction?**

**Which assumptions have the greatest influence on the result?**

And, in the case of infrastructure asset management:

**Where does capital investment provide the greatest reduction in risk?**

Those questions can provide valuable context when evaluating infrastructure investments, reliability, design decisions, and long-term capital planning.

## It Doesn't Replace Engineering Judgment

Monte Carlo simulation doesn't tell an engineer which water main to replace, how much risk is acceptable, or what decision to make.

And a simulation is only as meaningful as the assumptions, data, and probability distributions behind it.

If those assumptions don't reasonably represent the system being analyzed, running the model 100,000 times doesn't magically make the answer correct.

Computers remain remarkably efficient at producing bad answers very quickly when we give them bad assumptions.

The engineer still has to understand the system, evaluate the inputs, consider the consequences, interpret the results, and determine what level of risk is acceptable.

Monte Carlo simulation simply gives us another way to understand the uncertainty surrounding those decisions.

And understanding uncertainty is an important part of engineering judgment.

## Next: Putting It Into Practice

I'm currently working through an applied Monte Carlo simulation using Python to better understand the method beyond the theory.

In an upcoming edition of *Engineering Judgment*, I'll move from the concept to the application and show what a Monte Carlo simulation actually looks like in an engineering problem.

We'll look at how uncertain inputs can be modeled, how thousands of possible outcomes can be simulated, and, most importantly, how those results can help support an engineering decision.

Because the goal isn't to eliminate uncertainty.

It's to understand it well enough to make better decisions.

**Engineering begins with calculations.**
**Infrastructure analytics powers better decisions.**






