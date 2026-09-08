# Spotify Song Recommender

A content-based song recommender built on Spotify audio features
(danceability, energy, acousticness, etc.) plus track/artist text, combined
into feature vectors and compared with cosine similarity to recommend the
top 5 most similar songs to a given track.

> **Provenance note:** this notebook was reconstructed from a scrolling
> screen-recording after the original Google Colab notebook became
> inaccessible (via frame extraction + OCR). Most of it has been verified
> logically, but a few small gaps remain — see **Known Gaps** below before
> relying on it.

## What it does

1. Loads a Spotify dataset (artist, track, year, and audio features).
2. Combines each song's text fields (artist + track) into a single string
   and vectorizes them with `CountVectorizer`.
3. Normalizes the numerical audio features and concatenates them with the
   text vectors to form one feature vector per song.
4. Computes a cosine-similarity matrix across all songs.
5. Given a song (typed or picked from a dropdown widget), looks up its
   5 most similar songs and prints them.
6. Wraps the whole thing in a reusable `SongRec(song_title)` function.

## Setup

```bash
git clone <this-repo-url>
cd spotify-recommender
python3 -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

Then either open `spotify_recommender.ipynb` in Jupyter/VS Code and run
cells top to bottom, or explore `spotify_recommender.py` (the same
notebook in `# %%`-cell script form, handy for diffing in git).

```bash
jupyter notebook spotify_recommender.ipynb
```

You'll also need the dataset. The first cell fetches it via `wget` from a
Google Cloud Storage bucket — see **Known Gaps** below, the URL needs to be
completed before this will run.

## Known Gaps

These are spots where the source recording was cut off or obscured, not
just style nits — the notebook won't run cleanly until they're resolved:

- **Truncated data URL** (first cell): the `wget` URL got cut off by the
  scroll before this was recorded. You'll need to relocate the full URL
  (e.g. from original course materials) or point `data_path` at your own
  copy of the CSV.
- **Incomplete `numerical_features` list**: only 5 features were visible
  before the list scrolled out of frame, but the code clearly expects at
  least `instrumentalness` too. Likely candidates based on standard
  Spotify audio features: `liveness`, `valence`, `tempo`, `key`,
  `loudness`, `mode`. Run `data.columns` once you have the real CSV and
  reconcile.
- **`fix_genres` is referenced but never defined** in any captured frame.
  It's inside a conditional that doesn't trigger with the current
  `text_features` list, so it may be safely dead — but if you add a
  `genres` feature later, you'll need to write this function yourself.
- **`SongRec()`'s body was partially obscured** by a UI overlay in one
  frame. It's been reconstructed from the equivalent manual steps a few
  cells earlier and should be logically equivalent, but hasn't been run
  end-to-end. Compare its output for `'died in your arms'` against the
  expected result documented in the last cell to confirm.

## License

MIT — see [LICENSE](LICENSE). Update the copyright name before publishing
if you want it attributed to you.
