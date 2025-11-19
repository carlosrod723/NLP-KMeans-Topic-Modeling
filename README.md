# Unsupervised Topic Modeling: Vodafone Customer Feedback Analysis

**Status**: Completed
**Last Updated**: November 2025
**Author**: Carlos Rodriguez (carlos.rodriguezacosta@gmail.com)

An unsupervised NLP system that analyzes 16,194 Vodafone customer tweets using KMeans clustering to identify 6 distinct complaint categories. The project demonstrates iterative cluster refinement (K=2 → K=6), custom word cloud visualizations with brand-aligned styling, and transforms unstructured social media feedback into actionable business insights for telecommunications service improvement.

## 🎯 Core Problem Solved

Telecommunications companies receive thousands of customer complaints daily through social media but lack automated systems to categorize and prioritize issues. Manual review is slow, inconsistent, and misses emerging patterns. This project builds an unsupervised topic modeling system that processes 16K+ Vodafone tweets, clusters them into 6 thematic categories (billing issues 47.7%, network problems, roaming charges, customer service, porting difficulties), and generates visual summaries enabling data-driven decision-making for service improvements and churn reduction.

## ✨ Key Technical Achievements

- **Iterative Cluster Optimization**: Systematically compared K=2 (too broad) vs K=6 (optimal granularity) clustering approaches with business-driven justification for final selection
- **Large-Scale Text Processing**: Handled 21,047 raw tweets with 23% data reduction through deduplication and noise removal, creating 16,194 × 6,266 sparse document-term matrix
- **Custom Brand-Aligned Visualizations**: Generated 8 word clouds with Twitter logo masking and dynamic color extraction, producing publication-quality outputs (4000×1500px) for business presentations
- **Actionable Business Insights**: Identified billing issues as dominant complaint category (47.7% of feedback), network quality problems across multiple clusters, and international roaming as distinct pain point requiring separate attention

## 🛠 Technology Stack

### Core Technologies
- **Language**: Python 3.x
- **Environment**: Google Colab with Google Drive integration
- **Algorithm**: KMeans clustering (scikit-learn) with Euclidean distance
- **Dataset**: 21,047 Vodafone customer tweets from Twitter

### Key Libraries
- **scikit-learn**: KMeans clustering (K=2, K=6), CountVectorizer with min_df=0.0001 and max_df=0.7 frequency thresholds
- **nltk**: Text preprocessing and tokenization
- **wordcloud**: Custom word cloud generation with ImageColorGenerator for logo color extraction
- **pandas**: DataFrame operations on 21K records with deduplication and filtering reducing to 16K usable tweets
- **PIL (Pillow)**: Twitter logo image processing for word cloud masking
- **matplotlib** & **seaborn**: Visualization framework for word cloud rendering

## 🏗 Architecture

### High-Level Design
Notebook-based unsupervised learning pipeline with iterative clustering refinement. Google Colab environment enables cloud execution with visual output generation. Architecture optimized for sparse text data using Bag-of-Words vectorization feeding into KMeans algorithm for thematic grouping.

### Key Components
1. **Data Cleaning Module**: Processes 21K tweets → removes @mentions with regex (@[\w]*) → filters non-ASCII characters → lowercases text → removes words ≤2 chars → deduplicates → outputs 16,194 clean tweets
2. **Vectorization Engine**: CountVectorizer creates (16194, 6266) sparse matrix with unigrams only, English stopwords removal, min_df=0.0001 (rare word filter), max_df=0.7 (common word filter)
3. **KMeans Clustering**: Two-phase approach: initial K=2 broad categorization (13.9%/86.1% imbalance) → refined K=6 granular clustering (7.6%, 13.0%, 14.5%, 47.7%, 3.2%, 14.1% distribution)
4. **Word Cloud Generator**: Custom function with Twitter logo URL masking, ImageColorGenerator for brand colors, black background, 4000×1500px resolution, matplotlib rendering

