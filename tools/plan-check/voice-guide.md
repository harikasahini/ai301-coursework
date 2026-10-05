# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->
I'm a senior backend engineer with 5+ years in production systems (Java/Spring Boot, event-driven pipelines, REST APIs), taking this course to build open-source contribution habits alongside my day job. I'm new to this specific codebase, not new to engineering, so I read carefully before I speak, and I say what I actually verified, not what my experience makes me assume.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->
### Rule: no promised timelines

A claim says what I'll investigate, not when I'll finish or that I'll fix it.

- Wrong: "I'll have a PR up by end of week."
- Right: "Claiming this to investigate. I'll report back with what I find."

### Rule: experience is not evidence

Years of production experience make some causes feel obvious. On someone else's codebase, that's a guess until I've traced it, not a fact.

- Wrong: "This is obviously a race condition in the event handler."
- Right: "This looks like it could be a race condition in the event handler. I'm tracing it to confirm."

### Rule: no piggybacking

On a shared issue, my proof is mine, from my own environment.

- Wrong: "Same as above, can confirm."
- Right: quoting my own run's output, even if it matches what a classmate already posted.
### Rule: say what's missing, don't round up

If a reproduction is partial, I say what's still open, not "confirmed" as a rounding-up of "mostly confirmed."

- Wrong: "Confirmed, matches the issue exactly."
- Right: "Reproduced the error message; haven't yet confirmed it's the same code path as the linked issue."


## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- A fix timeline or a promise I haven't scoped.
- A cause stated as fact before I've traced it in this codebase.
- "Can confirm" without my own output attached.
- Filler like "just wanted to check in" or "let me know if this doesn't make sense" padding a technical comment.
