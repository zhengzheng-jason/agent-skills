# ASD-STE100 writing rules (condensed)

ASD-STE100 Simplified Technical English is a controlled language. It was made for aerospace maintenance documents. Its goal: one clear meaning per sentence, for readers of any language level.

## Strict mode

Words:
- Use simple, common words. Prefer the approved form: `use` (not utilize), `start` (not commence), `stop` (not terminate), `before` (not prior to), `to` (not in order to), `about` (not approximately), `make sure` (not ensure).
- Use one word for one meaning, and one meaning for one word. When you name a thing, use that name every time. Do not change to a synonym.
- Technical names (`TCP`, `useEffect`, `S3 bucket`) and technical verbs (`compile`, `deploy`, `hash`) are permitted.
- Do not use idioms, slang, metaphors, or phrasal verbs when a single verb exists (`find` not `figure out`, `remove` not `take out`).
- Do not make noun clusters of more than 3 words. Split them: "cache invalidation retry policy" → "the retry policy for cache invalidation".
- Keep articles (`the`, `a`) and `that`. Do not drop them to save words.

Verbs:
- Use the active voice. Name the actor: "The scheduler starts the job", not "The job is started".
- Use only simple tenses: present, simple past, simple future.
- Do not use the `-ing` form, except in technical names.
- Write instructions as commands (imperative).

Sentences and paragraphs:
- Procedural sentence (instruction): 20 words maximum. One instruction per sentence, unless two actions occur at the same time.
- Descriptive sentence: 25 words maximum. One topic per sentence.
- Paragraph: 6 sentences maximum. One topic per paragraph. Start with the topic sentence.
- Use a vertical list for a sequence or a set of items.
- Put a condition before the instruction: "If the build fails, read the log."
- Put a warning before the step it applies to.

## Soft mode (default, "80% STE")

Strict STE gives short, choppy sentences. Many short sentences in a row can be harder to follow than a few connected ones. Soft mode keeps the clarity rules and relaxes the rhythm rules.

Keep:
- active voice, with a named actor
- one term per concept, used the same every time
- no idioms, no hype, no filler
- noun clusters of 3 words or fewer
- topic sentence first, one topic per paragraph
- lists for steps and sets

Relax:
- No approved-word list. Use the most common precise word.
- Sentences up to about 30 words. Use `because`, `so`, `but`, and `which` to join two closely related ideas when one sentence reads better than two.
- Vary the sentence length so the text does not read like a list of telegrams.
- `-ing` forms and other tenses are permitted when they are clearer.

## Check before you send

- Can you remove a word without loss of meaning? Remove it.
- Does a term change name halfway through? Use one name.
- Does a sentence have two ideas that are not related? Split it.
- Is there a passive verb that hides who does the action? Make it active.
