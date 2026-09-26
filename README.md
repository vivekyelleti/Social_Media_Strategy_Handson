# Social Media Strategy with AI: Hands-on Demonstration

## 1. Problem Statement

Organizations receive large volumes of social-media conversations across multiple platforms, products, campaigns, markets, and audience groups. Basic reporting can show the number of posts or engagements, but it does not automatically answer the strategic questions that matter:

- What are customers and prospects discussing?
- Is the conversation positive, neutral, negative, mixed, sarcastic, or context dependent?
- Which themes are driving negative or positive conversation?
- Is a negative signal concentrated around a campaign, product, platform, or market?
- Which conversations need human validation or escalation?
- What should marketing, customer service, e-commerce, or operations do next?

The objective of this hands-on exercise is to demonstrate an auditable social-listening workflow that converts raw social-media-style posts into an executive decision brief.

The analytical journey is:

1. **Listen:** Load and inspect the conversations.
2. **Validate:** Check data quality, representation, sarcasm, slang, and uncertain model outputs.
3. **Understand:** Score sentiment and identify themes using TF-IDF.
4. **Interpret:** Examine campaign, platform, product, and market patterns.
5. **Act:** Convert the strongest signal into an evidence-led recommendation.
6. **Learn:** Track changes in sentiment, complaints, engagement, and response outcomes.

## 2. Learning Objectives

After completing the demonstration, participants should be able to:

- Inspect social-media data for quality, missingness, duplicates, and representation bias.
- Apply VADER as an explainable rule-based sentiment baseline.
- Interpret VADER's compound score as a directional signal rather than objective truth.
- Identify model limitations involving sarcasm, slang, mixed sentiment, and language context.
- Use TF-IDF unigrams and bigrams to identify themes within negative conversations.
- Compare sentiment across campaigns and platforms.
- Detect a recent increase in negative conversation.
- Prepare an executive decision brief containing signal, evidence, business meaning, action, ownership, and measurement.


## 3. Dataset Overview

The participant dataset contains **1,600 synthetic social-media-style records**. Each row represents one synthetic post or comment. The data are designed for teaching and demonstration; they do not represent real customers, accounts, brands, or platform users.

The dataset includes multiple platforms, products, campaigns, markets, languages, audience types, engagement measures, and text patterns. It also includes deliberately challenging language such as sarcasm, slang, Hinglish, and mixed sentiment so that participants can evaluate the limitations of automated sentiment analysis.

## 4. Metadata: Participant Dataset Columns

### `post_id`
- **Type:** Text/string
- **Description:** Unique synthetic identifier for each post.
- **Example format:** `SM00001`
- **Use:** Duplicate detection, row tracking, and joining with the instructor key.
- **Do not use as:** An analytical feature.

### `date`
- **Type:** Date and time
- **Description:** Synthetic timestamp associated with the post.
- **Use:** Daily aggregation, trend analysis, rolling sentiment metrics, and spike detection.
- **Preparation:** Convert using `pd.to_datetime()`.

### `platform`
- **Type:** Categorical text
- **Description:** Platform on which the synthetic conversation appeared.
- **Possible values:** Instagram, LinkedIn, Reddit, YouTube, X, and Facebook.
- **Use:** Platform-volume analysis, representation-bias discussion, and platform-level sentiment comparison.
- **Caution:** Higher platform volume does not necessarily mean greater market importance.

### `text`
- **Type:** Free text
- **Description:** Synthetic social-media-style post or comment.
- **Use:** VADER sentiment scoring, human validation, TF-IDF theme discovery, and representative-excerpt selection.
- **Caution:** Preserve the original text for VADER because punctuation, capitalization, intensifiers, and negation may affect scoring. Use a separately cleaned copy for TF-IDF.

### `engagement`
- **Type:** Integer
- **Description:** Synthetic weighted engagement measure.
- **Generation logic:** `likes + 2 × comments + 3 × shares`.
- **Use:** Prioritizing posts and comparing attention across sentiment groups.
- **Caution:** Engagement measures attention, not necessarily business importance, customer value, or positive impact.

### `likes`
- **Type:** Integer
- **Description:** Synthetic number of likes or reactions.
- **Use:** Descriptive engagement analysis.

### `comments`
- **Type:** Integer
- **Description:** Synthetic number of comments or replies.
- **Use:** Conversation-depth analysis and construction of the weighted engagement variable.

### `shares`
- **Type:** Integer
- **Description:** Synthetic number of shares or reposts.
- **Use:** Amplification analysis and construction of the weighted engagement variable.

### `views`
- **Type:** Integer
- **Description:** Synthetic number of content views.
- **Use:** Reach context and engagement-rate calculation.
- **Caution:** Check for zero values before dividing engagement by views.

