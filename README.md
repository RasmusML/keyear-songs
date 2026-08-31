# keyear-songs

The built-in songs for [KeyEar](https://keyear.app), as plain General MIDI
files. They live here rather than in the app repo so that adding or re-cutting
a song is not an app commit, and so their history (binary, and steadily
growing) stays out of the application's own.

```
songs/*.mid
```

**[SONGS.md](SONGS.md) lists what each file is** — title, composer, genre and
per-track difficulty. The filenames are UUIDs, so that table is the only way
to tell them apart at a glance; it is generated from the files themselves
rather than typed, and the app's test suite fails if the two disagree.

## How the app consumes this

The app pins an exact commit of this repo in its own `assets/songs.pin.json`
and fetches it at build time. Nothing here is read at runtime: the build
copies these files into the app's static assets and generates an index
(`catalog.json`) beside them, which is what the song dropdown reads. Picking a
song then downloads just that one file.

Because the pin names a commit, pushing here changes nothing for anyone until
the app repo moves its pin. That is deliberate: a song is content, and content
should not ship itself.

## The files

Filenames are UUIDs because they came out of KeyEar's song editor, which names
its exports by id. That is harmless: a file carrying a `[KeyEar.Metadata]`
block is named in the app by its `Title` and `Composer`, never by its
filename, so `fdd882ad-….mid` appears in the song dropdown as
"Für Elise - Ludwig van Beethoven".

Each file carries its own metadata block as an ordinary MIDI text meta event:
title, composer, genre, per-track ear-training levels and tags. Any other
program reading the file sees a text event and ignores it. The format is
documented in the app repo's README, under Song metadata.

## Adding a song

1. Export it from the KeyEar song editor, which writes the metadata block.
2. Drop the `.mid` into `songs/`.
3. Regenerate the listing from the app repo:
   `npx tsx scripts/build-songs-md.ts ../keyear-songs`
4. Commit and push both.
5. Update `assets/songs.pin.json` in the app repo to the new commit, and run
   `npm run sync-assets`.

## Provenance and licensing

Where each song came from, which reference score it was made from, and the
state of its licensing are recorded in the app repo (`assets/songs-sources.md`),
which is private. Check it before adding a song here or shipping one: the
compositions are out of copyright, but a specific arrangement is its
transcriber's own work.
