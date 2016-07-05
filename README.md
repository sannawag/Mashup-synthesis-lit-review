# Mashup-synthesis-lit-review
Literary review mashup, also called concatenative sound synthesis, related to Performance-view project

## Bob L. Sturm: adaptive concatenative sound synthesis and its application to micromontage composition (2006)
Summary of other methods:
- ACSS: 
- Musaicing (Zils and Pachet 2001)
  - Sample: sound object with high-level descriptors attached (instrument, tempo, etc…)
  - Retrieved from library, transformed, sequenced to match target
  - Two constraints: segment and sequence. 
  - Cost measured using low-level features
  - Does not compute global minimum: non-exhaustive, adaptive search
- Real-time version: Acouturier and Pachet 2006
- Caterpillar (Schwarz 2004)
  - Dynamic time warping with a score??
  - Motivated by the promise of high-quality musical synthesis from concatenative techniques
- Both Musaicing and Caterpillar have cost formula weights set by hand
- Scrambled Hackz (Sven Konig 2006)
  - Free, open-source
  - real-time
- CSS: 
- MoSevius (Lazier and Cook 2003)
  - ‘Sound sieve’ multi-dimensional feature space: fast, real-time search
- Soundmosaic (Hazel 2003)
  - Inner product: same as audio reconstruction. No windowing or overlap, so outcome is choppy
- MATConcat
  - Open-source
  - 6 features: zero crossings, RMS, spectral centroid, spectral rolloff, harmonicity (value of second peak of normalized autocorrelation), pitch
  - ‘Sound sieve’ = weighted l1-norm?
- match feature 1 within +- 10 %, feature 2 within …, etc
  - If no match is found, extend previous match
  - Convolve database and target units
  - force the RMS of target units on corpus units

To check
- CTTS: speech synthesis is very successful

#Improvasher: A Real-Time Mashup System for Live Musical Input. (inproceedings) Davies, Matthew EP and Stark, Adam M and Gouyon, Fabien and Goto, Masataka

The goal of this paper is related to CSS, but somewhat different: it is about creating beat-level mashups that accompany a given input piece. Smooth concatenation is done via 10ms crossfading.

