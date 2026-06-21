# Kaggle upload — operator steps (~2 minutes)

The KG sample is already public on GitHub + Hugging Face. Kaggle is the last
distribution surface. Everything is staged in this directory; the upload needs
**your** Kaggle API token (I can't enter credentials on your behalf).

## One-time setup

1. Install the CLI:
   ```
   pip install kaggle
   ```
2. Get your API token: kaggle.com → your profile → **Settings** → **API** → **Create New Token**.
   This downloads `kaggle.json`. Place it at:
   - Windows: `C:\Users\User\.kaggle\kaggle.json`
   - (the folder must exist; create it if needed)

## Edit the manifest

Open `dataset-metadata.json` in this folder and replace
`REPLACE_WITH_YOUR_KAGGLE_USERNAME` with your Kaggle username (lowercase). The
`id` becomes e.g. `arul/cricketstudio-knowledge-graph`.

## Create the dataset (first publish)

From this directory:
```
kaggle datasets create -p . --dir-mode zip
```

The dataset goes live at `https://www.kaggle.com/datasets/<your-username>/cricketstudio-knowledge-graph`.

## Update later (new version)

When the sample is regenerated:
```
kaggle datasets version -p . -m "v2: all 10 franchises + player attributes" --dir-mode zip
```

## What gets uploaded

Only the data files in this directory: `nodes.{json,csv}`, `edges.{json,csv}`,
`schema.json`, `README.md`, `LICENSE` + this manifest. All moat-safe (slug-keyed,
no internal ids, no external-ID crosswalk). Identical to the GitHub + HF copies.

> Note: this file and `dataset-metadata.json` are local staging — they are not
> committed to the public GitHub repo (the GitHub copy stays data-only).
