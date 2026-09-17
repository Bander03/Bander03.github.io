# Make It Do Something — the contact form, explained plainly

**The one feature:** a real contact form on the homepage that sends me an actual email when
someone fills it out — not a fake "coming soon" form, an actual working one.

## What a backend even is

Everything on my site before this — the hero, the case study, the charts — is static: it's just
files (`index.html`, some SVGs) that GitHub hands to your browser exactly as they're saved. Your
browser reads them and draws the page. Nothing "happens" anywhere — there's no server doing work,
just a file being handed over, like a printed flyer.

A backend is the opposite: it's a program running somewhere else, waiting to *do* something when
you ask it to — save something, send an email, check a password. My site itself has no backend
(GitHub Pages only serves static files, it can't run code), so the contact form's actual "do
something" work happens on Web3Forms' servers, not mine. My page just sends them a request; they
do the real work of turning that into an email.

## What my feature does

Someone types their name, email, and a message into the form and clicks "Send message." That's
it from their side — no page reload, no redirect to a different site.

## How the data actually flows

1. **The click.** JavaScript on my page (a small `<script>` block) intercepts the form submit —
   instead of letting the browser do its default behavior (reload the page and navigate to
   wherever the form points), my script grabs the typed values itself.
2. **The request.** My script packages those values (name, email, message) and sends them as an
   HTTP POST request — not to my own site, to `api.web3forms.com`. This is the only network call
   involved; there's no database or server of mine in the middle.
3. **Web3Forms' side.** Their server receives that POST, checks it against the access key I
   included (which tells them *which* account/inbox this belongs to — mine), and if it's valid,
   formats the message and sends it as a real email to the address I registered.
4. **The response.** Web3Forms sends a small JSON reply back ("success: true" or an error) to my
   page's script, which is what makes the "Sent — thanks" message appear without the page ever
   reloading.
5. **My inbox.** A normal email shows up, from Web3Forms, containing whatever the visitor typed.

## Why this design, not something else

I didn't build my own backend (a real server with my own code) because I don't need one yet — a
contact form is the textbook case for a small free tool like Web3Forms: no server for me to run,
patch, or pay for, and no database, since I'm not storing anything, just relaying it to email.
That's a deliberate "smallest tool for the actual job" choice, the same reasoning as my Week 4
stack decision — more infrastructure than this would be solving a problem I don't have.
