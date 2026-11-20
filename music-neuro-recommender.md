# Music That Induces a Chosen State, Tuned to the Listener's Brain

## The Idea

Certain moments in certain tracks hit the brain's wiring in a particular way: chills, a lift, a calm, a pull to replay. Everyone's wiring is different, so what works has a long tail. Genre tags and "people who liked X also liked Y" miss it.

The service takes a **target state** and finds music that moves *this* listener there:

- **happiness / uplift**
- **sadness** (catharsis, melancholy, a good cry)
- **sleepiness** (wind down, fall asleep)
- **sexual arousal** (mood, intimacy)
- possibly also focus, energy for a workout, calm

The request is "make me feel X", not "play me a rock song". Recommend by what a fragment *does* to a brain.

1. **Split each track into fragments** (a few seconds to a bar or two).
2. **Describe each fragment with signal features:** FFT/spectrogram, band energies (bass, mids, highs), onset and rhythm structure, tempo and its changes, loudness dynamics (builds, drops), harmonic movement.
3. **Predict the effect of each fragment per state:** a score for "pushes toward calm", "toward arousal", "toward sadness" and so on, via circuits such as auditory cortex, beat and motor timing, prediction and surprise, reward. This is a model, not a measurement.
4. **Learn each listener's response profile** from what they replay, skip, rate, report, or show through a sensor. The same fragment can calm one person and wind up another.
5. **Pick a path, not one song.** Choose and order fragments that move the listener from the current state toward the target, and re-plan from feedback. Sleep means slowing tempo and loudness over time; arousal means building.
6. **Find similar fragments** in the catalogue by predicted effect, not by genre, so long-tail passages surface.

## What exists (web search, 2026-11)

I read only search summaries and abstracts, not the full papers.