### Data Flow
tweets.csv (21K rows) → pandas load with ISO-8859-1 encoding → @mention removal → ASCII filtering → lowercase → tokenization → deduplication (21K → 16K) → CountVectorizer (6,266 features) → sparse matrix → KMeans fit (K=6) → cluster assignments → per-cluster text concatenation → word cloud visualization → business insight extraction

## 🚀 Key Features

### Iterative KMeans Cluster Refinement
- **What**: Two-phase clustering strategy comparing K=2 (broad themes) vs K=6 (granular categories) to find optimal granularity for business insights
- **How**: First run: KMeans(n_clusters=2) produces 13.9%/86.1% split → analysis reveals too broad; Second run: KMeans(n_clusters=6) produces balanced distribution (largest cluster 47.7%) → enables actionable categorization
- **Why**: K=2 creates overly general "all complaints" vs "specific complaints" without actionable detail; K=6 separates billing (47.7%), network (14.5%), roaming (7.6%), customer service (13.0%), porting (3.2%), unresolved complaints (14.1%)
- **Impact**: Demonstrates analytical thinking through comparative analysis; business can prioritize top cluster (billing: 7,722 tweets) while addressing niche issues (porting: 519 tweets); validates cluster selection through interpretability rather than pure metrics

### Custom Twitter Logo Word Cloud Masking
- **What**: Word clouds shaped like Twitter logo with brand-aligned colors dynamically extracted from logo image
- **How**: Fetches Twitter logo PNG from external URL → converts to numpy array mask → ImageColorGenerator extracts color palette → WordCloud(mask=Mask, background_color='black') shapes text → recolor(color_func=image_colors) applies brand colors
- **Why**: Standard rectangular word clouds lack visual appeal for presentations; Twitter-shaped clouds reinforce data source (social media) and create professional, branded visualizations for stakeholder communication
- **Impact**: 8 publication-quality visualizations (4000×1500px) suitable for business reports; immediate visual identification of top terms per cluster (e.g., Cluster 3: "bill", "deducted", "amount"); enhances communication of technical findings to non-technical executives

### Bag-of-Words with Intelligent Frequency Filtering
- **What**: CountVectorizer with dual thresholds: min_df=0.0001 (removes words in <0.01% of docs) and max_df=0.7 (removes words in >70% of docs)
- **How**: Analyzes 16,194 documents for word frequencies → filters rare words appearing in <2 tweets (noise/typos) → filters ubiquitous words appearing in >11,335 tweets (non-discriminative) → retains 6,266 meaningful features
- **Why**: Rare words (names, typos, URLs) add noise without signal; common words ("vodafone", "network" in 70%+ tweets) appear in all clusters and don't differentiate themes; balanced filtering maximizes cluster separation
- **Impact**: 6,266 features capture semantic diversity while eliminating noise; sparse matrix representation (16K × 6K) enables efficient KMeans computation; cluster coherence improves through discriminative vocabulary

### Twitter-Specific Text Preprocessing
- **What**: Multi-stage pipeline handling social media noise: @mention removal → non-ASCII filtering → lowercasing → short word removal → deduplication
- **How**: Regex pattern @[\w]* strips handles (@VodafoneIN, @TRAI) → ASCII check removes emojis/multilingual chars → lowercase normalization → tokenization → filter len(word)<=2 → drop_duplicates on clean_text column
- **Why**: Twitter data contains unique noise: @mentions don't convey sentiment; emojis/multilingual text complicate tokenization; duplicates (retweets) bias cluster sizes; short words ("hi", "ok") lack meaning; preprocessing standardizes input
- **Impact**: 23% data reduction (21,047 → 16,194) through deduplication; clean corpus enables accurate clustering; ASCII filtering handles multilingual Indian market tweets (Hindi/English code-switching)

