# MCP tool-call evidence log

**MCP client used:** Claude Code (this session runs inside it, connected to several MCP servers
at once — the browser-control server and the local-terminal server are the two used below).

**Note on evidence:** the tool calls below happened live in this Claude Code conversation and
are visible in its transcript as actual `tool_use` / `tool_result` blocks (each one names the
server, e.g. `mcp__Claude_Browser__...` or `mcp__terminal__...`, and shows real returned data,
not generated text). Screenshot that portion of the conversation directly for the strongest
proof — a screenshot of the chat transcript itself is more convincing than a second-hand log.
The session also rendered a live screenshot of Task 1's target page inline in the conversation
(the browser pane showing the real, currently-published Week 5 page) — screenshot that moment of
the conversation too as supporting visual evidence; it isn't saved as a separate file here since
the browser tool returns it inline rather than to disk.

## Task 1 — Fetch and read a live external page (server: `Claude_Browser`)

Tools called: `navigate` -> `https://aifluency.flyrank.ai/week-05.html`, then `get_page_text`.

**Why chat alone couldn't do this:** a plain chat model has no live network access — it can only
answer from training data or from text the user pastes in. This page (the Week 5 "Ship the Ugly
Version" assignment brief) didn't exist in any training data; the tool call fetched it live and
returned real current text: title, phase/hour tags, and body copy, confirmed word-for-word
against what's actually published right now.

## Task 2 — Read the local machine's terminal state (server: `terminal`)

Tool called: `read_terminal` (40 lines).

**Why chat alone couldn't do this:** this reads the literal contents of a terminal panel running
on the user's own machine right now — a PowerShell session sitting at
`C:\Users\kara\Desktop\FlyRank\FlyRank_Intern`. No chat interface has access to what's on a
specific person's local screen; this only works because the MCP server has a live connection to
that terminal.

## Task 3 — Inspect live network activity from a real page load (server: `Claude_Browser`)

Tool called: `read_network_requests` (on the page loaded in Task 1).

**Why chat alone couldn't do this:** this lists the actual HTTP requests the browser made while
rendering that page — real asset URLs (`styles.css`, `glossary-data.js`, `announce.js`, etc.)
with real status codes (`200`), captured from a live browser session. A chat model has no
runtime browser to inspect; there's no text prompt that produces a real network log, because the
data doesn't exist until a real page actually loads.
