# Cost Query Pro: From Personal Project to Internal Collaboration

When I began building **Cost Query Pro (CQP)** in July 2025, it was an experiment built around a problem I had been thinking about for several months:

**Engineering firms have years, sometimes decades, of historical construction cost data. How can we make that information easier for engineers and estimators to actually use?**

What started as a personal software project has now reached a significant milestone.

CQP is beginning to move beyond something I am building independently. I am now collaborating with an AI specialist within my organization who has reviewed the project, cloned the repository, and begun working from a separate development branch.

More importantly, conversations have started internally about where CQP could fit within the organization and how the concept might be developed further.

Nothing about enterprise software moves overnight, nor should it. But this represents an important transition for the project:

**CQP is moving from a portfolio project exploring an engineering problem toward a collaborative effort evaluating a real business application.**

## The Problem CQP Is Trying to Solve

Historical construction cost information is incredibly valuable.

Bid tabulations, engineer's estimates, contractor pricing, spreadsheets, and project records collectively tell us what infrastructure has actually cost to build.

But having that information and being able to use it effectively are very different things.

A typical question might be:

> *What have we historically paid for 8-inch PVC water main?*

Answering that sounds straightforward until you start looking at the source data.

One project might describe the item as:

**8" PVC WM**

Another:

**8-IN PVC WATER MAIN**

Another:

**8 inch PVC watermain**

And another:

**8" C900 PVC**

The units might be represented as any of the following:
- LF
- lf
- Lin. Ft.
- LIN FT
- linear feet

The project number might not even be part of the table. In many bid tabulations it appears in a page header or footer, meaning a conventional row-by-row parser may never see one of the most important pieces of metadata in the document.

That particular issue has become one of the more interesting challenges in CQP's ingestion architecture. The current pipeline operates primarily on normalized rows, while real engineering documents often contain important information at the document or page level. Solving that correctly requires carrying document context such as project number, location, year, and source page into the structured data produced by the parser.

This is why I increasingly think of CQP as more than a search application.

**The difficult problem is building trustworthy engineering data from information that was never created for analytics in the first place.**

## Working With Messy Engineering Data

One of the architectural decisions I'm happiest with is treating imperfect source data as normal rather than exceptional.

Engineering records are messy.

Merged cells happen. Notes appear in numeric columns. Headers change between agencies. Units aren't standardized. Duplicate records appear. Some rows are incomplete while hundreds of neighboring rows are perfectly usable.

An all-or-nothing ingestion process handles this poorly.

If a spreadsheet contains 500 records and three are malformed, rejecting all 500 doesn't improve data quality. It merely prevents 497 valid records from being used.

CQP therefore treats ingestion as a **partial-success process**.

Rows are validated independently. Valid records can be loaded while failures are isolated and recorded as data-quality issues. Re-uploading corrected information is designed to be safe through deduplication, and records retain lineage back to their source upload.

That may not be the glamorous part of an AI application, but increasingly I think it's one of the most important parts.

AI can't compensate for an unreliable data foundation.

## The LLM Shouldn't Be the Calculator

CQP also forced me to think carefully about what role an LLM should actually play in an engineering application.

The architectural principle I've settled on is:

**The LLM translates and narrates. The application computes.**

CQP uses natural language because engineers shouldn't necessarily have to learn a specialized query language just to retrieve historical cost information.

But interpreting a question and calculating an answer are different responsibilities.

The current architecture uses the LLM to interpret a user's question into structured search parameters. Application code then performs the database query and statistical calculations. A separate response stage can turn those calculated results into a natural-language answer.

The LLM never directly queries the database, and database records never enter the LLM prompt. The current request path consists of two LLM calls separated from the database and deterministic analytics stages.

That distinction matters.

If an engineer asks for historical unit costs, a number that merely *sounds plausible* isn't acceptable.

The arithmetic needs to come from the underlying records.

## Treating the LLM as an Untrusted Service

That principle also shaped the security model.

Historical bid pricing can contain competitively sensitive information. Project numbers, contractor information, individual unit prices, and source records don't need to be sent to an external language model simply because AI is part of the user experience.

CQP therefore treats the LLM as an **untrusted external service in both directions**.

Its structured output is validated before the application acts on it, and the information sent outward is deliberately constrained. The LLM receives the user's question, limited search-scope information, and aggregate statistics rather than raw database records.

This isn't merely a security feature.

It's an architectural boundary.

It means the generative component can assist with language while the application retains responsibility for data access, calculations, and business logic.

## What the Architecture Review Found

Before beginning this collaboration, I wanted a much more critical assessment of the project than *"the code looks good."*

The architecture was reviewed specifically around system boundaries, data flow, security, provenance, extensibility, integration opportunities, and the division of responsibility between deterministic code and generative AI.

