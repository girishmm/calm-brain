Resource Reference
==================

The CALM-Brain resource consists of data collected from at-risk
families along multiple modalities - Magnetic Resonance Imaging,
Electroencephalography, Functional near-infrared spectroscopy, Eye
tracking, Cognition, Genomics, and Clinical assessments. This document
describes how these modalities are stored. For information on how
these were acquired, please refer to the resource publication. For
information on these can be accessed, please refer to *Almirah*
documentation.

Data in the resource can be divided into two based on their content:
tabular records, and data files. Tabular records are stored as tables
in a Relational Database Management System. Data files are stored in
various repositories in an in-house G-node Infrastructure instance
(GIN).

Clinical assessments
--------------------

Participants undergo a series of clinical assessments that aid in
understanding their background, experiences, and aid in the
diagnosis. Each assessment is stored as a table in the database *cbm*
of the Relational Database Management system. In cases, where a
questionnaire has multiple modules, each module is stored as a table
to reduce redundancy. In this setup, each record, typically
corresponds to a row in the tables. In case of repetitive questions,
there might be more than a row for each record as the tables are
normalised. The recommended way to identify a record is using a
combination of *D-number* and *Session ID*.

The list of tables and the questionnaires they map to are below:

+------------------------------------------+-------------------------------------------------------------------------------------------+
| Table name                               | Questionnaire or Table details                                                            |
+==========================================+===========================================================================================+
| subjects                                 | List of all subjects recrited.                                                            |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| assessments                              | List of asssessments performed.                                                           |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| adult_adhd_self_report_scale             | Adult ADHD self-report scale (version 1.1)                                                |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| adult_temperament                        | Adult temperament questionnaire                                                           |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| adverse_childhood_experiences            | Adverse Childhood Experiences International Questionnaire (ACE-IQ)                        |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| agoraphobia                              | M.I.N.I International Neuropsychiatric Interview (Agoraphobia module)                     |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| alchohol_abuse                           | M.I.N.I International Neuropsychiatric Interview (Alcohol Abuse module)                   |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| alchohol_dependence                      | M.I.N.I International Neuropsychiatric Interview (Alcohol Dependence module)              |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| antisocial_personality_disorder          | M.I.N.I International Neuropsychiatric Interview (Antisocial Personality Disorder module) |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| anorexia_nervosa                         | M.I.N.I International Neuropsychiatric Interview (Anorexia Nervosa module)                |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| bulimia_nervosa                          | M.I.N.I International Neuropsychiatric Interview (Bulimia Nervosa module)                 |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| clinical_global_impression               | Clinical Global Impression Scale                                                          |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| global_assessment_of_functioning         | Global Assessment of Functioning                                                          |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| hamilton_anxiety_rating                  | Hamilton Anxiety Rating Scale (HARS)                                                      |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| hamilton_depression_rating               | Hamilton Depression Rating Scale (HDRS)                                                   |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| hindi_mental_state_examination           | Hindi Mental State Examination (HMSE)                                                     |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| mental_status_assessment                 | General comments on mental status.                                                        |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| mini_ipip_scale                          | 20 Item mini-IPIP                                                                         |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| modified_kuppuswamy_socioeconomic_scale  | Socioeconomic Status Scale                                                                |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| negative_symptoms_assessment             | Schedule for Assessment of Negative Symptoms (SANS)                                       |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| obsessive_compulsive_disorder            | M.I.N.I International Neuropsychiatric Interview (Obsessive-Compulsive Disorder module)   |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| panic_disorder                           | M.I.N.I International Neuropsychiatric Interview (Panic Disorder module)                  |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| physical_examination                     | General Physical examination of subject.                                                  |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| post_traumatic_stress_disorder           | M.I.N.I International Neuropsychiatric Interview (Posttraumatic Stress Disorder module)   |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| positive_symptoms_assessment             | Schedule for Assessment of Positive Symptoms (SANS)                                       |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| recent_life_events                       | Interview for Recent Life Events (IRLE)                                                   |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| severity_of_alcohol_dependence           |                                                                                           |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| socialphobia                             | M.I.N.I International Neuropsychiatric Interview (Social Phobia module)                   |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| suicidality                              | M.I.N.I International Neuropsychiatric Interview (Suicidality module)                     |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| work_and_social_adjustment_scale         | Work and Social Adjustment Scale (WSAS)                                                   |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| yale_brown_obsessive_compulsive_scale    | Yale-Brown Obsessive Compulsive Scale (Rating module)                                     |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| yale_brown_obsessive_compulsive_symptoms | Yale-Brown Obsessive Compulsive Scale (Symptoms module)                                   |
+------------------------------------------+-------------------------------------------------------------------------------------------+
| young_mania_rating_scale                 | Young's Mania Rating Scale (YMRS)                                                         |
+------------------------------------------+-------------------------------------------------------------------------------------------+


Endophenotype data files
------------------------

Data acquired via neuroimaging (mri), electroencephalography (eeg),
functional near-infrared spectroscopy (nirs), and eye tracking
(eyetrack) are called as endophenotype data files. The raw data for
each of these modalities is encrypted and stored in the
*cbm/{modality}* GIN repository. The *{modality}* name used for each
is mentioned in brackets. The organized (anonymized and format
converted) version of the endophnotype data files is stored in the
*cbm/data* repository collectively.

Both the raw data and the organized data are stored according to the
BIDS specification.

Genetic data files
------------------

Genome sequence reads are stored in the *cbm/genome* GIN repository in
a BIDS-like specification. This has been separated from the
endophenotype data files based on standard practice.
