---
title: "What is G2P?"
date: 2019-04-15
---

================
* G2P refers to grapheme-to-phoneme conversion. This is the process of using rules to generate a pronunciation for a word (for creating a pronunciation dictionary). The rules are usually created by a automated statistical analysis of a pronunciation dictionary. The G2P algorithm is used to generate the most probable phone list for a word not contained in the pronunciation dictionary (i.e. out-of-vocabulary words) used to create the G2P rules.

* The process of converting a sequence of letters into a sequence of phones is called grapheme-to-phoneme conversion, sometimes shortened g2p. The job of a grapheme-to-phoneme algorithm is thus to convert a letter string like cake into a phone string like [K EY K].

* In Kaldi, we tend to use **Sequitur G2P**, which is a data-driven grapheme-to-phoneme converter developed at RWTH Aachen University - Department of Computer Science by Maximilian Bisani.