# The traffic light nobody checked

The product story in first person. The decisions are detailed in [DECISIONS.md](DECISIONS.md), and
the code that rebuilds the logic is in this repository.

## The data already existed

At American Burrs, a manufacturer of dental burs that sells to dental schools, the ERP already
classified each customer by color, based on days since the last purchase. Green, yellow, red,
black, purple. The traffic light was right and nobody checked it. At the same time, reps didn't
like filling in the CRM, and the company was paying for two commercial tools to store data that
arrived incomplete.

When I took on the digital transformation, the obvious reading was adoption: train, enforce, build
a better dashboard. It took me a while to see that the problem was something else. No rep needed
more information. What they lacked was the time to look at the information that was already there.

## The bet behind the account

American Burrs' market strategy was to build loyalty with the dentist from university onward. In
practice, that strategy reaches the sales rep as one question: does this school still buy from us
this term? An account that stays active term after term is how the strategy shows up in the rep's
day.

## What Herbert Simon had already written in 1971

Herbert Simon, who would later win the Nobel Prize in economics, described this problem in a talk
on how to design organizations for an information-rich world. Information consumes the attention of
its recipients, and so a wealth of information creates a poverty of attention.

The counterintuitive part comes right after. For Simon, an information system only reduces the
load on an organization if it absorbs more information than it produces. The goal is not to give
the manager everything they need, but to rearrange the environment so they spend less time
receiving.

The traffic light did the opposite. Each color was one more thing to open, interpret and turn into
action.

## First, understand the buyer's cycle

In discovery, through Lean Inception workshops with the field team, we found that the decision maker
is not the school, it is the professor. Every academic term they build the bur kit for their class.
That gave meaning to the colors: green and yellow cover the current term, red is the window before
the next kit, black is the professor who has already skipped a cycle.

With that, the question changed. It was no longer "how do we get the rep to look at the traffic
light". It became "what does the rep need in hand on the day the account turns red".

## The decision: the system reads, the rep decides

The rep wouldn't go to the data. The data would go to the rep, already read. The traffic light was
synced daily into the CRM. When an account turned red or black, the AI read the ERP history and
delivered four things: the account situation, a next action, the WhatsApp message and the email.
The rep reviewed and sent in one click.

The business rules became product rules. The AI could only cite numbers that existed in the ERP. It
could not offer discounts, because the rep didn't have that authority either. And nothing went out
without someone reading it. I tuned the briefing text with real usage until it sounded like the rep.

The same reasoning applied to building kits. The app pulled price and stock from the ERP and
validated the class rules on its own: minimum units per student, the right mix of bur types, stock
for the whole class and a cost ceiling per student.

## Order mattered more than tools

I validated the hypothesis first on an off-the-shelf CRM, to save time, and built the integrations
from scratch instead of paying for ready-made ones. Only after seeing reps use it did I move the
CRM, pipeline and kit builder into our own low-code application, built and validated together with
the field team and adopted by the sales executives.

The result was over 60% reduction in commercial tool costs at the MVP stage, and 80% at full
rollout. One of the two licenses was dropped first, and the kit builder validated replacing the
other one too, which was the more expensive. The traffic light started to drive the rep's routine,
and manual data entry ended. The north star I defined is repurchase in the following term, which is
not instrumented yet.

## The line I would take to any meeting

Dashboards demand attention. Briefings give it back.

Most data projects for sales teams measure how much data reached the rep. I started designing the
other way around: how much the rep no longer had to read in order to act.

After I left, I rebuilt the logic in this repository, with fictional data, tests and an automated
evaluation of the briefing over 20 accounts. I built it with a coding agent and kept a record of
each of its deviations, like the day it changed a production rule without asking.

## What was not my merit

The most important rule in the briefing was not mine. The company decided that reps don't give
discounts long before there was any AI in the process. The product only treated that decision as a
boundary, and perhaps that is the part that transfers best to other places: before asking what the
AI can do, ask what the business has already decided nobody does.
