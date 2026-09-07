---
name: doc-writing
description: Writing conventions for Spinal internal docs. Load before writing or editing any .mdx page, and when asked to review a page for prose that reads as machine-written, vague, or jargon-heavy. Ends with a review pass that must run before a page is called done.
---

# Writing internal docs

The bar: a new engineer reads the page once and can act. Nothing in it reads as
machine-written. Plain words, specific facts, real names.

## Before you write

- Say who reads this and what they will do afterwards. Name that task in the first two
  sentences of the page.
- Write only what has to be true for them to succeed. Cut the rest.
- Know the facts. If a value is unknown, say so or leave a marked gap. Never pad a gap
  with confident-sounding filler.
- Use the real names from the repos and the clouds. Never invent a name for something.

## Voice

- Second person, active voice. "Run the job", not "The job can be run".
- Say "is" and "has". Not "serves as", "functions as", "acts as", "represents",
  "boasts", "features", "offers".
- One idea per sentence, about twenty words. A semicolon means two sentences.
- The plain word wins: use, start, before, about, need, show, change, end.
  Not: utilise, leverage, initiate, prior to, regarding, require (as filler), showcase,
  enhance, facilitate, streamline.
- Define a term once, on first use, then use that same term every time. Do not vary
  words for style; "elegant variation" makes a reader wonder if you mean something new.
- Concrete beats abstract. Name the file, the command, the error text, the resource.
  Commands go in code blocks. File names, paths, and flags go in backticks.
- Numbers that change what the reader does go in a table or on their own line. Numbers
  that do not, go.

## Jargon

- Product and infrastructure names are fine because readers must learn them: Cloud Run,
  Lighthouse, ARM, Artifact Registry. Define each once and link to the page that
  explains it.
- Avoid abstractions that hide the mechanism: "orchestration layer", "identity fabric",
  "security posture", "the platform". Say what actually happens: which process runs
  where, as whom, and what it calls.
- Expand an acronym on first use unless the whole team uses it daily (GCP, PR, CI, IAM).
- If a sentence needs three technical terms to be understood, it is probably two
  sentences, or it belongs in a deep-dive page with a link from here.

## What makes text read as machine-written

Adapted from Wikipedia's *Signs of AI writing*. Each is a symptom. Fix the vagueness
underneath it; swapping the words while keeping the emptiness only makes it harder to
spot.

| Pattern | Looks like | Do instead |
|---|---|---|
| Significance inflation | "pivotal", "crucial", "plays a vital role", "stands as", "a testament to", "the landscape" | State the fact. The reader decides what matters. |
| Puffery | "robust", "seamless", "powerful", "comprehensive", "elegant", "cutting-edge", "best-in-class" | Describe the behaviour. "Retries once" beats "robust". |
| Superficial -ing analyses | ", ensuring …", ", highlighting …", ", allowing …", ", enabling …" tacked on a sentence | If the clause carries a fact, make it its own sentence. If not, delete it. |
| Negative parallelism | "not just X, but Y", "it's not X, it's Y", "X rather than Y" where X is a strawman | Say Y. |
| Rule of three | Three adjectives or three examples by habit | Use the real count. |
| Vague attribution | "best practice says", "it is widely known", "experts agree" | Name the source or drop the claim. |
| Avoiding "is" | "serves as the entry point", "functions as", "represents" | "is the entry point". |
| Outline-like closers | "Challenges and future outlook", "Looking ahead", "In summary", a final paragraph restating the page | Stop when the content stops. |
| AI vocabulary | delve, intricacies, tapestry, meticulous, align with, foster, showcase, underscore, empower, holistic, navigate, streamline, leverage, utilise, "it's worth noting", "it is important to note" | The plain word, or nothing. |
| Throat-clearing | "Essentially", "Basically", "In today's world", "In the realm of", "It should be noted that" | Delete the phrase. Start at the fact. |
| Chatbot artefacts | "I hope this helps", "Let me know if", "Certainly", "Great question", knowledge-cutoff hedges, "[insert …]" placeholders, leftover citation tokens | Delete. A page is not a reply. |

### Formatting tells

- **Em dashes as the default joiner.** They are the strongest single tell. A full stop or
  a comma almost always works. Keep at most one or two per page, and never two in one
  sentence.
- **Bold for emphasis.** Bold only UI labels and, at most, the first few words of a
  bullet. Never a whole sentence.
- **Headings with nothing under them**, or a heading followed straight by a bullet list.
  Put at least one sentence of prose under every heading.
- **Skipped heading levels** and **Title Case Headings**. Use sentence case; go H2 to H3.
- **Emoji**, **horizontal rules**, and **curly quotes**. None.
- **Tables where a sentence would do.** A table is for rows that a reader compares.
- **Callouts as decoration.** One `<Note>`, `<Warning>`, or `<Tip>` per screen at most,
  and only when the reader would otherwise miss something that costs them.

## Structure

- Frontmatter: `title`, `sidebarTitle`, `description` (one sentence that says what the
  reader gets), `icon`.
- Lead with what the page is for and what the reader will be able to do.
- Use a code block for a sequence of steps a shell would run. Use `<Steps>` for steps a
  human performs in a UI.
- A bullet is one or two sentences. A list of parallel things is a list; an argument is
  prose.
- MDX hazards: any `<placeholder>` and any `{` or `}` in prose must sit inside backticks
  or a code fence, or the build breaks.

## Example

Before:

> Leveraging workload identity federation, the fleet identity seamlessly enables secure,
> secretless Azure access — ensuring robust cross-cloud authentication and empowering
> teams to deploy with confidence.

After:

> The job logs into Azure with a token minted from its GCP service account. There is no
> Azure client secret.

The second version is shorter, names the mechanism, and makes a claim a reader can check.

## Review pass

Run this before calling a page done. It is not optional.

1. Read the page as the new engineer would. Everywhere you pause to decode, rewrite.
2. Scan for tells. From the repo root:

   ```bash
   grep -nE ' — |not (just|only) |rather than|\b(ensur|highlight|leverag|showcas|foster|streamlin|robust|seamless|crucial|pivotal|delve|landscape|tapestry|utili[sz]|facilitat|empower|holistic|underscore)|worth noting|important to note|Essentially|Basically|In summary' <page>.mdx
   ```

   Every hit is a sentence to fix, not a word to replace.
3. Check the shape: every heading has prose under it; no level skipped; no bold sentence;
   bullets of one or two sentences; callouts only where they earn it.
4. Check the mechanics: every command in a code block; every file, path, and flag in
   backticks; every placeholder in backticks.
5. Cut the last paragraph if it only restates the page.
6. If the page explains a system, confirm one concrete "so what" for the reader in the
   first screen: what they run, what they will see, or what they must not do.
