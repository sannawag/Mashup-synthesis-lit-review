# Mashup-synthesis-lit-review
Literary review mashup, also called concatenative sound synthesis, related to Performance-view project

### Bob L. Sturm: adaptive concatenative sound synthesis and its application to micromontage composition (2006)
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

###Improvasher: A Real-Time Mashup System for Live Musical Input. (inproceedings) Davies, Matthew EP and Stark, Adam M and Gouyon, Fabien and Goto, Masataka
The goal of this paper is related to CSS, but somewhat different: it is about creating beat-level mashups that accompany a given input piece. Smooth concatenation is done via 10ms crossfading.

###The Caterpillar System for Data-Driven Concatenative Sound Synthesis, Diemo Schwarz (2005)

This paper uses the Viterbi algorithm to concatenate sound units, and uses a similarity measure to give a score for both sequence and segment. However, each unit is half of a note, so there are some additional features of a different (e.g. ADSR). 

Sequence and segment scores are calculated using a sum of weighted feature costs. The segment scores have different options, depending on whether much change is expected (e.g. onset), or not (e.g. sustain).

A database is used for the units, which are organized by "category descriptors (e.g. violin → strings → instrument)", "static descriptors (e.g. Midi note number)", and "dynamic descriptors (e.g. fundamental frequency).

###Schwarz, Diemo, and Benjamin Hackbarth. "Navigating variation: composing for audio mosaicing." International Computer Music Conference (ICMC). 2012.

This more recently published paper describes a system that lets a composer interact more directly with the unit selection process.

###TIMBRE REMAPPING THROUGH A REGRESSION-TREE TECHNIQUE, Dan Stowell and Mark D. Plumbley, Centre for Digital Music, Queen Mary University of London, UK (2010)

"We consider the task of inferring associations between two differently-distributed and unlabelled sets of timbre data."

"The core concept is to recursively partition the dataset, at each step splitting it into two subsets using a threshold on one of the independent variables (i.e. a splitting hyperplane orthogo- nal to one axis). The choice of split at each step is made to minimise an “impurity” criterion for the value of the re- sponse variable in the subsets, often based on the mean squared error...We will develop an existing unsupervised application of regression trees for this task."

"at each step of the recursion the data coming from the two distributions are separately centred. One single principal component is then calculated from their union. The recursion therefore generates two “similar but different” trees, implementing the notion that the two datasets have similarities in struc- ture (the orientations of the splitting planes are the same) but may have differences in location at various scales (the centroids of large or small subsets of the data are allowed to differ)...we weight the calculation so as to give equal emphasis to each of the datasets"

"To perform a remapping using a XAMRT data struc- ture, one takes a data point and descends the tree, at each split centring it by subtracting CX or CY as appropriate and then deciding which side of the splitting plane it falls. When the leaf node is reached, it contains two sets of train- ing data points (a subset each of X and Y ). To choose a corresponding coordinate relating to the opposite distribu- tion, one could for example use a random datum selected from the opposite subset, or the centroid of that subset, de- pending on the application. (If the sizes of the datasets are similar then the leaf will often contain just one datum from each of the two distributions.)"

"We chose a set of 10 common acoustic timbre features: spectral power, spectral power ratio in 5 log-spaced sub- bands (50–400, 400–800, 800–1600, 1600–3200, and 3200– 6400 Hz), spectral centroid, spectral 95- and 25-percentiles and zero-crossing rate (for definitions see [26])...Grains with a very low spectral power (< 0.002) were treated as silences and discarded."

"linear crossfade between grains."

