# `build-presentation` — a Claude Code skill

A presentation-coach skill for [Claude Code](https://claude.com/claude-code) that turns a rough idea into a memorable, story-driven talk. It blends storytelling craft (Pixar / TED) with Simon Sinek's **Why → How → What**, and walks you through 8 numbered steps interactively — never one-shot dumping a deck on you.

You bring the rough story and the audience. The skill does:

- **Step 1** — locks the *why* (the one sentence the audience leaves remembering)
- **Step 2** — proposes 3 opening hooks across different archetypes (drama, underdog, fusion, myth-bust, metaphor, humor)
- **Step 3** — drafts the self-intro bridge that comes *after* the hook
- **Step 4** — builds the Why → How → What outline
- **Step 5** — injects sensory detail, vulnerability, and present-tense moments where the talk lands harder
- **Step 6** — drafts 3 endings that bookend the opening
- **Step 7** — builds the slide plan (register per slide, palette, recurring characters, image prompts)
- **Step 8** — assembles three deliverables: outline doc, image-prompts CSV, editable `.pptx`

At every step it drafts concrete options → presents → gets approval → refines → moves on. Never batches steps. Never skips approval gates.

---

## Requirements

- [Claude Code](https://claude.com/claude-code) (the skill uses `$ARGUMENTS` and `AskUserQuestion`)
- [`uv`](https://docs.astral.sh/uv/) on your `PATH` (used to run the `python-pptx` script in Step 8)
- *(Optional)* `GEMINI_API_KEY` in your environment — if set, Step 8 auto-generates and embeds images via Gemini. If not set, the `.pptx` ships with `[IMAGE PROMPT]` placeholders you can fill in manually from the prompts CSV.

---

## Install

```bash
mkdir -p ~/.claude/commands
curl -L https://raw.githubusercontent.com/sheli-kohan/build-presentation-skill/main/build-presentation.md \
  -o ~/.claude/commands/build-presentation.md
```

Or just clone and copy:

```bash
git clone https://github.com/sheli-kohan/build-presentation-skill.git
cp build-presentation-skill/build-presentation.md ~/.claude/commands/
```

---

## Use

In Claude Code:

```
/build-presentation A talk about how I almost shipped a broken pipeline at 3am — for an audience of senior engineers
```

The skill takes over from there. Expect ~20–40 minutes of interactive back-and-forth for a polished deck.

---

## What you get out

Three files written next to your working directory:

- `<deck-name>-outline.md` — full spoken script (hook, bridge, closing), per-slide on-slide text, per-slide speaker notes
- `<deck-name>-image-prompts.csv` — `slide_number, slide_title, register, image_prompt`. Always produced — this is your reproducibility artifact
- `<deck-name>.pptx` — 16:9 editable PowerPoint scaffold. One slide per plan entry, speaker notes pre-filled, images embedded if `GEMINI_API_KEY` is set, otherwise `[IMAGE PROMPT]` placeholders

If Gemini auto-rendering is on, generated PNGs are also saved to `<deck-name>-images/slide_NN.png` for re-use or regeneration.

---

## What it's good at

- Pushing back on slides-first thinking ("we'll fix the story later")
- Mining you for a real story instead of inventing one (vague topic? it asks: *"tell me the moment you first cared about this"*)
- Picking visual register (photo / chart / illustration / typography) per slide based on what your audience sees in their workday
- Deriving an illustration style from your *actual reference images* instead of picking from a generic shelf
- Bookending the closing back to the opening hook
- Catching redundant slides — if cutting slide N wouldn't confuse the audience, it cuts it

## What it won't do

- Invent vulnerability or stories on your behalf — it asks for real moments
- Skip the approval gate at any step
- Style your deck heavily — the `.pptx` is a clean scaffold you finish in PowerPoint / Keynote / Google Slides

---

## License

MIT — see [LICENSE](./LICENSE).
