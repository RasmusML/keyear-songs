# Songs

Generated from each file's own `[KeyEar.Metadata]` block by the app repo's
`scripts/build-songs-md.ts`, not typed by hand, so it cannot drift from what
the app actually shows. The app's test suite re-derives this table from the
files and fails if the two disagree.

Filenames are UUIDs because they came out of KeyEar's song editor, which names
exports by id. That is deliberate: the filename is stable identity, so
retitling a song does not rename its file, and does not change its URL in the
shipped app. The cost is that the directory listing says nothing on its own,
which is what this table is for.

| File | Title | Composer | Genre | Per-track levels |
| --- | --- | --- | --- | --- |
| `3dddcf20-d0b7-4813-8b34-7109b9fe2f6d.mid` | Ave Maria | Franz Schubert | Classical | 6, skip, 4 |
| `66d08645-450c-4bb3-b605-be4c7d995ed2.mid` | Canon in D | Johann Pachelbel | Classical | 7, 5 |
| `7a560608-0a6d-4e7c-99cd-bb1bfa765da5.mid` | La Campanella | Franz Liszt | Classical | 3, skip, 3 |
| `7e130739-d2fc-4456-9128-8e8bdbf4707c.mid` | The House of the Rising Sun | American traditional folk song | — | 6, skip, 4 |
| `fdd882ad-ccaf-471e-84a7-f896658010f9.mid` | Für Elise | Ludwig van Beethoven | Classical | 3, 3 |

`skip` marks a track that should not be ear-trained against — an
accompaniment figure or a dense voicing, not a line a person could sing back.
It is deliberately distinct from level 1, which means "trivially easy".
— means the file states nothing for that field, or states a level per
track that no longer matches the tracks it has.
