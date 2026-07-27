# رسالةٌ لا تصل / al-Buna

<p align="center">
  <img src="assets/pull-quote.svg" alt="الكرسيُّ الفارغُ لا يخدعُك، هو فقط لا يُجيب — the empty chair doesn't deceive you, it just doesn't answer" width="720">
</p>

An Arabic literary parable about knowing what you can't confirm — three narrator voices, an interactive council you can seat yourself in, and an appendix that maps every symbol back to its distributed-systems concept.

**[Read it live →](https://mokenawy.github.io/al-buna/)**

<details>
<summary><strong>Unfold the manuscript</strong> — a few lines before you decide whether to open the rest</summary>

> *وُجِدَ هذا الدفترُ في برجِ الحراسةِ الشرقي، بعد أن خلا المكانُ بزمنٍ طويل. لا تاريخَ على صفحاته — يبدو أنَّ صاحبَه كان يرتابُ في التواريخِ أيضاً.*
>
> اسمي لا يُهِمّ. في هذا المعسكر يُنادونني بِـ«الشاكّ»... وأنا قد أجريتُ حسابَ الثقةِ مِراراً، فوجدتُه لا ينغلقُ أبداً. فأنا أعلمُ الأمر، وأريدُ أن أتأكَّدَ أنَّ صاحبي يعلمُه أيضاً، فأنتظرُ منه إشارة. وحين تصلُني الإشارةُ، أحتاجُ أن يعلمَ هو أنَّها وصلتْني... وهكذا، بلا نهاية.

*Found notebook, no dates — the guard doesn't trust dates either. Full text: [`الرسالة-التي-لا-تصل.md`](./الرسالة-التي-لا-تصل.md).*

</details>

## The problem

Distributed-systems concepts — Byzantine faults, quorums, the `n > 3f` threshold, the gap between safety and liveness — are usually taught through protocol diagrams and proofs. That's precise, but it doesn't transfer intuition: nobody *feels* why an absent voter is honest and a lying voter is dangerous just by reading a theorem.

The Arabic technical-writing space also has a specific gap: most of what exists is translation, not original work written to be read in Arabic first. Al-Buna is an attempt at both problems at once — carry BFT through narrative instead of notation, and write it as literature that happens to be technically exact, not as a translated explainer.

The text is a found manuscript: a doubt-ridden gate guard who becomes the scribe of a nine-member council, deciding a river dispute under a hundred-year-old majority rule. Every plot beat — the messenger who can't confirm delivery, the empty chair that "doesn't lie, it just doesn't answer," the old counselor doing the vote arithmetic — is a specific BFT concept wearing a story.

## Decisions

**Prose first, simulation second, appendix third.** The three narrator voices (skeptic, chronicler, believer) carry the concept load. The interactive council simulation lets a reader test the majority rule themselves instead of taking the narrator's word for it. The appendix is the only place vocabulary is named explicitly — Arabic term, English term, side by side — so the story itself never has to break voice to explain itself.

**No framework, no build step.** The whole reading experience — chapters, reveal-on-scroll, the council simulation, the appendix lexicon — is one `index.html` with inline CSS and JS. The alternative was a React/Vite site; rejected because the piece is a document, not an application, and a document should survive being opened from a plain file listing on GitHub Pages with zero tooling between the repo and the reader.

**Chapter narration is optional and per-chapter, not autoplay-on-load.** Audio files live in `audios/` and are wired to a corner toggle rather than starting on page load, so the text stands on its own for a silent read and the narration is there for anyone who wants it.

**Concepts are tagged, not glossed inline.** Rather than footnoting distributed-systems terms into the prose (which would break the literary register), each chapter closes with a `concept-tags` line and the full mapping lives in the appendix lexicon. The story reads clean; the appendix is where you go to check your understanding against the actual theory.

## The lexicon (a preview)

The full mapping lives in the appendix at the end of the piece. A sample:

| In the story | المفهوم | Concept |
|---|---|---|
| The road | قناةُ الاتصال | the channel |
| The guard / member | العُقدة | the node |
| The messenger | الرسالةُ المنقولة | the message / packet |
| The council's ruling | الإجماع | consensus |
| The empty chair | عُقدةٌ متوقّفةٌ صادقة | crash fault |
| The lying member | عُقدةٌ خبيثة | Byzantine fault |
| The one-third threshold | حدُّ تحمُّلِ الأعطال | the `n > 3f` bound |
| The quorum | الأغلبيةُ اللازمةُ للقرار | quorum |
| The seal on the letter | التوقيعُ المُعمَّى | cryptographic signature |

## Hear it

<audio controls src="audios/intro%20-%20approved.wav"></audio>

The opening narration, in the mystic voice used for Chapter I. Narration is optional throughout — a corner toggle on the live page, off by default — because the text is written to stand on a silent read first.

*(If the player above doesn't render in your GitHub client, the file is at [`audios/intro - approved.wav`](<./audios/intro - approved.wav>).)*

## What went wrong

The first pass tried to gloss the theory *inside* the narrative voice — a parenthetical here, a footnote there — to make sure a technical reader wouldn't miss the mapping. It read like a lecture wearing a costume. Pulling every explicit concept name out of the chapters and into a dedicated appendix (see `index.html`, the `.appendix`/`.lexicon` sections) is what let the prose commit to being prose. The lesson: if a piece has to work as literature *and* as an explainer, don't try to make one sentence do both jobs — split the surfaces.

## Running it

Deployment is automatic: `.github/workflows/static.yml` pushes `main` straight to GitHub Pages — the whole repo is the artifact, no separate `dist/`.

## Status

Live and complete for Chapter I, with narration and the interactive council shipped. Later chapters and the full appendix lexicon are in progress — check `index.html` for what's currently revealed versus scaffolded.
