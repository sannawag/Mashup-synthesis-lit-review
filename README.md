# Mashup-synthesis-lit-review
Literary review mashup, also called concatenative sound synthesis, related to Performance-view project

# Concatenative Synthesis demonstrations found Online
- [Synful, Lindemann, 2007](http://synful.com/SoundExamples.htm)
- [Schwarz CataRT, 2007](https://www.youtube.com/watch?v=IDgKqloa6ic)
- Xavier Serra: could not find an example of his own synthesis
- [Vocaloid:](https://www.youtube.com/watch?v=qASbgvulDSc) 8:00 

# Articles

###[Maestre, Esteban, et al. "Expressive concatenative synthesis by reusing samples from real performance recordings." Computer Music Journal 33.4 (2009): 23-42.](http://www.mitpressjournals.org/doi/pdf/10.1162/comj.2009.33.4.23)

- Serra et al. previously designed Vocaloid and are now doing something similar for instruments
- Note-by-note concatenative synthesis
- Database of four jazz standards played by a professional saxophonist at eleven different tempi around the nominal one
- 1.5 hours of recording, 5000 notes
- The following features are computed:

**Melodic and musical description**
- Parsing of recording to compute MIDi pitches, onsets, durations
- Automatic generation of 3 Narmour structures per note: based on concept that melodic patterns or grops can be identified that either satisfy or violate the implication as predicted by the principles

**Intra-Note and Transition Features**
- Energy envelope contour and curvature (one value per frame) are used to compute:
- Attack, release or Attack, sustain, release: linear segments (decay is characterized as sustain with various slopes)
- For each intra-note segment, describe duration (absolute and relative to note duration), start and end times, initial and final energy values (absolute and relative to note maximum), ans slope.
- Also extract from the sustain: spectral centroid and spectral tilt.
- Compute note detachment using a formula which looks at energy envelope minimum position and compares amplitude curvature around it to the curve representing the smoothest case of articulation. Legato descriptor between 0 and 1.
- Pitch contours are considered to have a 3-part linear structure

**Note classification**
- Four different articulation classes: SIL-n-SIL, SIL-n-NOTE, NOTE-n-SIL, NOTE-n-NOTE: will be a strict matching constraint
- Four each of the four categories, divide notes into clusters (which provide amplitude and timbre) based on 6 features: attack level, sustain duration (relative), sustain slope, spectral centroid, spectral tilt. 
- Annotate notes for consolidations (agglomeration of notes), fragmentations, and ornamentations
- Then, Expressive Performance is modeled as follows:

**Training data** 
- Each note in the musical score is characterized by a set of features which describe its context: pitch, duration, metrical strength, relative pitch, duration of neighboring notes, current note's Narmour structures
- Also, intra-note features are computed: attact level, sustain relative duration, sustain slope, legato from left, legato to right, mean energy, spectral centroid, spectral tilt

**Training**
- Tilde's inductive algorithm used to predict expressiveness

**Note-Level prediction**
- duration transformation: percentage of note score duration
- onset deviation: fraction of a quarter note
- energy variation: percentage of average energy value from full database
- note alterations: consolidation, fragmentation, ornamentation, none

**Transition-Level Prediction**
- assign to one of the four groups (e.g. SIL-n-NOTE)
- 0 to 1 value for legato

**Intra-Note Level Prediction**
- k-means clustering to all the notes in a particular articulation group using the intra-note features

Finally, a performance for a new score is computed using candidate selection and the Viterbi algorithm.
1. Generate audio sequance based rediction of the expressive performance model
2. Choose best candidates based on cost of transformations and on the concatenation

**Candidate selection**
- Pre-clustering avoids sparseness in certain areas resulting from certain set of dimensions 
- There will always be a selection of notes (retain n best candidates). The remaining features are the ones that can be transformed

**Computation of costs**
- Time stretching for ASR sections, frequency transposition, energy transformation
- Concatenation: legato cost, interval cost, continuity cost (interpolating surrounding frames)

**Final concatenation**
- smooth discontinuities between end of previous note and beginning of current with respect to amplitude, pitch and timbre

###[Vocaloid](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.455.9800&rep=rep1&type=pdf) 
- Commercial Yamaha program used by Goto for synthesis)
- The samples must include all possible combinations of phonemes of the target language. In English case, all possible combinations of C-V, V-C, V-V are recorded, processed, and put into the Library. The developer can optionally add polyphones with more than two phonemes. 
- Sustained vowels are also put into the Library. They are used to reproduce the behavior of sustained vowels, which are essential in singing synthesis. 
- **The number of samples is approximately 2000 per one pitch**. In order to record these samples effectively, a special script is designed. After a recording is done, the recorded wave files are semi-automatically segmented and necessary segments are extracted. 
- The problem in concatenating samples is that the samples are recorded in different pitches and different phonetic contexts, i.e. the **pitch must be converted** to a desired one, and the timbre must be “smoothed” around the junction of samples. 
- p. 2: pitch conversion via: **spectral smoothing**: divide power spectrum into regions, each of which is scaled by a given factor, keeping the local spectral shape
- Phase is also adjusted
- The timbre of a sustained vowel is generated by **interpolating spectral envelopes** of the surrounding samples. 

### [Sample-Based Singing Voice Synthesizer By Spectral Concatenationm Jordi & Bonada, 2003](https://www.researchgate.net/profile/Jordi_Bonada/publication/2478088_Sample-Based_Singing_Voice_Synthesizer_By_Spectral_Concatenation/links/0912f510beb32ef582000000.pdf) 
- Goes into some additional details about the concatenation
-	EpR (Excitation plus Resonances) source/filter approach to Voice Model
-	Singer database (much like Vocaloid. Databases hold both phonetic and expression information about the singer)
-	Phonetic database: contains steady-states and articulations at different pitches
-	Expression database: phoneme independent musically meaningful classification of vibratos and note templates, which model attacks, releases and note transitions at different pitches.
-	Ability to change “breathiness”, roughness and other such characteristics
-	Transformation: Spectral Peak Processing used for transposition, phase correction, equalization (timbre adjustment to envelope), phase vocoding, spectral interpolation

###[Bonada, Jordi, and Xavier Serra. "Synthesis of the singing voice by performance sampling and spectral models." IEEE signal processing magazine 24.2 (2007): 67-79.](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.354.155&rep=rep1&type=pdf)
- **Transformation model**
- EpR (Excitation plus Resonances) source/filter approach to Voice Model:
  - 3 filters in cascade
    - Source filter response with exponential curve plus one resonance
    - Vocal tract: vector of resonances which emulate voice formants
    - Difference between two previous filters and harmonic envelope
- Transformation technique: Phase-Locked Vocoder
  - Segment spectrum into regions
  - Each is represented and controlled by harmonic spectral peak
  - Modifications to amp, freq, phase are applied uniformly to all bins within a region
  - Developed method to separate voice pulses from the harmonic phases to avoid phasiness and roughness (?)
  - Developed VPM to apply transformations such as creakiness, growling by adding and modifying subharmonics
    - Allows decomposition of voice into three components which can be independently modified: harmonics, noise, transients
  - In the process, breathy and noisy sounds are stored untransformed (in residual) and can be added back to the sound
- The main characteristics which are determined by the Performer Model are the tempo, the deviation of note duration from the standard value, the vibrato occurrences and characteristics, the loudness of each note, and how notes are attacked, connected and released in terms of musical articulation (e.g. legato, staccato, etc.)
- High-level expression is not addressed
- **Database Classification**
- 521 combinations of the 29 possible Spanish allophones are sufficient
- A: set of all samples used in synthesis. Grouped by pitch (can allow transp +/- 6 semitones), 4 loudness levels, 2 articulations, 2 temp contexts (12 groups in total)
- B: set of vibratos, used as templates for modifying (flat) samples in A
  - EpR (gain, slope, slope depth)
  - pitch variations relative to their slowly varying mean
  - set of marks pointing the beginning of each vibrato cycle and used as anchor points for transformations (for instance time-scaling can be achieved by repeating and interpolating vibrato cycles) and for estimations (for example vibrato rate would be the inverse of the duration of one cycle).
  - attack, sustain and release sections
  - EpR voice model ensures that the harmonics will follow the timbre envelope defined by the formants while varying their frequency
- C: set of articulations: note attacks, transitions, releases
- **Forming the Database**
- Automated much of the segmentation process
- In our recording scripts we set tempo, pitch and loudness to be constant along each sentence. 
- want to capture loudness and pitch variations inherent to phonetic articulations (see Figure 16), and make them independent of the ones related to musical performance. Another reason is that we want to constrain the singer’s voice quality and expression to ensure a maximal consistency between different samples among the database, intending to help hiding the fact that the system is concatenating samples and increasing the sensation of a continuous flow.
- **Result**
- If we restricted our view to the sonic space we deal with, we would reach the conclusion that transformed samples do connect perfectly. However, this is not true, because the actual sonic space of the singing voice is much richer and complex than our approximation. Thus, transformed samples almost never connect perfectly. Many voice features are not described precisely by the coordinates in A subspace, and others such as voice phonation modes are just ignored.

###[TIMBRE REMAPPING THROUGH A REGRESSION-TREE TECHNIQUE, Dan Stowell and Mark D. Plumbley, Centre for Digital Music, Queen Mary University of London, UK (2010)](http://smcnetwork.org/files/proceedings/2010/7.pdf)

"We consider the task of inferring associations between two differently-distributed and unlabelled sets of timbre data."

"The core concept is to recursively partition the dataset, at each step splitting it into two subsets using a threshold on one of the independent variables (i.e. a splitting hyperplane orthogo- nal to one axis). The choice of split at each step is made to minimise an “impurity” criterion for the value of the re- sponse variable in the subsets, often based on the mean squared error...We will develop an existing unsupervised application of regression trees for this task."

"at each step of the recursion the data coming from the two distributions are separately centred. One single principal component is then calculated from their union. The recursion therefore generates two “similar but different” trees, implementing the notion that the two datasets have similarities in struc- ture (the orientations of the splitting planes are the same) but may have differences in location at various scales (the centroids of large or small subsets of the data are allowed to differ)...we weight the calculation so as to give equal emphasis to each of the datasets"

"To perform a remapping using a XAMRT data struc- ture, one takes a data point and descends the tree, at each split centring it by subtracting CX or CY as appropriate and then deciding which side of the splitting plane it falls. When the leaf node is reached, it contains two sets of train- ing data points (a subset each of X and Y ). To choose a corresponding coordinate relating to the opposite distribu- tion, one could for example use a random datum selected from the opposite subset, or the centroid of that subset, de- pending on the application. (If the sizes of the datasets are similar then the leaf will often contain just one datum from each of the two distributions.)"

"We chose a set of 10 common acoustic timbre features: spectral power, spectral power ratio in 5 log-spaced sub- bands (50–400, 400–800, 800–1600, 1600–3200, and 3200– 6400 Hz), spectral centroid, spectral 95- and 25-percentiles and zero-crossing rate (for definitions see [26])...Grains with a very low spectral power (< 0.002) were treated as silences and discarded."

"linear crossfade between grains."

### Lindemann, Synful
- Description by Serra
- "Reconstructive phrase synthesis (RPM)
- Blend of functional additive synthesis and phrase-oriented parametric concatenative synthesis that can be used both off-line from a score, and real-time from MIDI performance controls
- Slow-varying harmonic componenents are directly predicted from the input score or controls via spectral nonlinear prediction based on neural networks."

### Ramirez et al. (2008) 
- "Explore and compare different machine-learning techniques for inductin both an interpretable expressive performance model and a generative one" (Serra)

### Canazza et al. (2004)
- "Modify the expressive content of a performance in a gradual way among different moods. They use a linar model to carry out the alterations based on previous segmentation, and they modify the melodies at both the symbolic and audio-signal levels." (Serra)

### Dannenberg, Pellerin, Derenyi (1998)
- "Study trumpet performance by computing amplitude descriptors." (Serra) "Statistical analysis techiniques used for analyzing trumpet envelopes led the authors to find significant envelope groupings."

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


##To check later

###definitely

[PDF] Cross-associating unlabelled timbre distributions to create expressive musical mappings.
D Stowell, MD Plumbley - WAPA, 2010 - jmlr.org

The sound space as musical instrument: Playing corpus-based concatenative synthesis
D Schwarz - New Interfaces for Musical Expression (NIME), 2012 - hal.archives-ouvertes.fr

VOICE-CONTROLLED INTERFACE FOR DIGITAL MUSICAL INSTRUMENTS
S Fasciani - 2014 - scholarbank.nus.edu.sg

[HTML] Interacting with a Corpus of Sounds
D Schwarz - SI13: NTU/ADM Symposium on Sound and Interactivity, 2013 - econtact.ca

###If there is time

[13] J.-J. Aucouturier and F. Pachet, “Improving timbre similarity: how high’s the sky?,” Journal of Negative Results in Speech and Audio Sciences, vol. 1, no. 1, 2004.

[26] G. Peeters, “A large set of audio features for sound de- scription,” tech. rep., IRCAM, 2004.

[17] J. Wouters and M. W. Macon, “A perceptual evalua- tion of distance measures for concatenative speech syn- thesis,” in Proceedings of ICSLP’98, vol. 6, (Sydney), pp. 2747–2750, Nov 1998.

