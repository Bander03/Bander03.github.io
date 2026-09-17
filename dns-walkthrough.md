# DNS Walkthrough — what actually happens when someone opens my site

**In plain words, no networking background assumed.**

## The problem DNS solves

Computers on the internet find each other by number — an IP address, something like
`185.199.108.153`. Nobody wants to type that to visit a website. DNS (Domain Name System) is the
system that lets you type `bander03.github.io` instead, and quietly turns it into the right
number behind the scenes. It's the internet's phone book: you look up a name, you get a number.

## The four things involved

- **A resolver** — usually run by your internet provider or a public service (Google's, at
  `8.8.8.8`, is a common one). This is the "operator" your computer calls first and asks
  "where is `bander03.github.io`?" It doesn't know the answer itself most of the time — its job
  is to go find out and remember the answer for a while (this remembering is called caching, so
  the next person asking gets a faster answer).
- **A nameserver** — the actual authority for a domain. GitHub runs the nameservers responsible
  for knowing where every `*.github.io` site actually lives. When the resolver doesn't already
  know the answer, it eventually asks a nameserver.
- **A record** — the actual entry stored on that nameserver: a small piece of data that maps a
  name to a value. Two kinds matter for a site like mine:
  - **An A record** maps a name directly to an IP address (`bander03.github.io` → `185.199.108.153`).
  - **A CNAME record** maps a name to *another name* instead of a number directly — "this name
    is really just an alias for that other name, go look that one up instead." A CNAME is what
    you'd use if you connected a custom domain later: pointing `mysite.com` at
    `bander03.github.io` with a CNAME means "whatever `bander03.github.io` currently resolves to,
    use that" — so if GitHub ever changes the underlying server IP, your custom domain doesn't
    break, because it's following the name, not a number that could go stale.
- **A response** — the actual answer that travels back: an IP address, handed back through the
  resolver to your computer.

## The full sequence, start to finish

1. You type `bander03.github.io` into your browser and hit enter.
2. Your computer asks its configured **resolver**: "what's the address for this name?"
3. If the resolver already has the answer cached from a recent lookup, it hands it straight back
   — done, no further travel needed. This is the common case and it's fast.
4. If not, the resolver goes and asks the internet's directory system, working its way down to
   the **nameserver** that's actually responsible for `github.io` domains.
5. That nameserver looks up its own **record** for `bander03.github.io` and returns the answer —
   in this case, one of GitHub Pages' IP addresses.
6. The resolver hands that answer back to your computer as the **response**, and caches it for
   next time.
7. Your computer now has an actual IP address, so it opens a direct connection to GitHub's
   servers at that address and requests the page.
8. GitHub's server checks which site that address/hostname combination belongs to, and sends
   back my actual `index.html` and its assets.
9. The padlock (HTTPS) appears because that connection in step 7 isn't plain — it's wrapped in
   TLS encryption using a certificate GitHub automatically issues and manages for `*.github.io`
   domains, so nothing in between (your wifi router, your ISP) can read or tamper with the page
   as it travels to you.

All of that — steps 2 through 9 — typically happens in well under a second, and almost always
happens invisibly before you even finish typing the address if your browser autocompletes it
from history.

## Why this matters for a custom domain later

Right now my site's name (`bander03.github.io`) already *is* the name GitHub's nameservers know
about directly — no extra setup needed, which is why it worked the moment Pages was turned on.
If I later buy my own domain (say `bandersidiq.com`), I would go to *my domain's* registrar (not
GitHub) and add a CNAME record there pointing `bandersidiq.com` (or `www.bandersidiq.com`) at
`bander03.github.io`. That CNAME is the instruction "anyone asking for my custom domain should
really be sent to look up GitHub's name instead" — from that point on, the same resolver →
nameserver → record → response sequence above just runs twice in a row: once for my custom name,
which redirects the lookup to GitHub's name, and once for GitHub's name, which resolves to the
real IP address.
