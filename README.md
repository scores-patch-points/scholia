# Scholia

In the Alexandrian libraries, *scholia* were the notes scholars wrote in the margin of a text. This tool does the same for a machine reading: it shows the text with what the reader marked beside it.

One call to khora's `readToWeft` returns an entry. A read **appends to no log**; nothing is written to disk. Scholia renders that entry as one static HTML page:

- the text, every word tinted by its class (noun, verb, preposition, ...), with names, pronoun bindings (confident, or a contested guess) and prepositional phrases marked, each with a toggle;
- every he/she-class pronoun and the being it was bound to;
- every sentence as a dependency tree (each word under its head, with its relation) and as a clause nest (relation, marker, subject, predicate, object, polarity);
- every top-level field of the entry, expandable, raw.

## Use

Scholia reads through [khora](https://github.com/scores-patch-points/khora) (English only for now). Point it at a checkout:

```bash
node build.mjs --khora ../khora --file my-text.txt --out scholia.html
```

`--khora` can also be the `KHORA_DIR` environment variable, and defaults to `../khora` beside this repo. With no `--file` it renders a short demo passage. Open the HTML file in a browser; it is self-contained.

## What to trust

The word classes and trees come from khora's English dependency parser. It is judged by a fixed external giver, the official CoNLL 2018 UD evaluation script (khora round 26, gold tokenization): UPOS 94.1, UAS 77.1, LAS 72.7 on GUM dev (a set the parser never saw); LAS 76.6 on EWT test (possibly seen in training). About one prepositional phrase in five gets its head in the wrong class ("at the station on Tuesday" is hung on "John" and not on "met"). Expect wrong attachments, and use the page to see them.

## Test

```bash
KHORA_DIR=../khora npm test
```

The test skips itself when no khora checkout is found.

## Licence

None chosen yet; until one is added all rights are reserved by the author.
