# Just the Yes

**Volunteer matching on Solid where an organisation gets your yes, not your profile.**

Status: design proposal, September 2026. Nothing on Solid is built yet. This repository holds the design, a browser demo, example data and the evidence behind it. It is part of an application to the ODI's Solid Open Call (Start tier).

**Try the demo:** [demo/index.html](demo/index.html) (live at [ai-proof.github.io/just-the-yes/demo](https://ai-proof.github.io/just-the-yes/demo/)). It runs the whole flow on 376 real London roles from the Volunteering Data Standard API. The Pod, inbox and access control are simulated in the browser tab.

## The problem

The first step into volunteering is usually a form. In a small sample of eight public application forms from UK councils and charities ([the list is here](docs/baseline-forms.md)):

- six ask about criminal convictions;
- seven want two referees' names and contact details;
- most ask about health or disability.

All of this comes before anyone knows whether the role fits, or whether the organisation will reply. Some roles do need these checks, but later: one council already asks about convictions only after shortlisting. Today the checks go to every organisation a person contacts, and small organisations then hold personal data they may never use.

## How it works, in three steps

1. **Check fit privately.** Your details (skills, availability, how far you can travel, access needs) stay in your own Solid Pod. Your app downloads open role data and compares it with your details on your own device. Nothing from your profile is sent while you look.
2. **Send your yes.** Pick a role, and your app writes a small "yes" in your Pod holding only what the role needs for a first reply. You see and approve it, then the app posts a short message to the organisation's inbox that links to it. Each role shows how many more yeses it can answer on time, so its reply promise can be kept. The pilot also tests a small monthly allowance of yeses per person, and drops it if it puts people off.
3. **Get a reply.** Every role shows a reply promise: a named contact and a reply-by date. When the organisation answers, your app removes its access to what you shared. Checks the role really needs, such as references or a background check, happen after both sides want to go ahead.

## Why Solid

- The data about you stays with you, in your Pod, instead of being copied into each organisation's database.
- WebIDs and inboxes (Linked Data Notifications) carry the yes and the reply.
- Access control lets one named coordinator read the yes, and the app removes that access after the reply. Servers that support expiring access grants can enforce the time limit themselves.
- The role data already exists. Volunteering platforms publish it with the ODI's [Volunteering Data Standard](https://standard.volunteeringdata.io/), which is RDF, and a [public API](https://api.volunteeringdata.io/swagger) serves it. On 23 September 2026 the API reported 5,000 activities from 503 organisations.
- In the pilot, only roles from pilot organisations (published with a WebID and an inbox) offer a yes. Other roles link to the organisation's usual way to apply.

## Where it fits the Volunteering Data Standard

The standard's own [use-case list](https://standard.volunteeringdata.io/use-cases) includes "a data standard to describe a volunteer" (1.2) and "a standard to match volunteers to opportunities" (1.3). Just the Yes covers both, with one change: the description of the volunteer is held by the volunteer, in their Pod, and only a yes crosses to the organisation. It also touches use case 4 (checks and references), by moving them after both sides say yes.

**A gap the demo exposed.** On 24 September 2026 the API's location search returned 614 activities within 8 km of central London. The query asks for skills, requirements, session times and remote participation, but none of the 614 had any of these filled in: only title, description, organisation, location and, for 238 of them, an apply link. So today fit can only be checked from distance and keywords. (The demo's interest areas and "online" option are guessed from each listing's text.) The project would propose a few person-side and role-side fields to the standard's working group.

## What it is not

It is not a new volunteering platform, and it does not rank people. Nobody computes a score about you for anyone else. It is a pattern, plus open-source parts, that existing platforms, councils and charities could adopt.

## What the pilot will measure

- Which fields each pilot organisation agrees to leave out of first contact, compared with its current form.
- The share of yeses answered by the promised date.
- The share of yeses that lead to a first conversation.
- Whether volunteers can go from search to a sent yes, unaided, within 15 minutes.

## Where the idea comes from

Just the Yes tests one rule from the General Matchmaking Protocol, a longer design I wrote for matching people with organisations. In that design the person holds their own profile, and the organisation receives only a deliberate action, never a score. The same rule could later apply to other first contacts, such as job or housing applications. A two-page summary is in [docs/background/](docs/background/).

## Files

- [ARCHITECTURE.md](ARCHITECTURE.md): the flow, the Solid building blocks, threats and open questions.
- [examples/](examples/): example data in Turtle (a role, a private profile, a yes, the notification, a reply, an access rule). All of it is synthetic.
- [docs/baseline-forms.md](docs/baseline-forms.md): the eight forms, what each asks, and how I counted.
- [docs/background/](docs/background/): background written for job markets, where the idea started: a two-page summary of the General Matchmaking Protocol, and a two-page note with a small simulation on how many priority applications a market can honour. Not part of the volunteering proof of concept.
- [demo/](demo/): the browser demo, a single self-contained page. The role snapshot it uses (376 roles, pulled from the Volunteering Data Standard API on 24 September 2026; the dataset's metadata gives its licence as CC BY 4.0) is embedded in the page.

## How this was made

I designed Just the Yes and decide what goes in it. An AI assistant (Claude, by Anthropic) did much of the building under my direction: the demo code, the pull from the Volunteering Data Standard API, the first count of the eight forms, and the simulation in the background note. I review and correct what it produces. AI-generated code in future work will be marked as such in its commits.

## Who

Daniel Bulla, independent systems architect, Bratislava, Slovakia.

Code is released under the MIT licence. Text and example data are released under CC BY 4.0.
