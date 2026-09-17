# Workflows, Agents, and MCP — what they actually are

## Workflow vs. agent, in my own words

A **workflow** is a system where a developer decides the path ahead of time. You write code (or
a prompt) that calls an LLM one or more times in a fixed order — chain the output of step 1 into
step 2, maybe route to a different prompt based on a condition, maybe run several calls in
parallel — but the *sequence of steps* is fixed before the system ever runs. The LLM is doing the
thinking inside each step, but it never decides what step comes next, whether to skip one, or
whether to go back and redo one. That decision belongs to the code around it.

An **agent** is a system where the LLM itself decides what happens next, in a loop, using tools
and feedback from its own actions to figure out the next move. Nobody wrote down in advance "call
tool A, then tool B, then stop" — the model looks at the current state of the task, picks a tool,
sees what comes back, and decides again, until it judges the task done (or hits a limit). The
control flow lives inside the model's own reasoning at runtime, not in code written beforehand.

The practical difference isn't "how smart is the LLM inside it" — it's **who is holding the
steering wheel**. In a workflow, the developer is. In an agent, the model is.

## Classifying FL-04 (the Weekly Search-AI Brief pipeline)

My FL-04 pipeline is a **workflow**, specifically the "prompt chaining" pattern: gather →
synthesize → draft → review → format, run in a fixed order every time, where each step is only
allowed to see the previous step's output. I wrote that sequence into the Claude Project's
instructions myself, and it never changes based on what the model finds — even when Step 1 turns
up only two usable sources, the instructions tell it to *stop and say so*, not to decide on its
own to search again with a different query, widen the topic, or push forward anyway. That's the
tell: the pipeline has a rule for "not enough sources," but the *model* isn't the one deciding
what to do about it — the prompt already decided, in advance, that stopping is the only allowed
response. A true agent version would let the model make that call itself.

## What MCP is

MCP (Model Context Protocol) is a standard way for an AI application to connect to external
tools and data, instead of every AI app and every tool needing a custom one-off integration.
Before MCP, wiring an AI app to your files, a database, and a browser meant writing three
separate, app-specific integrations. MCP defines one protocol any "server" (a file reader, a
database connector, a browser controller) can speak, and any "client" (the AI app) can use —
write the integration once, and it works everywhere MCP is supported, the way USB-C lets one
cable work across devices instead of every device needing its own plug.

MCP servers can expose three kinds of things:

- **Tools** — functions the model can actively call to *do* something, usually with a real-world
  side effect or a live lookup: read a terminal, click a button, run a search. This is the one I
  actually used below.
- **Resources** — data a client can attach as context, more like a file the application chooses
  to hand the model rather than something the model reaches out and calls mid-conversation.
- **Prompts** — reusable, server-defined prompt templates a user can invoke on purpose (closer to
  a slash command than something the model decides to use on its own).

## Evidence: one MCP client, three tasks chat alone couldn't do

I ran this from inside Claude Code (the MCP client), using two connected MCP servers — a browser
controller and a local-terminal reader. Full detail is in `evidence/mcp-tool-call-log.md`; in
short: (1) fetched and read the live, currently-published FlyRank Week 5 page — content no chat
model could have from training data alone; (2) read the actual contents of a PowerShell terminal
running on this machine right now — no chat interface has that access without a local
connection; (3) pulled the real network requests (URLs, status codes) the browser made loading
that page — data that doesn't exist until a real browser renders a real page. All three produced
real tool-call results visible in the transcript, not generated-sounding text.

## What FL-04 would need to become an agent

The concrete upgrade: **give the model the search tool directly, inside the loop, instead of
handing it a pre-fetched source list, and let it decide when it has "enough."** Right now Step 1
runs one fixed search and hands a static list to Step 2. An agent version would let the model
run a search, judge the quality/coverage of what came back, decide whether to search again with
a refined query, a different angle, or stop — the way I manually decided to run a follow-up
search if the first pass looked thin. That single change — search-as-a-tool-in-a-loop instead of
search-as-a-fixed-first-step — is what would actually move this from a workflow to an agent,
because it's the first point where the model, not my prompt, would be deciding what to do next.