### Six-Theme Business-Aligned Clustering
- **What**: K=6 clustering producing interpretable business categories: billing (47.7%), network (14.5%), general service (13.0%), unresolved (14.1%), roaming (7.6%), porting (3.2%)
- **How**: KMeans assigns each tweet to nearest centroid in 6,266-dimensional space → clusters validated through word frequency analysis (top terms per cluster) → business interpretation applied based on dominant keywords
- **Why**: Six categories provide optimal balance: enough granularity for actionable insights (separate roaming from billing) but not so many that themes overlap; aligns with telecommunications business structure (network ops, billing dept, customer service, roaming team)
- **Impact**: Enables prioritization: billing issues (7,722 tweets) require immediate attention; porting problems (519 tweets) are niche; network complaints span multiple clusters suggesting systemic infrastructure issues; provides roadmap for service improvement initiatives

## 📊 Performance & Scale

| Metric | Value | Context |
|--------|-------|---------|
| Original Dataset | 21,047 tweets | Raw Twitter data with duplicates and noise |
| Processed Dataset | 16,194 tweets | After deduplication and cleaning (23% reduction) |
| Feature Dimensions | 6,266 unique terms | Reduced from full vocabulary using min_df/max_df filters |
| Sparse Matrix Size | 16,194 × 6,266 | Document-term matrix for KMeans input |
| Number of Clusters (K) | 6 final (vs 2 initial) | Iteratively refined for optimal granularity |
| Largest Cluster | Cluster 3 (47.7%) | Billing & deductions: 7,722 tweets |
| Smallest Cluster | Cluster 4 (3.2%) | Porting & migration: 519 tweets |
| Word Cloud Resolution | 4000 × 1500 pixels | High-quality output for presentations |
| Visualization Outputs | 8 word clouds | 2 from K=2 approach + 6 from K=6 approach |

## 🔧 Technical Highlights

### Why KMeans Over LDA/NMF for Topic Modeling
Three topic modeling approaches available: **LDA (Latent Dirichlet Allocation)**, **NMF (Non-negative Matrix Factorization)**, and **KMeans clustering**. **Chose KMeans** for several reasons: (1) **Simplicity** - KMeans requires minimal hyperparameter tuning (only K) vs LDA's alpha/beta priors and iteration counts; (2) **Speed** - KMeans converges quickly on sparse high-dimensional data (6,266 features) through efficient Euclidean distance calculations; (3) **Hard Assignments** - each tweet belongs to exactly one cluster, simplifying business interpretation ("this is a billing complaint") vs LDA's probabilistic topic mixtures ("30% billing, 50% network, 20% service"); (4) **Interpretability** - cluster centroids directly map to word importance, whereas LDA topic distributions are abstract. **Trade-off**: KMeans assumes spherical clusters and Euclidean distance, which may not capture semantic relationships as well as probabilistic models; no topic mixing means tweets discussing both billing AND network issues forced into single category. **Decision**: For customer feedback categorization with clear business categories, KMeans provides sufficient accuracy with superior interpretability—business stakeholders prefer "7,722 billing complaints" to "23% of corpus shows billing topic with 0.65 probability."

### Cluster Distribution Analysis and Business Prioritization
Six clusters exhibit significant size imbalance requiring strategic interpretation. **Cluster 3 (Billing - 47.7%)**: Dominates with 7,722 tweets containing "bill", "deducted", "amount", "balance", "recharge"—indicates systematic billing problems requiring immediate attention; high volume suggests widespread issue affecting nearly half of complainants. **Mid-Sized Clusters**: Cluster 2 (Network - 14.5%, 2,343 tweets), Cluster 5 (Unresolved - 14.1%, 2,278 tweets), Cluster 1 (Service - 13.0%, 2,100 tweets) represent 40% of feedback combined—suggests 3-4 major operational areas need improvement. **Small Clusters**: Cluster 0 (Roaming - 7.6%, 1,232 tweets) and Cluster 4 (Porting - 3.2%, 519 tweets) indicate niche but distinct issues. **Business Implications**: (1) **Prioritize billing audit** - 47.7% concentration demands immediate investigation of charging systems; (2) **Infrastructure investment** - network complaints span multiple clusters suggesting pervasive quality issues; (3) **Separate roaming team** - 7.6% is small but distinct enough to warrant specialized handling; (4) **Don't ignore small clusters** - porting difficulties (3.2%) may cause high-value customer churn despite low volume. **Strategic Insight**: Imbalance reveals what customers care about most; uniform distribution would suggest unfocused complaints, whereas concentration highlights systemic problems.

