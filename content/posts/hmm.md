---
title: "HMM topology and transition modeling"
date: 2019-04-15
---

================
## HMM topologies

```
 <Topology>
 <TopologyEntry>
 <ForPhones> 1 2 3 4 5 6 7 8 </ForPhones>
 <State> 0 <PdfClass> 0
 <Transition> 0 0.5
 <Transition> 1 0.5
 </State>
 <State> 1 <PdfClass> 1
 <Transition> 1 0.5
 <Transition> 2 0.5
 </State>
 <State> 2 <PdfClass> 2
 <Transition> 2 0.5
 <Transition> 3 0.5
 </State>
 <State> 3
 </State>
 </TopologyEntry>
 </Topology>
```

## Pdf (probability distribution function)-classes

0 -> 0 -> 1 -> 1 -> 1 -> 2 -> 2 -> 2 -> 3

​                   |			         	 |

self_loop_pdf_class        forward_pdf_class

? If two states have the same pdf_class variable, then they will always share the same probability distribution function (p.d.f.) if they are in the same **phonetic context**.

- phone (one-based): this type of identifier is used throughout the toolkit; it can be converted to a phone name via an OpenFst symbol table. Not necessarily contiguous (the toolkit allows "skips" in the phone indices).
- hmm-state (zero-based): this is an index into something of type [HmmTopology::TopologyEntry](http://kaldi-asr.org/doc/classkaldi_1_1HmmTopology.html#aba67ff7bf4a95d8b1b33f1f41b385a74). In the normal case, it is one of {0, 1, 2}.
- pdf, or pdf-id (zero-based): this is the index of the p.d.f., as originally allocated by the decision-tree clustering; (see [PDF identifiers](http://kaldi-asr.org/doc/tree_externals.html#pdf_id)). There would normally be several thousand pdf-ids in a system.
- transition-state, or trans_state (one-based): this is an index that is defined by the [TransitionModel](http://kaldi-asr.org/doc/classkaldi_1_1TransitionModel.html) itself. Each possible triple of (phone, hmm-state, pdf) maps to a unique transition-state. Think of it is the finest granularity of HMM-state for which transitions are separately estimated.
- transition-index, or trans_index (zero-based): this is an index into the "transitions" array of type [HmmTopology::HmmState](http://kaldi-asr.org/doc/structkaldi_1_1HmmTopology_1_1HmmState.html). It numbers the transitions out of a particular transition-state.
- transition-id, or trans_id (one-based): each of these corresponds to a unique transition probability in the transition model. There is a mapping from (transition-state, transition-index) to transition-id, and vice versa.