# Turning Historical Cost Data into Engineering Intelligence

In early 2025, I started thinking about a problem I kept seeing in engineering consulting:

**We have years of historical construction cost data. But how effectively are we actually using it?**

Bid tabs, engineer's estimates, spreadsheets, and other project records contain valuable information about what infrastructure has actually cost to build.

The problem is that having the data and having **usable data** are two very different things.

Over the following months, that idea developed into the concept for **Cost Query Pro (CQP)**. I began building CQP in July 2025, and I've continued developing and refining it ever since.

The concept sounds simple:

**Let an engineer ask a cost question in plain English and use historical project data to produce a traceable, defensible answer.**

For example:

*"What have we historically paid for 8-inch PVC water main?"*

But the deeper I've gotten into the problem, the more interesting it has become.

Historical engineering data wasn't created for analytics.

A project number may be sitting in the header or footer of a bid tab rather than inside the structured table.

Units that mean exactly the same thing may appear as:

**LF, lf, Lin. Ft., LIN FT, linear feet**

Descriptions aren't standardized either:

**8" PVC WM**
**8-IN PVC WATER MAIN**
**8 inch PVC watermain**
**8" C900 PVC**

To an experienced engineer or estimator, those may obviously describe comparable work.

To a computer, they're different strings.

Then there are capitalization differences, blank cells, inconsistent column names, duplicate records, malformed rows, changing terminology, different spreadsheet layouts, and decades of files that were never intended to become a clean analytical dataset.

That's the problem I've really become interested in solving.

CQP is being designed to ingest historical cost information, normalize and validate it, preserve where the information came from, and make that history searchable through natural language.

I've deliberately kept one architectural principle at the center of it:

**The LLM translates and narrates. The application computes.**

AI can help interpret an engineer's question and deal with some of the ambiguity inherent in engineering language.

But it should not invent the answer.

The actual records are searched by the application, and the statistical calculations are performed deterministically in code. The LLM doesn't get to decide that the average cost of water main is $52.40 because $52.40 happens to look convincing.

That distinction becomes important when a number might eventually influence an engineering estimate or bid.

The same philosophy applies to the data itself.

If 497 rows of a 500-row spreadsheet are valid, I don't necessarily want three malformed rows to make the other 497 useless. I want to ingest what can be trusted, identify what can't, and preserve the data-quality issues so they can be reviewed.

There is still a lot to build.

PDF ingestion presents some particularly interesting problems because important project metadata can live outside the table itself. Semantic retrieval should eventually help recognize that differently written descriptions may represent the same type of work. Stronger record-level provenance will make it easier for an engineer to trace a result all the way back to the projects that produced it.

Eventually, I'd also like to explore escalation, regional comparisons, forecasting, and additional historical cost sources.

But the underlying idea I've been pursuing since early 2025 hasn't changed:

**Engineering firms already possess tremendous amounts of institutional knowledge in their historical project data.**

The challenge isn't simply collecting more data.

It's turning the data we already have into reliable information engineers can actually use to make better decisions.

That's the problem I've been trying to solve with Cost Query Pro.

> **Engineering begins with calculations.**
> **Infrastructure analytics powers better decisions.**