### CountVectorizer Parameter Optimization Strategy
Vectorization parameters critically impact clustering quality through vocabulary selection. **min_df=0.0001 (0.01% threshold)**: Filters words appearing in <2 documents out of 16,194 (0.0001 × 16,194 ≈ 1.6); removes typos ("vodafoone"), rare names ("@JohnDoe123"), URLs—these contribute noise without discriminative power across clusters. **max_df=0.7 (70% threshold)**: Filters words appearing in >11,335 documents; removes ubiquitous terms like "vodafone" (appears in nearly all tweets since they're Vodafone complaints), "network" (appears across billing, service, technical clusters)—these don't help differentiate themes. **Result**: 6,266 features represent "Goldilocks zone" of vocabulary—common enough to be meaningful but rare enough to distinguish clusters. **Why Not TF-IDF?**: Raw counts preserve word frequency importance (complaint mentioning "deducted" 5× signals stronger billing concern than 1×); TF-IDF downweights frequent words, but max_df already handles this. **Alternative Considered**: No min/max thresholds → 20K+ features including noise; tighter thresholds (min_df=0.001, max_df=0.5) → only 3K features, losing nuance. **Validation**: Word clouds show coherent themes (Cluster 3: "bill", "deducted", "recharge" clearly financial), confirming parameter choices produced interpretable clusters.

### Deduplication Impact on Cluster Quality
Data reduction from 21,047 → 16,194 tweets (23% decrease) through duplicate removal critically improves clustering. **Problem**: Twitter users often retweet identical complaints or copy-paste template messages to @VodafoneIN; duplicates artificially inflate cluster sizes and bias KMeans centroids toward repeated text. **Example**: If "network down in Mumbai" appears 500 times (retweets), KMeans creates cluster centered on this exact phrase rather than generalizing "network issues." **Solution**: `df.drop_duplicates(subset='clean_text')` removes 4,853 duplicate tweets based on preprocessed text (after @mention removal, lowercasing). **Impact**: (1) **Reduced bias** - clusters reflect unique complaint themes, not viral tweet volume; (2) **Faster computation** - 23% fewer documents speeds KMeans convergence; (3) **Better generalization** - centroids represent diverse vocabulary within theme rather than single viral phrase. **Trade-off**: Loses information about complaint popularity (viral tweets indicate widespread frustration), but clustering prioritizes theme identification over volume measurement. **Validation**: Final clusters show diverse vocabulary (Cluster 3 has "bill", "deducted", "amount", "balance"—not dominated by single phrase), confirming deduplication prevented viral tweet bias.

### Visual Communication Through Custom Word Clouds
Word clouds transform abstract cluster centroids into interpretable business insights but require careful design. **Technical Implementation**: (1) Fetches Twitter logo PNG from external URL as numpy array; (2) ImageColorGenerator extracts blue/white color palette from logo pixels; (3) WordCloud class applies logo as mask, constraining text to Twitter bird shape; (4) Background set to black for contrast; (5) 4000×1500px resolution for print-quality output. **Design Rationale**: Twitter logo shape immediately communicates data source (social media feedback); brand colors (blue/white) create professional aesthetic for stakeholder presentations; high resolution enables embedding in reports without pixelation. **Word Frequency Encoding**: Font size represents term frequency within cluster—"bill" appearing 3,000× in Cluster 3 rendered larger than "payment" with 500×; enables quick identification of dominant themes. **Limitations**: Word clouds show frequency but not context (can't distinguish "good network" vs "bad network"); no sentiment information; spatial placement is aesthetic, not meaningful (words near each other aren't necessarily related). **Why Not t-SNE/PCA Plots?**: Dimensionality reduction visualizations show cluster separation in 2D but require technical explanation; word clouds are immediately interpretable by non-technical business stakeholders. **Business Impact**: Executives can glance at Cluster 3 word cloud and immediately see "bill", "deducted", "amount" dominating—no data science expertise required.

## 🎓 Learning & Challenges

### Challenges Overcome
1. **Lack of Quantitative Evaluation Metrics**: Project doesn't include silhouette scores, elbow method, or inertia plots to validate K=6 choice; addressed through qualitative analysis (word cloud coherence, business interpretability) and comparative approach (K=2 vs K=6 documented comparison)
2. **Multilingual Twitter Data**: Indian market tweets contain Hindi/English code-switching and emojis; solved with ASCII filtering removing non-English characters, but loses semantic information from Hindi complaints (acceptable trade-off for English-focused analysis)
3. **Extreme Cluster Imbalance**: Cluster 3 (47.7%) dominates while Cluster 4 (3.2%) is tiny; accepted imbalance as reflecting real-world complaint distribution rather than forcing artificial balance through resampling (business insight: billing really is the biggest issue)

### Key Learnings
- **Unsupervised learning requires business validation**: Without labeled data, cluster quality must be validated through domain expertise (telecommunications knowledge) and stakeholder review; technical metrics alone insufficient
- **Iterative K selection beats arbitrary choice**: Comparing K=2 (too broad) vs K=6 (optimal) demonstrates analytical rigor; shows understanding that K is hyperparameter requiring experimentation rather than random selection
- **Visual communication as important as technical accuracy**: Custom word clouds with brand styling converted technical clustering results into executive-ready insights; data science impact depends on communication
- **Preprocessing dominates clustering quality**: 23% data reduction through deduplication and noise removal more impactful than algorithm choice; clean data + simple KMeans outperforms dirty data + complex models
- **Cluster imbalance reflects reality**: Unlike supervised learning where class balance aids training, unsupervised clustering imbalance reveals what customers actually complain about (billing dominates because it's genuinely the biggest problem)

## 📁 Project Structure

```
NLP-KMeans-Topic-Modeling/
├── README.md                                  # This file (comprehensive documentation)
├── LICENSE                                    # MIT License
├── requirements.txt                           # Python dependencies
├── jupyter-notebook/
│   └── NLP_Kmeans_Topic_Modeling.ipynb       # Main analysis notebook (preprocessing → clustering → visualization)
└── images/                                    # Word cloud visualizations
    ├── wordcloud_cluster_0_0.png             # K=2 approach: Cluster 0
    ├── wordcloud_cluster_0_1.png             # K=2 approach: Cluster 1
    ├── wordcloud_cluster_1_0.png             # K=6 approach: Cluster 0 (Roaming)
    ├── wordcloud_cluster_1_1.png             # K=6 approach: Cluster 1 (Service)
    ├── wordcloud_cluster_1_2.png             # K=6 approach: Cluster 2 (Network)
    ├── wordcloud_cluster_1_3.png             # K=6 approach: Cluster 3 (Billing)
    ├── wordcloud_cluster_1_4.png             # K=6 approach: Cluster 4 (Porting)
    └── wordcloud_cluster_1_5.png             # K=6 approach: Cluster 5 (Unresolved)
```

**Notable Structure Decisions**:
- Images directory stores 8 word clouds (2 from initial K=2 + 6 from final K=6) documenting iterative refinement process
- Notebook naming convention (wordcloud_cluster_X_Y) tracks clustering approach (X) and cluster number (Y)
- Google Colab workflow eliminates local environment setup requirements

## 🔒 Security Considerations

- **Public Twitter Data**: Dataset contains publicly posted tweets; no privacy violations as users posted complaints publicly with @VodafoneIN mentions
- **No API Keys**: Word cloud logo fetched from public URL (clipart-library.com); no Twitter API authentication required
- **Anonymization**: Usernames included in dataset but not used in analysis; consider removing username column if sharing publicly to protect user privacy
- **Data Sensitivity**: Customer complaints may reveal security vulnerabilities (e.g., "account hacked", "fraudulent charges"); Vodafone should treat identified issues as confidential
- **No PII in Visualizations**: Word clouds show aggregate word frequencies, not individual tweets or user identifiers

## 📈 Future Enhancements

**Quantitative Cluster Validation**:
- Implement silhouette analysis to validate K=6 choice with scores ranging -1 (poor) to +1 (excellent clustering)
- Elbow method plotting inertia (within-cluster sum of squares) for K=2 to K=10 to empirically determine optimal K
- Davies-Bouldin Index and Calinski-Harabasz Score for cluster separation metrics
- Compare multiple K values systematically rather than manual K=2 vs K=6 comparison

**Dimensionality Reduction Visualization**:
- t-SNE projection of 6,266-dimensional space to 2D for cluster separation visualization
- PCA analysis showing variance explained by top components and cluster overlap
- Interactive 3D scatter plots (Plotly) allowing exploration of cluster boundaries
- Colored by cluster assignment to validate separation in reduced space

**Feature Engineering Improvements**:
- TF-IDF weighting instead of raw counts to emphasize discriminative terms per cluster
- Bigrams/trigrams to capture phrases ("customer service", "international roaming", "network issue")
- Sentiment analysis layer (VADER, TextBlob) to separate "billing issue resolved quickly" from "billing nightmare"
- Character-level N-grams to handle misspellings and Twitter abbreviations ("pls", "thx", "asap")

**Temporal Analysis**:
- Time-series clustering: how do complaint themes evolve over months?
- Identify spike events (e.g., network outage causing surge in Cluster 2)
- Seasonal patterns (roaming complaints increase during holiday travel)
- Track cluster distribution changes after service improvements

**Alternative Topic Modeling**:
- LDA (Latent Dirichlet Allocation) for probabilistic topic assignments allowing tweets to belong to multiple themes
- NMF (Non-negative Matrix Factorization) for parts-based topic decomposition
- BERTopic using transformer embeddings for semantic topic modeling
- Compare KMeans vs LDA vs NMF performance on same dataset

**Production Deployment**:
- Real-time tweet classification API: new tweet → preprocess → vectorize → predict cluster → route to department
- Automated monitoring dashboard tracking cluster distribution over time
- Alert system when cluster sizes shift dramatically (e.g., sudden spike in Cluster 2 indicating network outage)
- Integration with customer service ticketing system for automatic complaint categorization

## 📚 Related Projects

- **NLP-Canva-Reviews**: Binary sentiment classification with N-grams and TF-IDF comparison achieving optimal performance through feature engineering
- **NaiveBayes-MultiClass-Classification**: Multi-class text classification of 2.3M financial complaints with 78.74% accuracy using Multinomial Naive Bayes
- **Customer-Churn-Prediction**: Predictive modeling for customer retention with imbalanced dataset handling
- **Social-Media-Sentiment-Tracker**: Real-time sentiment analysis pipeline for brand monitoring across Twitter/Reddit

---

**Contact**: carlos.rodriguezacosta@gmail.com
**License**: MIT License (see LICENSE file)
**Dataset**: Vodafone Twitter customer feedback (21,047 tweets)
**Contributions**: Open to pull requests for quantitative validation metrics, alternative topic modeling approaches, and temporal analysis enhancements