- **Closed loop with EEG.** A [chill brain-music interface](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12809743/) ([bioRxiv preprint](https://www.biorxiv.org/content/10.1101/2024.11.07.621657.full.pdf), [press summary](https://neurosciencenews.com/musical-chills-brain-interface-30146/)) picks songs from in-ear EEG. Its playlists produced more chills and higher pleasure than playlists tuned to lower pleasure, and beat acoustics-only recommendation, which is what commercial services resemble. One state (chills), one sensor.
- **Audio features alone are not enough.** A [Zenodo paper](https://zenodo.org/record/14877461/files/000092.pdf) found EEG stimulus-response correlations added to audio features improved prediction of familiarity. Audio features missed part of the listener's response.
- **Feature to brain correlation tracks enjoyment.** A [TU Delft study](https://repository.tudelft.nl/record/uuid:2a8e1693-e4b6-442e-86d7-25dae7896b27) uses canonical correlation analysis to find music features that covary with brain signals. Stronger correlation went with more enjoyment.
- **Audio embeddings to fMRI.** An [arXiv paper](https://arxiv.org/pdf/2406.15537) uses CLAP audio embeddings and an fMRI set of 540 clips from five participants, with encoding and retrieval models that identify which clip produced a given response.
- **Individual differences are real.** An [fMRI study](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11318860/) of 49 participants links auditory-reward connectivity to predicted chill duration. A [PNAS Nexus paper](https://escholarship.org/content/qt6wr146hv/qt6wr146hv.pdf?t=snctyq) uses machine learning on trait and state measures to predict who gets chills.
- **Multimodal emotion prediction.** The [Nightingale paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12844538/) combines EEG and audio features for music therapy, and reports better emotional-response prediction than audio alone (DEAP dataset).

## Prior art: GitHub (search 2026-11; only the first row was inspected)

| Repo / paper | What it does | Relation to this idea |
|---|---|---|
| [fmri-music-encoding](https://github.com/shreepalbishnoi/fmri-music-encoding) | Course project. Ridge regression (alpha fixed at 1000) from 27 librosa features per 1.5 s (13 MFCC, 12 chroma, RMS, centroid) with 0 to 5 sample delays, to voxel-wise BOLD on OpenNeuro ds003720. One subject, one train/test split, no cross-validation. Claims best voxel r = 0.33 in auditory cortex (not verified). Test-set masking, weights not saved, no license. | Shows the basic feature-to-brain regression, but not reusable as shipped. Worth copying only the delayed-feature setup. |
| [ISMIR 2017 paper](https://archives.ismir.net/ismir2017/paper/000184.pdf) | Hybrid encoding-decoding with canonical correlation between time-varying music features and EEG; code on GitHub. | Time-resolved feature to brain mapping. No recommender. |
| [AES 2025 late-breaking paper](https://ccrma.stanford.edu/~iran/papers/Bozilovic_and_Roman_AESAIMLA_2025.pdf) | Temporal response function decoding envelope and onsets from EEG; has a repo. | Same family as above. |
| [Neuro_Spark](https://github.com/Hars7hitha/Neuro_Spark), [BRAIN-TUNE](https://github.com/Team-NeuroSpark/BRAIN-TUNE-), [eeg-emotion-music](https://github.com/Lee-Seungyoon/eeg-emotion-music) | Classify cognitive load or emotion from live EEG, then pick music (Jamendo or Spotify API). | Closest to "induce a state", but from live EEG and coarse labels, not per-fragment effect or a learned personal profile. One notes Spotify's audio-feature and recommendation endpoints are now restricted for new apps. |
| [BCI-Music-Stimulus](https://github.com/SureshKumar-Rahul/BCI-Music-Stimulus) | Tell 10 songs apart from EEG of 5 people. | Tiny, but shows the dataset scale problem. |
| [Pop Music Highlighter](https://github.com/remyhuang/pop-music-highlighter) | TensorFlow, GPL-3.0; finds emotional "keypoints" in pop songs via emotion classification. | Fragment picking (step 1) without a listener model. Usable as a baseline. |
| [ChillsDB](https://github.com/ripolleslab/chiller) | Open chills-stimulus database: 204 clips (music, film, speech). | Labelled source of chill-inducing fragments. Covers one state only. |

None of these combines fragment-level effect prediction, multiple target states and a personal profile.

## Where the gap is

- Existing work mostly needs EEG or fMRI per listener. A consumer service has none of that.
- Datasets are tiny (five fMRI participants, tens of subjects, one in the GitHub project). A model of "which wiring gets hit" cannot be trained from them alone.
- Most work targets one state (chills, pleasure, stress). A set of target states, including sleep and sexual arousal, with fragment-level control was not found.

## Practical path

- **State labels without a brain:** ask the listener ("how do you feel now / want to feel"), and use proxies: replays, skips, scrubbing back to the same spot, saves, time-stamped "that part" taps, time to fall asleep, session length.
- **Sensors as an optional tier:** phone or watch heart rate and its variability (calm and sleep), skin response (arousal, chills), movement (sleep onset). Earbuds with EEG later.
- **Features:** mel spectrogram, onset/beat tracker, and a pretrained audio embedding (CLAP-style) per fragment. FFT bands alone are the cheap baseline to beat. Tempo, loudness and spectral brightness are known levers for arousal and sleep, so they are the first features to check.
- **Profile:** each listener becomes a weighting per target state over fragment embeddings. Cluster listeners to share signal among similar wiring.
- **Planner:** order fragments along a trajectory toward the target, with smooth transitions, and adapt when the signal says it is not working.
- **Test first:** (a) does fragment-level matching beat track-level recommendation at predicting a held-out replayed passage? (b) for sleep, does a personalised sequence shorten time to sleep onset against a generic playlist? Both are cheap to measure before building a service.

## Variant: generate simple tracks, measure stress with a watch, learn across the population

Instead of guessing brain responses from audio, measure the outcome directly and let the data say which patterns work. Start with one state, stress reduction, because a smartwatch gives an objective signal for it.

**Loop**

1. **Device.** A smartwatch reads pulse (optical sensor). Derive heart rate and heart-rate variability (HRV), for example RMSSD, as the stress indicator. Higher HRV and lower heart rate at rest generally mean less stress (unsourced; standard in the HRV literature).
2. **Generate simple tracks.** AI-generated, deliberately controlled and low-dimensional: a few knobs such as tempo, key and mode, loudness envelope, spectral brightness, rhythmic density, texture (pad, piano, pulse), and any breathing-paced swell. Simple tracks make attribution possible. Rich music mixes too many variables.
3. **Session.** Baseline pulse for a few minutes, play one track for a fixed length, then post-track pulse. Optionally a one-tap "how do you feel" for a second, subjective signal.
4. **Log per session** to the cloud: the track's parameter vector, pre and post pulse metrics, time of day, motion level, and an anonymous listener id.
5. **Learn.** Estimate which parameters reduce stress, for whom, and how much. Pick the next track by a bandit or Bayesian optimisation (explore new parameter settings, exploit what has worked), as the [sleep device study](https://arxiv.org/pdf/2211.02592) did with existing audio.

**Question to answer**

- Which patterns (slow tempo, low pitch, soft attack, sparse rhythm, a particular harmonic movement) reduce stress, and is the effect from the pattern itself or from the listener's habits and the time of day?
- What share of the population responds to each pattern, and what splits responders from non-responders?
- Ultimate goal: a small library of patterns that work for a large share of people, plus a personalisation layer for the rest.

**Analysis**

- Model each session as the change in HRV and heart rate against the track parameters, with a per-listener effect and a population effect (a mixed-effects or hierarchical model). The population term answers "what works for many"; the per-listener term answers "what works for me".
- Cluster listeners by their response profile to find groups. Whether groups map to anything (age, listening habits, baseline HRV) is an open question.
- Use feature attribution on the parameter vector to say which knob moves the result, then confirm in a designed experiment that varies one knob at a time.

**Traps to design against**

- **Stress falls anyway.** Sitting still for ten minutes lowers heart rate. Include silence and neutral-noise control sessions, and randomise track order, or every track will look effective.
- **Regression to the mean.** People start a session when stressed; a high baseline tends to drop on its own. Compare against matched baseline levels.
- **Motion and posture.** Wrist optical pulse is unreliable during movement. Accept sessions only when the watch reports stillness, and drop noisy windows.
- **Entrainment is not relaxation.** Heart rate may follow musical tempo without any stress change. Check that HRV and the subjective tap agree.
- **Watch accuracy.** Consumer wrist sensors are less accurate than a chest strap for HRV (unsourced). Validate against a strap on a small group.
- **Novelty and fatigue.** A pattern's effect can fade with repeats, so track effect against how many times a person has heard it.
- **Sample size.** Individual effects are small and noisy, so many sessions per person and many people are needed before a pattern is declared effective. Pre-register the analysis plan.

**Cloud, privacy, ethics**

- Pulse and mood are health data. Anonymise, collect explicit consent, say plainly what is stored, and allow deletion. Check the rules that apply (for example GDPR in Europe, HIPAA-like rules in the US if health claims are made).
- Avoid medical claims ("treats anxiety") without evidence. Frame it as a relaxation tool, and show the user their own data.
- A user whose stress rises during a track should be able to stop it, and the system should treat a rise as a negative reward.

**Related work (search 2026-11, summaries only)**

- [HeartDJ](https://digitalcommons.dartmouth.edu/cgi/viewcontent.cgi?article=1224&context=masters_theses) updates the generation prompt after each song from HRV and reports that AI music without biofeedback may raise stress.
- [CAT](https://arxiv.org/pdf/2505.09872) generates relaxation music from context and stress level; its user study found stress reduction.
- [Moodify](https://www.mdpi.com/2076-3417/12/21/11209) uses reinforcement learning toward a target emotion with per-session feedback, on existing tracks.
- The [sleep device study](https://arxiv.org/pdf/2211.02592) uses a bandit over audio content with a physiological reward.
- Not found: a study that pools generated-track parameters and watch HRV across a large population to learn which patterns work for many people. That is the new part here.

## Open questions

- Does a fragment's effect survive without context (the build-up before the drop)? Window size matters.
- Sad music can feel pleasant or depressing depending on the person and the moment. Is the target "sad" or "moved"?
- Novelty: the response to a passage fades with familiarity, so the profile must drift.
- Safety and consent: a service that steers mood, sleep and sexual arousal needs clear user control, a way to stop, and care around vulnerable listeners, such as someone depressed asking for sadness.
- Privacy: listening behaviour, and especially physiological signals and intimate-state requests, are sensitive data.
