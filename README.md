# Spotify Song Recommender

A content-based song recommender built on Spotify audio features
(danceability, energy, acousticness, etc.) plus track/artist text, combined
into feature vectors and compared with cosine similarity to recommend the
top 5 most similar songs to a given track.

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

## License

MIT — see [LICENSE](LICENSE). Update the copyright name before publishing
if you want it attributed to you.
