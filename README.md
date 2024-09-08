# NLP Topic Modeling with K-Means: Vodafone Customer Feedback Analysis

## Overview
This analysis investigates customer feedback and complaints from Vodafone users through Twitter data. By applying Natural Language Processing (NLP) techniques and KMeans clustering, the goal is to uncover patterns, common themes, and areas of concern within customer complaints. Visual representations, such as word clouds, are generated to highlight frequently mentioned terms across clusters.

## Objective
The objective is to extract insights from customer feedback to help Vodafone improve customer service, identify common network issues, and address pain points expressed by users. The analysis focuses on clustering feedback into different themes to provide actionable insights for the business.

## Dataset
The dataset used in this project consists of tweets collected from Vodafone users who shared their complaints and feedback on Twitter. The dataset contains various fields, including usernames, tweet content, and mentions.

### Data Dictionary:
| Column Name | Description                                                |
|-------------|------------------------------------------------------------|
| `username`  | The username of the person who posted the tweet            |
| `date`      | The date when the tweet was posted                         |
| `tweet`     | The text content of the tweet                              |
| `mentions`  | Twitter mentions included in the tweet                     |
| `clean_text`| Processed tweet content, free from mentions and special characters |

## Methods
1. **Data Preprocessing:**
   - Cleaning and processing of raw tweets by removing mentions, special characters, and non-ASCII text to prepare for clustering.
   
2. **Clustering:**
   - KMeans clustering is applied to group the customer feedback into thematic clusters based on the similarity of tweet content.
   
3. **Visualization:**
   - Word clouds are generated for each cluster to visualize the most frequent terms and key topics in customer complaints.

## Clustering Analysis
Two different clustering methods are compared in this analysis: 
1. **2-Cluster Approach:**
   - The feedback is initially grouped into two clusters. However, this approach results in general themes that are too broad for practical action.
   
2. **6-Cluster Approach:**
   - A more detailed approach is applied by increasing the number of clusters to six, resulting in more defined themes, which provide deeper insights into specific areas of concern (e.g., network issues, billing problems, customer service, etc.).

## Key Findings
- **Network Issues:** Many users reported problems with network connectivity, call drops, and poor internet speed.
- **Billing Complaints:** Customers raised concerns over incorrect charges and unexplained deductions from their accounts.
- **Customer Service:** Users frequently expressed dissatisfaction with Vodafone’s customer service, citing slow response times and unhelpful representatives.

## Business Impact
The findings from this analysis can be invaluable for Vodafone's business operations. Understanding customer pain points can help:
1. Improve the quality of network services by identifying common areas facing connectivity issues.
2. Resolve billing-related problems and minimize customer dissatisfaction regarding unexpected charges.
3. Enhance customer service by addressing the major frustrations and improving response times.

By addressing these key areas, Vodafone can boost customer satisfaction and reduce churn, ultimately leading to better retention rates and improved brand reputation.

## Requirements
The project uses the following libraries and tools:
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `re` (Regular Expressions)
- `sklearn` (for KMeans clustering)
- `wordcloud` (for word cloud generation)

- ## Conclusion
This analysis provides Vodafone with valuable insights into the key areas where improvements are needed. By using the 6-cluster approach, the breakdown of customer complaints becomes clearer and more actionable. The identified clusters help the company prioritize efforts in the following areas:
- **Network Improvements:** Addressing connectivity and internet speed issues.
- **Billing Adjustments:** Resolving concerns regarding incorrect charges and deductions.
- **Customer Support Enhancement:** Improving response times and overall customer service quality.

By focusing on these areas, Vodafone can boost customer satisfaction, reduce churn, and enhance their overall reputation in the telecommunications market.