The review confirmed several decisions that have held up well.

The separation between deterministic computation and generative output is real and enforced in the current code. The LLM provider abstraction is isolated. CSV and Excel ingestion with lineage is one of the project's most mature areas. Authentication, provider failover, cost tracking, and the secure two-call query pipeline are implemented.

But the review also identified weaknesses, which is arguably more valuable.

One is particularly important.

Although the **calculation** is deterministic, the current LLM still helps determine which records are selected by interpreting the search keyword.

That means saying "the system is deterministic" without qualification would overstate what the architecture currently guarantees.

The arithmetic is deterministic.

**Retrieval is not yet fully deterministic or reproducible.**

That's exactly the sort of distinction I want these reviews to uncover before an application ever approaches production.

## Why Semantic Retrieval Is Becoming Important

The retrieval problem also connects directly back to messy engineering terminology.

Today's search implementation is primarily lexical.

That creates an obvious problem:

**"8-inch PVC water main"**

doesn't necessarily match:

**8" PVC WM**

even though an engineer immediately recognizes the relationship.

The architecture review identified semantic retrieval as one of the highest-value extensions available to CQP. Importantly, the existing architecture provides a clean boundary where the search implementation can eventually be replaced or augmented without rewriting the analytics, security, or response pipeline.

A hybrid approach is particularly interesting: semantic similarity for identifying comparable descriptions combined with deterministic structured filters for things such as location, year, unit, and price.

That gets much closer to the way an experienced engineer actually searches historical information.

## Traceability Still Needs to Get Better

Another important lesson from the review concerns provenance.

CQP currently returns the scope associated with a query so that the user can understand what was searched.

That's useful, but it isn't enough.

An estimator ultimately needs to be able to ask:

**Which projects produced this number?**

The current architecture provides scope-level provenance but not complete record-level provenance in the user response. The underlying information exists, but it needs to be exposed appropriately to the authenticated user without crossing the LLM security boundary.

That's now one of the areas I consider important to address.

A defensible cost estimate shouldn't end with:

*"The system says the median is $X."*

It should allow the engineer to trace that result back to the historical projects and records that support it.

## There Is Still Plenty to Build

CQP is not finished, and I don't want project updates to pretend otherwise.

CSV and Excel ingestion are implemented. PDF ingestion is not.

PDF is particularly important because historical bid tabs and estimates frequently exist in that format. But PDF extraction introduces layout-dependent problems, including the header/footer metadata issue that originally helped motivate the ingestion design.

Other areas still under consideration include stronger semantic retrieval, improved record-level provenance, query reproducibility, additional statistics, regional comparisons, additional cost sources, cost escalation, forecasting, enterprise authentication, and eventually an analytical warehouse architecture.

Some of those extensions fit naturally into the existing architecture. Others, particularly forecasting and ML, require considerably more foundational work and shouldn't be treated as simple feature additions.

That's part of building this responsibly: distinguishing what exists today from what is merely possible tomorrow.

## A New Stage for Cost Query Pro

The most significant development right now isn't another endpoint or feature.

It's collaboration.

For the first time since I began developing CQP in July 2025, another engineer is actively working from the repository and evaluating the architecture alongside me.

That changes the project.

Ideas that made sense while developing independently now have another engineer challenging them. Architectural decisions have to survive scrutiny. Integration questions matter. Security and data governance become much more concrete when you're thinking about an application operating inside an actual organization rather than on a development machine.

And discussions are beginning about how CQP might fit with other internal efforts around historical construction cost information.

One particularly interesting conclusion from the architecture review is that successful integration may not necessarily mean combining applications or sharing large amounts of code.

A common cost-record schema and common project identity model could potentially be more valuable than tightly coupling two systems. The review specifically identified agreement around project and item data structures as one of the highest-value forms of alignment between complementary applications.

That's the kind of architectural discussion I'm looking forward to having.

## From an Idea to Something More

I started thinking about this problem in early 2025.

I began building Cost Query Pro in July 2025.

At the time, I didn't know whether it would become anything beyond a way for me to explore the intersection of civil engineering, software development, data engineering, and applied AI.

Now another engineer is contributing to it, conversations about real organizational use have begun, and the project is entering a stage I couldn't realistically simulate while building it alone.

There is a great deal of work between that and a production system.

But this is still a milestone worth recognizing.

The original idea remains remarkably simple:

**Engineering firms already possess tremendous amounts of institutional knowledge in their historical project data.**

The hard part is extracting it, normalizing it, understanding it, protecting it, tracing it, and ultimately making it accessible enough that an engineer can use it when making a decision.

That's the problem I've been trying to solve with Cost Query Pro.

And now, for the first time, it's becoming a problem I'm not solving alone.

> **Engineering begins with calculations.**  
> **Infrastructure analytics powers better decisions.**
