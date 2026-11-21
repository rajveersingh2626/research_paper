# Algorithmic Influence on Political Awareness and Narratives
### How Instagram’s Engagement System Influences the Civic Understanding of the Indian Youth

[![SSRN Preprint](https://img.shields.io/badge/SSRN-5652570-blue.svg)](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5652570)
[![Zenodo DOI](https://img.shields.io/badge/Zenodo-10.5281%2Fzenodo.17434259-green.svg)](https://zenodo.org/records/17434259)
[![Paper PDF](https://img.shields.io/badge/PDF-Download%20Paper-red.svg)](./paper.pdf)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8+-yellow.svg)](https://www.python.org/)

**Authors:**  
- **Suhani Minocha**  
- **Rajveer Singh Marwah** ([GitHub](https://github.com/rajveersingh2626) &bull; [LinkedIn](https://linkedin.com/in/rajveer-singh-marwah-61195a278))

---

## Abstract

With the increasing dominance of social media platforms like Instagram in shaping youth culture and communication, algorithmic curation has become an invisible yet decisive force in determining what young citizens encounter, engage with, and believe. 

This computational social science research empirically investigates how Instagram’s algorithmic engagement mechanics differentially amplify entertainment content over political and civic discourse among Indian youth. By combining web-scraped public data, natural language processing (NLP), non-parametric statistical hypothesis testing, and econometric regression modeling, we demonstrate a structural under-prioritization of civic narratives in favor of low-friction, high-velocity entertainment media.

- **Preprint (SSRN):** [https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5652570](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5652570)
- **Preprint (Zenodo):** [https://zenodo.org/records/17434259](https://zenodo.org/records/17434259)
- **Full Text PDF:** Read directly in this repository: [`paper.pdf`](./paper.pdf)

---

## Key Empirical Findings

| Metric | Entertainment | Political / Civic | Statistical Test / Significance |
|---|---|---|---|
| **Median Engagement Score** | `5,533.86` | `117.00` | Mann–Whitney U: $p < 0.001$ |
| **Effect Size (Cliff's $\Delta$)** | — | — | **$\Delta = -0.744$** (Strong negative disparity) |
| **Negative Binomial Coeff ($\beta$)** | Ref | **$-3.3664$** | GLM IRLS: $z = -21.050$, $p < 0.001$ |
| **Flesch-Kincaid Grade Level** | `8.96` (Accessible) | `14.91` (College level) | $t = 5.42$, $p < 0.001$ |
| **Sentiment Polarity (Mean)** | `+0.117` | `+0.086` | Non-significant predictor of volume |

### Core Takeaways:
1. **Severe Engagement Asymmetry**: Political and civic posts receive orders of magnitude lower engagement than entertainment content ($5533.86$ median vs $117.00$ median), validated by a Mann-Whitney U test ($p < 0.001$) and a large effect size ($\text{Cliff's } \Delta = -0.744$).
2. **Independent Algorithmic Penalty**: Controlling for readability, emotional sentiment polarity, and text subjectivity in a Generalized Linear Model (Negative Binomial Regression), political content exhibits a statistically isolated penalty ($\beta = -3.3664, p < 0.001$).
3. **Processing Fluency & Civic Neglect**: Entertainment content is linguistically simpler (Flesch-Kincaid Grade 8.96 vs 14.91 for political discourse). The recommendation architecture structurally rewards low-friction cognitive processing, resulting in systemic neglect of civic deliberation in digital spaces.

---

## Visualizations

### 1. Engagement Distribution Across Categories
<div align="center">
  <img src="graph1_engagement_boxplot.png" alt="Engagement Boxplot by Category" width="750" />
</div>

### 2. Engagement vs. Sentiment Polarity
<div align="center">
  <img src="graph2_engagement_polarity.png" alt="Engagement vs Polarity" width="750" />
</div>

### 3. Readability & Processing Fluency (Flesch-Kincaid Grade)
<div align="center">
  <img src="graph3_engagement_readability.png" alt="Engagement vs Readability" width="750" />
</div>

### 4. Predictive Vocabulary (TF-IDF & Logistic Regression)
<div align="center">
  <img src="graph4_top_political_keywords.png" alt="Top Political Keywords" width="48%" />
  <img src="graph5_top_entertainment_keywords.png" alt="Top Entertainment Keywords" width="48%" />
</div>

---

## Methodology & Pipeline

```
Raw Instagram Post Data (15 Verified Indian Accounts)
                    │
                    ▼
          [ clean.py / clean data ]
                    │
                    ▼
    [ nlp.py: Sentiment Polarity & Readability ]
     (TextBlob, Textstat: Flesch-Kincaid)
                    │
       ┌────────────┴────────────┐
       ▼                         ▼
[ hypotest.py ]           [ model.py / ml.py ]
Mann-Whitney U Test       Negative Binomial GLM Regression
Cliff's Delta (-0.744)    TF-IDF Logistic Classifier (78% Acc)
```

1. **Data Ingestion**: Scraped over 220 public posts from 15 high-reach verified Indian media and entertainment accounts spanning news publishers (*The Wire*, *The Mojo Story*, *Youth Ki Awaaz*, *OpIndia*, *The Quint*) and youth entertainment channels (*FilterCopy*, *ScoopWhoop*, *MensXP*, *Netflix India*, *Humans of Bombay*).
2. **Text Processing & Feature Engineering** (`nlp.py`): Extracted linguistic complexity metrics (Flesch-Kincaid grade level, syllable counts) and semantic sentiment (polarity and subjectivity) from post captions.
3. **Hypothesis Testing** (`hypotest.py`): Evaluated distributional differences without normality assumptions using the non-parametric Mann-Whitney U test and Cliff's Delta effect size.
4. **Econometric GLM Regression** (`model.py`): Modeled overdispersed engagement counts using Negative Binomial Regression to assess the isolated effect of political categorization while controlling for linguistic features.
5. **Supervised Classification** (`ml.py`): Trained a TF-IDF vectorizer + Logistic Regression classifier (78% test accuracy, weighted F1: 0.75) to extract the primary lexical markers predictive of political versus entertainment categories.

---

## Repository Structure

```
.
├── paper.pdf                               # Full 27-page research paper PDF
├── clean.py                                # Data deduplication, parsing, and normalization
├── nlp.py                                  # NLP pipeline (TextBlob polarity, Textstat readability)
├── hypotest.py                             # Mann-Whitney U tests and Cliff's Delta calculations
├── model.py                                # Negative Binomial GLM regression
├── ml.py                                   # TF-IDF + Logistic Regression category classifier
├── graph.py                                # Matplotlib & Seaborn visualization generator
├── analysis_data_fully_processed.csv       # Fully processed analysis dataset
├── consolidated_data.csv                   # Raw scraped post collection
├── results_A_hypothesis_test.txt           # Hypothesis testing output
├── results_B_regression_summary.txt        # Full statsmodels GLM regression table
├── results_C_ml_report.txt                 # Classification report & top predictive tokens
├── Data/                                   # Account-level scraped CSV datasets
├── Research Items/                         # Background literature and policy references
└── Statistical research/                   # Methodological and econometric references
```

---

## Reproduction & Execution

### Prerequisites
```bash
pip install pandas numpy scipy statsmodels scikit-learn textblob textstat matplotlib seaborn
```

### Running the Analysis
```bash
# 1. Clean raw scraped datasets
python clean.py

# 2. Extract sentiment and readability features
python nlp.py

# 3. Execute Mann-Whitney U & Cliff's Delta tests
python hypotest.py

# 4. Run Negative Binomial Regression
python model.py

# 5. Train TF-IDF classifier and inspect predictive keywords
python ml.py

# 6. Generate publication plots
python graph.py
```

---

## Citation

If you reference this research, data, or methodology, please cite:

```bibtex
@article{minocha_marwah_2025,
  title={Algorithmic Influence on Political Awareness and Narratives: How Instagram’s Engagement System Influences the Civic Understanding of the Indian Youth},
  author={Minocha, Suhani and Marwah, Rajveer Singh},
  journal={SSRN Electronic Journal},
  year={2025},
  month={October},
  doi={10.2139/ssrn.5652570},
  url={https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5652570}
}
```

Or APA:

> Minocha, S., & Marwah, R. S. (2025). *Algorithmic Influence on Political Awareness and Narratives: How Instagram’s Engagement System Influences the Civic Understanding of the Indian Youth*. SSRN Electronic Journal. https://doi.org/10.2139/ssrn.5652570

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