### `product`
- **Type:** Categorical text
- **Description:** Synthetic product referenced in the post.
- **Possible values:** NovaPhone X, AirBeat Pro, FitPulse Watch, and HomeHub Mini.
- **Use:** Product-level sentiment and theme comparison.

### `campaign`
- **Type:** Categorical text
- **Description:** Synthetic campaign associated with the conversation.
- **Possible values:** Always-on, Festival Launch, Creator Collab, Service Update, and None.
- **Use:** Campaign-level sentiment comparison and recent negative-signal detection.
- **Teaching purpose:** The data contain an embedded campaign-linked issue for participants to diagnose.

### `market`
- **Type:** Categorical text
- **Description:** Broad synthetic market or geographic grouping.
- **Possible values:** India-North, India-South, India-East, India-West, and India-Central.
- **Use:** Market-level segmentation and concentration analysis.
- **Caution:** These are synthetic broad categories and should not be treated as real demographic or geographic evidence.

### `language`
- **Type:** Categorical text
- **Description:** Language style used in the synthetic post.
- **Possible values:** English and Hinglish.
- **Use:** Language-context discussion and model-limitations analysis.
- **Caution:** A general English sentiment lexicon may not fully interpret Hinglish or context-specific language.

### `author_type`
- **Type:** Categorical text
- **Description:** Synthetic role of the account posting the conversation.
- **Possible values:** Customer, Prospect, Creator, and Community member.
- **Use:** Audience-group comparison and representation discussion.
- **Caution:** This variable is synthetic and should not be used to make judgments about real people.

### `verified_account`
- **Type:** Binary integer
- **Description:** Synthetic indicator for whether the account is marked as verified.
- **Possible values:** `1` for verified and `0` for not verified.
- **Use:** Source-context comparison.
- **Caution:** Verification is not a credibility, accuracy, expertise, or importance score.



## 5. Software Requirements

Use Python 3 with the following libraries:

```text
pandas
numpy
matplotlib
seaborn
scikit-learn
vaderSentiment
```

Install the dependencies with:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn vaderSentiment
```

For Google Colab:

```python
!pip install pandas numpy matplotlib seaborn scikit-learn vaderSentiment
```

## 6. Running the Demonstration

### Local Python

```bash
python social_media_strategy_handson_corrected.py
```

### Google Colab

Upload the Python file and the participant CSV to the Colab session, then run:

```python
%run social_media_strategy_handson_corrected.py
```

If the instructor-key file is also uploaded, the optional model-validation section will run automatically. If it is absent, the main participant demonstration will still run.

## 7. Outputs Produced

The script can create the following files in `social_demo_outputs/`:

| Output | Description |
|---|---|
| `01_platform_volume.png` | Conversation volume by platform. |
| `02_sentiment_distribution.png` | VADER-classified sentiment distribution. |
| `03_negative_themes.png` | Leading TF-IDF terms and phrases among negative posts. |
| `04_negative_trend.png` | Daily negative share and seven-day rolling trend. |
| `top_negative_terms.csv` | Ranked TF-IDF terms from negative posts. |
| `theme_summary.csv` | Theme volume, negative share, engagement, and average sentiment. |
| `sentiment_by_campaign_platform.csv` | Sentiment mix by campaign and platform. |
| `campaign_summary.csv` | Campaign-level volume, negative share, engagement, and score. |
| `daily_sentiment_trend.csv` | Daily sentiment counts and negative-share measures. |
| `social_posts_scored.csv` | Participant data with VADER scores, sentiment labels, and derived fields. |
| `executive_decision_brief.txt` | Automatically generated signal-to-action summary. |
| `instructor_model_evaluation.csv` | Optional comparison of model output with hidden synthetic labels. |

## 8. Analytical Notes

### VADER sentiment

The script uses the VADER compound score and the following demonstration thresholds:

```text
Compound score >= 0.05  → Positive
Compound score <= -0.05 → Negative
Otherwise               → Neutral
```

VADER should be treated as an explainable baseline. It can misinterpret sarcasm, slang, mixed sentiment, domain-specific language, and Hinglish.

### TF-IDF

TF-IDF is applied to posts classified as negative to identify comparatively informative words and phrases. The script uses unigrams and bigrams. TF-IDF identifies recurring language patterns; it does not automatically prove why the issue occurred or whether it caused a business outcome.

### Campaign spike detection

The demonstration calculates:

- Daily negative-post share
- A seven-day rolling mean
- Recent campaign-level negative share

The resulting pattern should be validated using post examples, platform and market splits, and operational evidence before making a business decision.

### Executive decision brief

The generated brief includes:

- **Signal:** What changed or which campaign stands out
- **Evidence:** Post count, negative share, leading terms, and examples
- **Business meaning:** A cautious interpretation
- **Action:** Validation and response steps
- **Owner and window:** To be assigned by the participating executive team
- **Measurement:** Negative share, repeat complaints, engagement context, and response time
