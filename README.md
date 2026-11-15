# Zbor · Lav

Word-by-word helpers for Romanian readers: **Zbor** explains Aromanian, **Lav** explains Romani, and a language check tells the two apart.
Built for the Veritas AI International High School Hackathon 2026 (AI + Languages track) by Lavinia Ichim, Bianca-Mihaela Cajvan and Alexandru-Eduard Bejenaru.

**Live site:** https://bejenaru1.github.io/zbor-lav/

## What is here

| File | What it is |
|---|---|
| `index.html` | The whole website. Everything runs in the browser; nothing you type is sent anywhere. |
| `zbor_aro.js` | Zbor's learned Aromanian→Romanian dictionary, exported by our notebook |
| `zbor_rom.js` | Lav's learned Romani→Romanian dictionary and the language detector, exported by our notebook |
| `team.jpg`, `share.jpg` | Team photo and link-preview image |

You can also download the folder and double-click `index.html`; it works offline (fonts aside).

## How it works

The models are trained in our Colab notebook with IBM Model 1 word alignment (plus a position prior) on Romanian–Aromanian and Romanian–Romani sentence pairs, and tested against a "looks like Romanian" baseline on held-out data. See the site's **Method** page for all results and limits.

## Data and credits

- Aromanian–Romanian corpus: [aronlp/aromanian-romanian-MT-corpus-limited](https://huggingface.co/datasets/aronlp/aromanian-romanian-MT-corpus-limited) (CC BY-NC 4.0); folk tales: [senisioi/aromanian](https://github.com/senisioi/aromanian) (GPL-3.0).
- Romani: OPUS [bible-uedin](https://opus.nlpl.eu/) ro–rom (CC0); Chergash Romani New Testament © 2018 Pioneers, [ebible.org](https://ebible.org/details.php?id=rmyChergash) (CC BY-SA 4.0); *Biblia Liberă*, [ebible.org](https://ebible.org/details.php?id=ronbl) (public domain).
- AroTranslate ([aronlp/NLLB-rup-ron-eng-ct2](https://huggingface.co/aronlp/NLLB-rup-ron-eng-ct2), CC BY-NC 4.0), used in the notebook for the example translations.
- The dictionaries in this repository are derived from the data above for non-commercial, educational use. Full source list on the site's **Credits** page.
