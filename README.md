### Project Overview

Early detection of common illnesses can drastically improve patient outcomes, yet accurate decision‑support tools are still scarce outside large hospital systems. This project translates our academic study Early Disease Detection through Machine Learning into a working, open‑source pipeline that predicts likely diseases from a free‑text list of symptoms. By fusing a richly curated symptom–disease knowledge‑base with lightweight machine‑learning models, the repository shows that high‑quality diagnostics do *not* require heavyweight neural nets or expensive hardware.

### Challenges in Tabular Data Inference

Medical symptom tables are high‑dimensional: each additional symptom creates a new binary feature, pushing the data into ever‑wider spaces. This “curse of dimensionality” leads to sparsity, over‑fitting and heavy compute loads. Our workflow tackles these issues with regularisation, careful feature selection and dimensionality reduction, ensuring the model generalises rather than memorises training noise.

### Data Acquisition & Pre‑processing

We began with Columbia University’s open symptom list, then expanded it using the National Health Portal of India and targeted Wikipedia scraping. The raw dump—over *1,300 diseases* and their symptoms—was cleaned, de‑duplicated and tokenised. A 0.75 Jaccard‑similarity threshold and WordNet synonyms collapsed near‑duplicates, yielding a concise yet comprehensive dataset fit for machine learning.

### Symptom Expansion & Feature Engineering

When a user enters symptoms, the system splits the sentence, removes stop‑words, lemmatises tokens and adds synonym expansions. Each final token is mapped onto the master symptom index to build a binary feature vector (1 = present, 0 = absent). The same pipeline vectorises the training corpus, keeping both user input and historical data in a consistent space.

### Modelling Strategy

Four classical classifiers—Logistic Regression, Random Forest, Decision Tree and Multinomial Naïve Bayes—were benchmarked with 5‑fold cross‑validation. Logistic Regression provided the best trade‑off between bias and variance, achieving ~92 % accuracy with only a two‑point drop across folds. TF‑IDF weighting and cosine similarity further refine rankings, so the API returns not just what might be wrong but why those diseases outrank others for the given symptoms.

### Evaluation & Results

Performance metrics highlight Logistic Regression’s stability (Accuracy ≈ 91.7 %, Recall ≈ 91.7 %, CV ≈ 89.2 %). Random Forest matched top‑line accuracy but lost five points under cross‑validation, signalling mild over‑fitting. Decision Trees suffered the widest generalisation gap, while Multinomial NB traded speed for precision. The current release therefore ships with pre‑trained Logistic Regression weights for dependable everyday use.

### Interactive Prototype

A Streamlit front‑end completes the loop: users type symptoms, confirm suggested matches and receive ranked disease predictions plus live‑scraped Wikipedia summaries on causes, risk factors and first‑line treatments. This demo proves the model’s practicality for clinicians, students and health‑conscious individuals alike, all from a standard laptop

### Future Directions

Next iterations will fold in demographic metadata (age, gender) and patient history to sharpen predictions, explore image‑based extensions for dermatological conditions, and offer safe over‑the‑counter remedy suggestions with clear disclaimers. Each enhancement will be driven by open issues and pull requests as we continue evolving this community‑driven diagnostic platform.
