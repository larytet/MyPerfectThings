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

**Related work (search 2026-11, summaries only, details unverified)**

Generated music and stress:

- [HeartDJ thesis](https://digitalcommons.dartmouth.edu/masters_theses/205/): mixed. A significant RMSSD rise (p = 0.0277) in preliminary analyses, but in a later phase the condition with four AI-generated tracks showed a significant HRV decrease. Listeners found the AI tracks emotionally thin. It suggests AI music without biofeedback may raise stress.
- [Context-AI Tunes](https://arxiv.org/pdf/2505.09872): generated music beat pre-selected relaxing music at reducing self-reported stress. No watch.
- A [Frontiers AI-music paper](https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2025.1669029/pdf) reports anxiety effects, called preliminary by its authors.
- A 500-student, 12-week trial is cited in a [critical review](https://pmc.ncbi.nlm.nih.gov/articles/PMC13740824) with HRV support. The primary paper was not found and randomisation is unconfirmed.
- [NCT07359950](https://clinicaltrials.gov/study/NCT07359950): registered trial of music with AI voice guidance, HRV measured, no results yet.

Wearable pulse in a closed loop:

- [EarStreAM](https://arxiv.org/html/2609.19127v1): earable detects stress from pulse and starts an LLM-generated meditation. A demo, not a user study.
- [Smartwatch haptic biofeedback](https://arxiv.org/abs/2507.02432): vibration timed slightly slower than live heart rate; first study found a heart-rate drop. Vibration, not music.
- [Wearable Music2Emotion](https://arxiv.org/html/2508.04723): assesses emotion from AI-generated music with EEG, fNIRS and PPG; not closed loop.
- Endel uses watch heart rate, activity, time and weather. A [hobby project](https://dev.to/arlejtech/i-built-a-desktop-app-that-reads-your-hrv-sleep-data-and-generates-a-unique-therapeutic-p7p) turns Amazfit HRV and sleep data into a daily soundscape. No GitHub repo pairing generative music with Apple Watch or Garmin data was found.

Learning from feedback (existing tracks, not generated):

- [Moodify](https://www.mdpi.com/2076-3417/12/21/11209): reinforcement learning toward a target emotion with per-session feedback.
- [Sleep device study](https://arxiv.org/pdf/2211.02592): bandit over audio content with a physiological reward.

Which patterns work (general music):

- [Stress meta-analysis](https://pubmed.ncbi.nlm.nih.gov/31167611/): 104 randomised trials; physiological d = 0.38, psychological d = 0.55; larger effect on heart rate than blood pressure or hormones.
- [2026 HRV review](https://pmc.ncbi.nlm.nih.gov/articles/PMC12976007): 24 randomised trials, 1,295 people; relaxing music raised the high-frequency HRV share, with largest gains in people with stress, anxiety or sleep problems.
- Tempo: a [Tilburg trial](https://research.tilburguniversity.edu/en/publications/classical-beats-and-white-noise-unveiling-the-effect-of-different/) found slow classical music gave higher RMSSD than electronic or personal music, only at slow tempo. A [2017 study](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5718605/) linked slow tempo to lower heart rate and fast tempo to more sympathetic activity. No meta-analysis isolating tempo was found; preference, genre and mood also matter.

Not found: a study that pools generated-track parameters and watch HRV across a large population to learn which patterns work for many people. That is the new part here.

Design consequence: the HeartDJ decrease means control sessions need silence and human-made calm tracks as comparisons, not only generated tracks against each other. Slow tempo is the best-supported first knob to vary.

## Use case: long-haul driver, focused and relaxed

A truck or coach driver on a six to ten hour shift has two opposing problems: drifting into drowsiness on monotonous road, and building up tension and stress from traffic, schedule pressure and fatigue. The target state is **alert and calm**, which is neither "wake up" nor "relax". Music is already on in the cab, so it costs the driver nothing extra.

**What the system does**

- **Reads state** from the driver's smartwatch pulse (heart rate and HRV), optionally steering-wheel grip or lane-keeping data from the vehicle, time on the road, and time of day. Rising heart rate with falling HRV suggests tension; a slow heart rate with drifting HRV can suggest drowsiness (unsourced; needs validation on drivers).
- **Chooses a direction** per moment: if drowsy, add gentle activation (somewhat faster tempo, more rhythmic and spectral movement, melodic change); if tense, lower tempo and density, soften attacks, calm harmonic movement; if in the target band, hold steady and avoid surprises.
- **Plans over the shift**, not per track: alertness dips at predictable times (the early afternoon, the small hours, after long monotonous stretches), so schedule stimulation ahead of the dip and relaxation after stressful stretches.
- **Learns per driver** which patterns hold them in the target band, using the same generate, measure, learn loop as in the stress variant, and pools results across drivers to find patterns that work for many.

**Why this fits the idea**

- Both signals are in the pulse and the driving context, so no brain scanner is needed.
- The shift gives many hours of data per driver and a natural before/after structure.
- A fleet is a ready population for finding which patterns work for a significant share of drivers, and one operator can run controlled comparisons.

**Hard problems specific to driving**

- **Safety comes first.** Music must never mask sirens, horns or engine and tyre sounds, never grab attention, and never produce sudden changes. Loudness limits and a hard cap on surprise are requirements.
- **Do not hide fatigue.** Music that keeps a drowsy driver feeling awake can delay the decision to stop. The system should treat music as a minor aid, and when pulse and driving data say fatigue is high, recommend a break instead of playing more upbeat music. Check what the regulations say about driver working hours and fatigue management in the target market.
- **"Relaxed" can mean "sleepy".** Calming a tense driver can tip into drowsiness, so the system needs a drowsiness signal as well as a stress signal, and must not use the sleep-inducing patterns from the sleep variant.
- **Measurement noise.** Wrist pulse is affected by gripping the wheel, vibration and arm movement. Rely on trends over minutes, and consider a chest strap, a seat sensor or a camera-based driver monitor as sturdier signals.
- **Outcome measure.** Heart rate and HRV are indirect. Better outcomes are lane drifts, reaction time on a short check, microsleep events, and the driver's own rating, measured in a driving simulator before any road trial.
- **Ethics and labour.** A system that monitors a driver's body for an employer can become surveillance. Keep the data with the driver by default, share only aggregates with the fleet, and get explicit consent.
- **Existing work:** driver fatigue detection from pulse and from cameras is an established field, and in-car music systems exist, but I have not searched for work that combines generated music with driver state. That search is still to do.

**First experiment:** a driving simulator with a monotonous highway task, 60 to 90 minutes, comparing silence, a fixed playlist, and adaptive generated music. Measure lane variance, reaction time, pulse and HRV, and self-rated alertness and tension.

## Use case: psychology and psychiatry, working with autistic children

A therapist, psychologist or child psychiatrist works with autistic children whose sensory profiles differ sharply from one child to the next. Some are distressed by sounds that others ignore; some use music to self-regulate; some avoid it entirely. Many cannot say how they feel in words. That is the "long tail of wiring" problem in its most acute form, and the one place where a per-child model and objective signals matter most. This is a tool *for the clinician and the family*, not a replacement for therapy.

**What the system could do**

- **Find a safe, calming sound palette for one child.** Start with very simple generated sounds (a single timbre, narrow pitch range, soft attack, slow and predictable rhythm) and vary one parameter at a time. Watch pulse and electrodermal response (skin sweat) and the child's behaviour. Learn which sound envelope, pitch register, tempo and source are calming, neutral or aversive for this child.
- **Detect distress early.** Rising heart rate and skin response can flag anxiety or sensory overload before it shows in behaviour. The system lowers intensity, simplifies or stops the sound, and alerts the adult.
- **Support regulation and transitions.** Pre-agreed calming music for known hard moments (arriving at school, a change of activity, bedtime), with the child's own response deciding the pattern.
- **Give the clinician data.** Per-session logs of which sound patterns calmed or disturbed the child, which can feed the therapist's own judgement and the family conversation.
- **Population learning, carefully.** Pooled and consented data may show which patterns calm many autistic children, and which sound features are commonly aversive. Autism is a spectrum, so group averages must not override the individual profile.

**What exists (search 2026-11, summaries only)**

- **Music therapy evidence.** A [2022 meta-analysis](https://pubmed.ncbi.nlm.nih.gov/36276324/) concludes music therapy improves social skills in autistic children, though whether the effect lasts is unclear. A [2024 meta-analysis](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11106491/) of randomised trials (1,457 children) reports gains in language communication and social skills, with high heterogeneity (I2 = 80% for language). A [2025 trial review](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12034304/) looks at what shapes the effect. The reviews I saw did not report anxiety as a main outcome, so anxiety reduction by music is an evidence gap here.
- **Wearable anxiety detection.** The [Anxiety Meter](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8591877/) shows heart-rate-derived anxiety level; in a pilot randomised trial (28 children) the feedback was associated with more deep-breathing attempts. Researchers on biomusic note that [separating anxiety from excitement](https://www.smithsonianmag.com/innovation/can-biomusic-offer-kids-autism-new-way-communicate-180968649/) is an open question, since the two share many physiological signals.
- **Sensory overload detection.** A [University of Bath project](https://researchportal.bath.ac.uk/en/projects/explore-sensory-overload-detection-with-biosensing-wearables/) explores a wearable that alerts a parent or teacher; the WPI [AuSense prototype](https://users.wpi.edu/~aadiga/docs/ausense-poster.pdf) uses personalised light, sound and heart-rate thresholds.
- **Music with a physiological trigger.** App4Autism plays music when it detects loud noise and heart-rate rise (no effectiveness evidence seen). A [WIRN 2019 study](https://iris.unitn.it/bitstream/11572/319252/1/WIRN_2019_paper_47.pdf) used sensorised garments to collect ECG during music therapy sessions while limiting sensory load.
- **Sound sensitivity and preference.** A [2022 review](https://www.frontiersin.org/articles/10.3389/fnins.2022.924806) separates hyperacusis (loudness discomfort), misophonia (irritation at specific sounds) and phonophobia (fear of sounds) and links them to autism. A small [2009 study](https://pubmed.ncbi.nlm.nih.gov/19673802/) of severely autistic adults found the same basic music preferences as controls (familiar and pleasant music preferred). A [McGill study](https://escholarship.mcgill.ca/downloads/37720j083) found similar genre variety in autistic and typically developing adolescents, with possibly different uses of music. A 2025 University of Delaware thesis notes some autistic people engage with music despite sound sensitivity while others avoid it, and highlights sound envelope, pitch register and source.
- **Not found:** a system that reads heart rate and skin response from autistic children and adapts generated music in real time, nor generative-music tools tested with autistic children. The closed loop appears largely unexplored.

**Hard problems specific to this use case**

- **Consent and assent.** Parents or guardians consent, and the child's own signals of "stop" or discomfort (pulling off a sensor, covering ears, moving away) must override the system. Many children cannot report distress, so the system must err towards stopping.
- **Sensors on a sensitive child.** A wrist or finger sensor can itself be aversive, and some children will remove it. A soft garment, ring or bracelet option, and gradual habituation, matter. Movement and stimming create noise in pulse data.
- **Anxiety versus excitement.** Heart rate and skin response rise in both, so use the child's behaviour and the caregiver's tag as additional signals, and prefer individual baselines over fixed thresholds.
- **Do not train distress.** Exploration (trying new sounds to learn what works) must never expose the child to loud, sudden or known-aversive sound. Start from known-safe sounds, change one small step at a time, and set hard loudness caps.
- **Spectrum, not average.** Population findings must not be used as norms or as a standard for what an autistic child "should" like. Personal profile first.
- **Clinical claims.** Do not claim to treat autism or anxiety. Position it as a calming aid and a data source for the clinician, and run any outcome claims through proper trials with ethics approval. Sensitive health data of children has the strictest privacy rules (for example GDPR for children, HIPAA and COPPA in the US); check what applies.
- **Neurodiversity view.** Many autistic people object to interventions that aim to remove autistic traits. Involve autistic adults and families in the design, and aim the tool at comfort and regulation chosen by the child and family, not at making the child behave less autistically.
- **Outcome measures.** Beyond pulse: caregiver and clinician ratings, standard anxiety and sensory questionnaires, frequency and duration of meltdowns, sleep, and the child's own choices to use or avoid the sound.

**First study:** a small within-child pilot, with a clinic and consenting families: baseline silence, a fixed calm playlist, and an adaptive generated palette, in short sessions in random order. Measure pulse, skin response, caregiver-rated comfort, and the child's behaviour.

## Dopamine and music: the mechanism behind "hits the wiring"

Music reward has a measurable chemical basis. This section records the evidence (search 2026-11, summaries only) and what it means for the design.

**Evidence**

- **Dopamine is released while listening (imaging).** [Salimpoor et al., 2011](https://www.zlab.mcgill.ca/publications/docs/salimpoor_2011_nn.pdf) used PET with raclopride, a tracer that binds D2 dopamine receptors and is displaced by dopamine, on 8 volunteers who reliably get chills from certain pieces. Dopamine release in the striatum rose during chills. It occurred in two places at two times: the dorsal striatum (caudate) during the roughly 15 seconds of anticipation before the climax, and the ventral striatum (nucleus accumbens) at the peak itself. Favourite music displaced more tracer than neutral music. The music was instrumental, so voices are not required. Chill intensity tracked heart rate, breathing and skin response. Caveats: n = 8, and the claim that people without chills show the same effect comes from a press interview, not the paper's data.
- **Dopamine is causal for music pleasure (drug study).** [Ferreri et al., 2019, PNAS](https://pubmed.ncbi.nlm.nih.gov/30670642/) gave 27 healthy people levodopa (raises dopamine), risperidone (blocks it) and placebo, double-blind and within subject. Levodopa raised music pleasure and motivation, including willingness to pay; risperidone lowered both. Chills and skin response were indirect measures, so the neurochemical reading needs some caution. Naltrexone (an opioid blocker) did not appear in the results I saw, so the opioid side is unchecked.
- **Parkinson's disease and rhythm.** Rhythmic cueing with music or a metronome helps gait in some patients, but response varies a lot between individuals. One [review](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10306373) proposes individualised cueing via mobile technology, and [individualised music-based cueing](https://www.researchgate.net/profile/Simone-Dalla-Bella/publication/324783869_Individualization_of_music-based_rhythmic_auditory_cueing_in_Parkinson%27s_disease/links/5b169ef7aca272d43b7f162e/Individualization-of-music-based-rhythmic-auditory-cueing-in-Parkinson%27s_disease.pdf) is a related paper. A [2025 gait pilot](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12110284/) with 9 people found a non-significant trend (p > 0.063).
- **Not found:** work linking dopamine gene variants (for example COMT or DRD2) to music reward or to response to musical cueing.

**What it means for the design**

- **Anticipation is part of the effect.** Dopamine rises before the peak, so a fragment should be scored together with its build-up, not alone. That sets a minimum window size (tens of seconds) and favours the planner choosing sequences with tension and release over single isolated clips.
- **It fits some target states better than others.** Dopamine explains reward, pleasure, motivation and drive, so the happiness, energy and arousal states are the natural fit. Stress reduction and sleep are mostly about the autonomic nervous system (heart rate, HRV), and dopamine does not directly explain them. Do not use "dopamine" as the model for the calming use cases.
- **Chills and skin response are the cheapest proxies.** Both tracked the dopamine-linked peak in the studies above, and a watch can read skin response or heart rate. They give a per-listener reward signal without a scanner, though they are indirect.
- **Individual differences are expected.** Dopamine tone differs between people, and the drug study shows the same music lands differently when it changes. That supports a per-listener profile and a long tail of tastes. The gene-variant link is unproven.
- **Medication is a confounder and a safety flag.** People on antipsychotics (dopamine blockers) or Parkinson's drugs (dopamine boosters) may respond differently, as risperidone and levodopa did in the study. Record medication where consented, treat results from those users separately, and do not draw population conclusions that mix them in.
- **Reward-seeking risk.** A system that finds and repeats what maximises dopamine reward could drift toward compulsive use. Cap session length, avoid pushing intensity up over time, and keep the listener's wellbeing, not engagement, as the objective.
- **Do not claim to change dopamine levels.** The studies show music engages the dopamine system, not that a given track will raise or lower a person's levels in a measurable or therapeutic way. Avoid neurochemical claims in any product text.

## Taste is plastic: growing a listener's taste instead of only matching it

A recommender that treats taste as fixed will lock listeners in. Evidence says taste changes with exposure, which turns the system from a matcher into a guide. Search 2026-11, summaries only, details unverified.

**Evidence**

- **Repeated exposure builds liking.** [Krugman (1943)](https://web.colby.edu/cogblog/?p=5004): people who preferred one of two genres raised their liking of the other after repeated listening. The same effect appears for [music from an unfamiliar culture](https://par.nsf.gov/servlets/purl/10516817).
- **Connectivity changes with exposure.** A [Psychological Science study](https://www.psychologicalscience.org/journals/psychological-science/09567976231214185/) taught US and Chinese listeners melodies in a scale no culture uses. Liking grew with exposure at a rate that depended on each person's music-reward sensitivity. In fMRI, connectivity between auditory regions and medial prefrontal cortex tracked exposure and prediction error. A press summary says the link between hearing and reward strengthened for better-known pieces. The [preprint](https://www.biorxiv.org/content/10.1101/2022.06.17.496615.full.pdf) describes nine studies.
- **Training shapes the circuit.** A [2021 study](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8334552/) found Chinese-trained musicians had stronger auditory-reward connectivity for Chinese-style music than Western-trained ones. This concerns trained musicians, not ordinary listeners.
- **Limits of exposure.** Liking can level off or fall with heavy, attentive listening: [Szpunar et al.](https://sites.utm.utoronto.ca/sites/sites.utm.utoronto.ca.glenn_website/files/download/Szpunar.pdf) found an inverted U after focused listening and a steady rise after incidental listening. The role of complexity is [still debated](https://pmc.ncbi.nlm.nih.gov/articles/PMC5374342). The leading explanations are better prediction and easier processing, which are theories, not settled.
- **Structural change comes mostly from playing.** A [15-month instrumental study of young children](https://pubmed.ncbi.nlm.nih.gov/19279238/) found structural brain changes tracking motor and auditory skill gains, with a matched but non-randomised control. [Habibi et al. 2017](https://dornsife.usc.edu/brainandmusic/wp-content/uploads/sites/265/2023/10/Childhood_music_training_changes_brain_structures_Habibi_et_al._2017.pdf) reports macro- and microstructural changes in school-age children. A [longitudinal study of 7 to 9 year olds](https://pmc.ncbi.nlm.nih.gov/articles/PMC6705250) found auditory cortex structure highly stable. I found no evidence that passive listening changes brain structure; the evidence for exposure is about connectivity and reward response.
- **Explanation and context: weak evidence.** A [child study](https://www.psypost.org/past-experiences-with-classical-music-predict-a-taste-for-sophisticated-genres/) found formal lessons and past exposure predicted liking sophisticated music, but the strongest predictor was emotional activation during listening, not knowledge (correlational). An older dissertation found a music-appreciation course raised acceptance of art music. No experiment comparing adults given context with adults not given it was found. A [King's College summary](https://culturecase-os.kdl.kcl.ac.uk/research/2025/07/people-can-develop-taste-classical-music-and-opera-throughout-their-lives?format=pdf) says taste for classical music and opera can develop throughout life, while one [Thai study](https://so08.tci-thaijo.org/index.php/dhammalife/article/download/3807/3592/41726) found over half of music students did not like classical music, so familiarity alone does not guarantee liking.

**What it means for the design**

- **Graded exposure as a feature.** Beyond matching, the system can widen a listener's taste on purpose: pick a bridge from what the listener already enjoys toward a target genre (classical, a new culture's music), choosing fragments close enough to be liked and far enough to be new, and step outward as liking grows.
- **Measure the change.** Track liking and the reward proxies (chills, skin response, replays) per fragment over repeated plays, so the planner sees a taste growing and not only a taste present.
- **Avoid overexposure.** Space out repeats, prefer incidental listening to forced attentive listening, and drop a fragment when liking turns down. Pushing a track too hard can lower liking.
- **Use context carefully.** Short, optional context (who wrote it, what to listen for) is plausible but unproven; test it as an A/B arm instead of assuming it works, and watch emotional engagement as the likely mediator.
- **Playing beats listening for structure.** If the goal is a lasting brain change, a "play along" mode (rhythm taps, humming, simple instruments) is better supported than passive listening.
- **Parent and child case.** A parent introducing a child to classical music is a human version of this loop. The service could suggest a ladder of pieces and flag when to stop, but should respect the child's response and not turn it into a duty.
- **Profile must drift.** Fits the existing open question on novelty: taste changes, so a profile fitted once goes stale.
- **Filter bubble and manipulation.** A system that shapes taste has power. Make the direction visible and chosen by the listener, avoid steering toward whatever is most profitable, and let the listener turn the widening off.

## Open questions

- Does a fragment's effect survive without context (the build-up before the drop)? Window size matters.
- Sad music can feel pleasant or depressing depending on the person and the moment. Is the target "sad" or "moved"?
- Novelty: the response to a passage fades with familiarity, so the profile must drift.
- Safety and consent: a service that steers mood, sleep and sexual arousal needs clear user control, a way to stop, and care around vulnerable listeners, such as someone depressed asking for sadness.
- Privacy: listening behaviour, and especially physiological signals and intimate-state requests, are sensitive data.
