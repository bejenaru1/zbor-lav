# Zbor · Lav

**Track:** AI + Languages
**Team:** Lavinia Ichim (research & strategy), Bianca-Mihaela Cajvan (linguistic data & content), both Colegiul Național „Petru Rareș” Suceava; Alexandru-Eduard Bejenaru (AI & technical development), Ovidius High School, Constanța
**Website:** https://bejenaru1.github.io/zbor-lav/ · **Notebook:** https://colab.research.google.com/github/bejenaru1/zbor-lav/blob/main/Zbor.ipynb · **Code:** https://github.com/bejenaru1/zbor-lav

## The problem
Romanians mix up two "Rom-" languages. **Aromanian**, an endangered cousin of Romanian, looks familiar, so Romanians think they can read it, but many words mean something else: *zbor* means "word", not "flight". **Romani**, the language of the Roma, is unrelated to Romanian, yet slang (*mișto*, *șucar*) and manele make people think they know it. Google Translate has no Aromanian; its Romani (added 2024) translates whole sentences without explaining words or telling the two languages apart.

## What we built
A Romanian learner pastes a text. The site detects the language, then shows every word on a card with its most likely Romanian meaning and confidence (sure / check / guess). Look-alike traps get a red stamp. **Zbor** explains Aromanian; **Lav** (*lav* = "word" in Romani) explains Romani. Phrases from our sourced lists (e.g. *Tu san shukar*) get their checked meaning in a separate box, apart from the model's guesses. Everything runs in the browser.

## How it works
**Data:** 65,708 Romanian–Aromanian pairs (University of Bucharest corpus) plus 1,474 folk-tale pairs. For Romani: 7,900 Kalderash Bible verse pairs (OPUS) plus 7,157 Chergash (Vlax Romani) verses paired with a modern Romanian Bible, for training only, with every dev and test verse removed. Train/dev/test splits; test sets used once.
**Model:** IBM Model 1 word alignment learns P(Romanian word | Aromanian or Romani word). Unknown words borrow the meaning of the most similar known word (for Romani, via a simplified spelling "skeleton", since *so keres* is also written *socares*). A character n-gram naive Bayes model detects the language.
**Baseline:** "looks like Romanian" (the Romanian word spelled most alike), which is what a reader does in their head. Scoring is clipped, so a cheating "always *și*" model gets only 5%.

## Results (held-out test data, % of words right)
| | Looks like Romanian | Ours |
|---|---|---|
| Aromanian sentences (Zbor) | 22.5% | **52.5%** |
| Everyday Aromanian, 55 phrasebook items | 22.7% | **60.8%** |
| Romani Bible verses (Lav) | 6.7% | **39.1%** |
| Everyday Romani as typed online, 38 items | 3.0% | **43.3%** |
| Romani words known from songs, 12 items | 4.8% | **42.9%** |

Language detection: 96.8% (Aromanian), 100% (Romani), 95.4% (Romanian) of test sentences. Green ("sure") words are right 84% of the time for Zbor and 80% for Lav.
**What we learned:** our first metric didn't clip, and "always *și*" beat our model. A second Romani Bible raised everyday Romani from 35.8% to 43.3%, and a position prior (as in fast_align) added about half a point everywhere. Removing 579 pairs our data checker flagged did not help. We chose every setting on dev and dropped ideas that hurt it, even when they helped a test set.
**Where it fails:** old, religious training text, so slang is often wrong (*Socares* → "înveți" instead of "ce faci"). Lav is rarely "sure" (about 1 word in 10). One meaning per word, no context. No native speaker has checked our 177 possible traps yet.

## What we'd do next
Have Aromanian and Romani speakers check the traps and meanings, and add modern text (news, songs, with permission).

## Sources
Aromanian corpus: huggingface.co/datasets/aronlp/aromanian-romanian-MT-corpus-limited (CC BY-NC 4.0; Petrariu & Nisioi 2024; Jerpelea et al. 2025). Folk tales: github.com/senisioi/aromanian. Romani: opus.nlpl.eu bible-uedin (CC0; Christodoulopoulos & Steedman 2015); Chergash NT © 2018 Pioneers (CC BY-SA 4.0) and Biblia Liberă (public domain), ebible.org. AroTranslate: huggingface.co/aronlp/NLLB-rup-ron-eng-ct2. IBM Model 1: Brown et al. 1993. Google Translate languages: support.google.com/translate/answer/15139004. Test-phrase sources are listed line by line in the notebook. Libraries: pandas, NumPy, rapidfuzz, sacrebleu, CTranslate2. **AI tools:** Claude (Anthropic) helped us research data, write and debug code and draft text. We ran every step ourselves and can explain each part.
