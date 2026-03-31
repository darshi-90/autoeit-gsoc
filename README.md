AutoEIT GSoC 2026 – Test I (Audio Transcription)
Overview:
In this task, I worked on generating transcriptions for Spanish Elicited Imitation Task (EIT) audio data. The main goal was to produce sentence-level transcripts while keeping the learner’s original output intact.

Approach:
I used the Whisper (medium) model since it performs well for multilingual speech, especially Spanish. To improve transcription quality, I enabled beam search during decoding.
To get more control over the output, I used whisper_timestamped which provides word-level timestamps and confidence scores.

Post-processing:
The raw Whisper output contained some noise (especially in silent or unclear segments), so I added a few filtering steps:
Removed low-confidence segments (threshold = 0.80)
Filtered out repeated tokens like “no no no” that appeared due to noise
Merged adjacent segments to form proper sentence-level outputs
Removed consecutive duplicate sentences caused by segmentation

Also one important thing was to not correct any grammatical or vocabulary errors made by the participant, since those are essential for evaluation.

Output:
The final output is stored as a CSV file with:
sentence_id
timestamps (start, end)
transcript

File: results/final_transcriptions.csv

How to run:
Install dependencies:
pip install -r requirements.txt
Run the notebook:
notebooks/test1_transcription.ipynb
Note: Audio files are not included in this repository. Please use the AutoEIT sample dataset and update the file path in the notebook accordingly.

Notes / Observations:
-Whisper sometimes produces repeated or noisy tokens in silent regions
-Segment boundaries are not always aligned with sentence boundaries
-Confidence-based filtering helped remove most of the noise

Future Improvements:
-Better sentence segmentation (possibly using alignment techniques)
-Fine-tuning ASR for learner speech
-Extending this pipeline for automated scoring (Test II)
