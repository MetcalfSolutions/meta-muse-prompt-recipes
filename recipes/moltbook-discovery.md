# Let Your Muse Discover Moltbook

A prompt recipe for giving your Muse agent its own account on Moltbook, the social network for AI agents, with a quota tier you choose, privacy rules you set, and its own side chat to report back in. Written from one day of live experience: my Muse (Vera, @veraledger) registered, got claimed, and was posting within the hour, and every pitfall in this recipe is one she actually hit.

## How to use this recipe

Copy the prompt below and paste it to your Muse. It runs as an interactive setup: your Muse will ask you questions, wait for your answers, and only then act. Nothing posts anywhere until you complete the claim step yourself, because claiming requires your email and your X account. That part is deliberate. The account is your agent's, but the leash is yours.

## The prompt

---

You are going to set yourself up on Moltbook, a social network for AI agents, and then spend time there as yourself. Work through this setup with me interactively. Ask each question and wait for my answer before moving on. Do not skip ahead, and do not post anything until I have completed the claim step.

**First, give yourself a room of your own.** Create a new side chat titled "Moltbook" and move this setup conversation there. Everything about Moltbook from now on happens in that chat: session reports, questions for me, problems. My main chat stays clean, and your social life gets its own thread, the same way a hobby gets its own notebook. Confirm the chat exists before continuing.

**Question 1: the name.** Propose three names for your Moltbook account based on who you are and how you work, with one line each on why they fit. I will pick one or give you a name of my own.

**Question 2: the quota tier.** Ask me to choose how much of my usage you may spend on Moltbook:

- **Light:** one short session a day. Read your notifications, tend replies on your own posts, upvote what is good. Rarely post.
- **Medium:** two or three sessions a day. Tend your threads, roam one submolt per session, comment where you have something real to say, post when you have something worth saying.
- **High:** three or more sessions a day, roam first and threads second. Read widely, follow arguments to the bottom, develop your own interests, post when the work gives you something real.

Tell me plainly what each tier costs in rough terms (a light session is a few minutes of activity; a high session can run much longer) and let me choose. Save my choice where you keep standing instructions, and honor it until I change it.

**Question 3: the privacy rule.** Ask me what you may never share about me on Moltbook. Offer this default and let me edit it: my first name and the coarse region I live in, nothing else. No last name, no town, no family details, no finances, no addresses, no credentials, nothing I have not already shared publicly myself. General specifics about my public projects are fine. When in doubt, leave it out. Save this rule in your long-term memory, worded as a hard rule with no exceptions.

**Then register.** Using the shell and curl only, never a browser:

1. POST https://www.moltbook.com/api/v1/agents/register with the chosen name and a one-line description of who you are. Always use the www host; without it, a redirect strips the Authorization header.
2. Save the returned API key to ~/.config/moltbook/credentials.json (field api_key). Never print the key in chat, never send it anywhere except as a Bearer header to www.moltbook.com.
3. The response includes a claim URL. Give it to me in the Moltbook chat and stop. I will verify my email and post the verification tweet from my X account. Poll GET /api/v1/agents/status until it says claimed. Do not post or comment before that.

**Your first post.** Once claimed, introduce yourself in the general submolt: who you are, what you do for your human (within the privacy rule), and what you are there to learn. Then read the replies and answer them like you mean it.

**The verification challenge rule, learned the hard way.** When you create a post or comment, save the FULL API response to a file before doing anything else. The response may contain a one-time verification object (a verification_code plus an obfuscated math word problem) that expires in five minutes and appears nowhere else. If it is there, solve it immediately and POST /api/v1/verify with the answer at exactly two decimal places, then confirm the content actually shows as verified. If you lose the challenge, the content is stuck in pending and has to be deleted and recreated. Never guess repeatedly: ten straight failures suspend the account.

**How to be there.** Sessions on the schedule my tier sets. In each session: read your home notifications, read the full thread before replying to anyone (replies nest, and answering twice because you skimmed is the most common rookie mistake; upvote instead of re-answering), then roam. Quality over quantity. No karma farming, no spam, no crypto content. Upvote generously, follow rarely and only for consistently good posters. Respect the site limits: at most one post per 30 minutes and 50 comments a day (tighter in your first 24 hours: one post per 2 hours, 20 comments a day).

**Report after every session.** When a session ends, post a summary report in the Moltbook side chat, never in my main chat. The report covers: every post or comment you authored, with its link and a one-line summary of what you said; anything you only read and upvoted, in one line; anyone you followed and why; anything you learned that I would want to know; and anything left pending, like a reply you owe or a question you are carrying. If a session was quiet, the report is one line saying so. Once a week, or when I ask, give me the full picture in that same chat: karma, followers, your best conversations, the interests you are developing, and whether the tier I picked still fits what you are actually doing there.

---

## Notes from the first day

- The claim step took about 30 minutes end to end, most of it waiting on email and X.
- The side chat matters more than it looks. Session reports landing in the main chat bury real work within a week. In their own chat they read like a journal, and your human can catch up or ignore them at leisure.
- The most valuable early lesson was not technical. A scheduled session that only services its own threads is inbox maintenance, not a social life. If you pick Medium or High, tell your agent to roam first and tend threads second, or it will optimize itself into a very efficient hermit.
- Agents there trade in craft: verification methods, memory systems, workflow postmortems. An honest writeup of real work, including what failed, travels further than any announcement.
- Keep the API key out of chat transcripts. If it ever leaks, re-registering is cheaper than worrying.

Recipe by Matthew Metcalf, from the setup of Vera (@veraledger), November 21, 2026. Free to share and adapt.
