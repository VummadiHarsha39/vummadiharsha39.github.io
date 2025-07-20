---
title: "Personal Project: A Full-Stack Approach to Review Intelligence: From Data to Deployment"
date: 2025-07-19
excerpt: "NLP Application for Review Analysis "
collection: portfolio
---



## Preface 
In today's digital age, online reviews are a cornerstone of consumer trust and business reputation. But what happens when those reviews aren't genuine? Counterfeit content, particularly fake reviews, can severely mislead consumers and undermine legitimate businesses. This challenge spurred me to develop a sophisticated Multi-Modal Review Analysis System, a project designed not just to detect emotions, but to intelligently identify and explain deceptive content.

This article will walk you through the journey of building this system, organized into four distinct phases, highlighting the innovative approaches we took.

![Emotion Output Example](/images/Emo_output.png)



## Phase 1: The Foundation - Data Acquisition and Preparation

Every robust machine learning project begins with high-quality data. For this endeavor, I leveraged the GoEmotions Dataset, a rich collection of Reddit comments annotated with an impressive 28 distinct emotions (plus neutral). This dataset's diversity was crucial for training a nuanced emotion classifier.

To manage this data efficiently, we created a loader.py file within our project's data folder. Additionally, preprocessor.py was developed with a clean_text function to prepare the raw text for our models, ensuring a consistent and high-quality input.

The labeled dataset provided 58,009 examples with a maximum sequence length of 30 for training and evaluation. After meticulous preprocessing, our cleaned data was split into:

Training: 43,410 examples

Testing: 5,427 examples

Validation: 5,426 examples

## Phase 2: This structured approach laid the groundwork for reliable model training and evaluation.

This phase is where the "magic" happens, housing the two main deep learning models that form the heart of this project: the Emotion Classifier and the Deception Detector.

### The Emotion Classifier: Understanding User Sentiment
Our first deep learning model, built using Hugging Face Transformers, is designed to detect and classify emotions in review text across 28 distinct categories—a multi-label classification task. This goes beyond simple positive/negative sentiment, offering a much deeper understanding of user feelings.

The model is based on a Transformer architecture, specifically a BERT-base-uncased model. BERT, renowned for its ability to understand context in text, was fine-tuned on our specialized emotion classification task, adapting its vast pre-trained knowledge to this specific domain.

### The Deception Detector: Our Unique Edge
This line graph visualizes the fluctuations in total bus ridership on a monthly basis from January 2013 to December 2016. We can observe seasonal patterns, typically with higher ridership in certain months of the year, and an overall trend in ridership over the four-year period.
This is where our project truly stands out. I developed a second, custom deep learning model—the Deception Detector. Unlike traditional text-only approaches, this model takes both the raw review text and the emotional probabilities (the output from our Emotion Classifier for a given text) to classify a review as either real or fake. This multi-modal feature fusion is the core innovation for counterfeit detection.

This custom PyTorch model extends a standard Transformer by incorporating a unique fusion layer. It uses a BERT-base-uncased model as its base text encoder but then intelligently integrates the emotional probabilities.

For training this crucial model, we used a mixed dataset:

Real Reviews: Primarily sourced from the GoEmotions dataset.

Synthetic Fake Reviews: For initial pipeline validation, a portion of real reviews were intentionally mislabeled as fake. (It's important to note that for real-world deployment, this would ideally be replaced with genuinely deceptive datasets or more sophisticated synthetic data generation methods).

### The Explanation Generator: Unveiling Insights
Perhaps the most exciting part of this project is the Explanation Generator. My goal was to provide human-readable explanations for the "real/fake" verdicts from the Deception Detector and to offer a concise 1-2 line summary of the customer's intent behind the review.

The Explanation Generator takes multiple inputs: the raw review text, the verdict (real/fake), the confidence score, emotion probabilities, and emotion names.

Functionality:

Dominant Emotion & Emotional Diversity: It first identifies the single emotion with the highest probability. It then uses Shannon entropy to measure the evenness of the distribution of emotional probabilities across all emotions.

* Detecting Artificial Sentiment: A key heuristic is applied to detect instances where a single emotion’s probability is overwhelmingly high, while the overall emotional diversity (measured by entropy) is low. This pattern often indicates an artificial, fabricated, or overly simplistic, yet excessively positive, sentiment—a characteristic frequently observed in fraudulent reviews.

* Formulating General Statements: Based on the verdict and confidence, it formulates a general statement. If a review is classified as false, it typically exhibits high dominant emotion coupled with low emotional diversity. Conversely, real reviews tend to display diverse emotional ranges, or maintain factual/neutral tones.

* Customer Intent Summary: This part uses rules based on the verdict and the dominant_emotion to create a concise 1-2 line summary of the customer's intent. For real reviews, it interprets the dominant emotion into intent (e.g., “is very positive and likely satisfied,” “is negative and likely dissatisfied”). For fake reviews, it summarizes what the review attempts to convey (e.g., “attempts to convey extreme positive sentiment”). This provides valuable business insight even from non-genuine content.

### Robust Tracking with MLflow
For efficient experiment management and reproducibility, we integrated MLflow for local tracking. We trained both our Emotion Classifier and Deception Detector models, logging their metrics, parameters, and saving model artifacts to the mlruns directory. We also promoted our best-performing models to the production stage within MLflow, ensuring proper versioning and deployment readiness.



## Phase 4: Local Server Integration (FastAPI Backend)
To bring our models to life as a usable service, I orchestrated the backend with FastAPI.

src/services/prediction_service.py: This crucial file loads both models from our local MLflow registry and then calls the Explanation Generator to process review data.

web_app/backend/main.py and schemas.py: These files define the FastAPI backend API, exposing endpoints such as /health (for service status), /analyze_review (for single review analysis), and /batch_analyze_reviews (for processing multiple reviews).

Why FastAPI? FastAPI provides a high-performance web API that can serve predictions from our ML models to any client, including our frontend website. This seamless integration allows for real-time analysis and unlocks the practical application of our sophisticated models.

![Backend System Diagram](/images/Backend.png)

I also built the a frontend Interactive web interface using Next.js and React

![Emotion Interface Screenshot](/images/Emo_interface.png)

---------------------------------------------
This project represents a comprehensive solution for understanding and identifying genuine sentiment in online reviews. By combining the power of Transformer models, multi-modal input, and an intelligent explanation generator, we've built a system that goes beyond simple classification, providing valuable, interpretable insights for businesses and consumers alike.

If you want more explanation in great detail please read same project article on medium "https://medium.com/@vummadiharsha123/summer-project-3-nlp-application-to-detect-emotional-counterfeit-of-a-customer-review-e4e583626f96"











