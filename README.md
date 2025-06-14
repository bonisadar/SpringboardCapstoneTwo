## Project Title

Building a machine learning model to detect phishing URLs.

## Project Overview

Phishing URLs are deceptive links crafted by cybercriminals to steal sensitive user information. These malicious URLs 
are commonly spread via spam emails, fraudulent messages, and compromised websites.

Phishing attacks pose severe risks to individuals and organizations, leading to financial losses and data breaches. 
With advancements in technology, cybercriminals are constantly refining their attack methods. In 2023, phishing attacks 
surged by 173% compared to the previous quarter.

This project aims to build an efficient and scalable machine learning model to detect phishing URLs and mitigate 
cybersecurity threats.

## Methodology

This approach focuses on analyzing the inherent characteristics of phishing URLs rather than relying on external data 
sources like robots.txt, CSS values, or WHOIS records. Scraping such information can be tedious, and in many cases, 
it may not even be available. By leveraging a simple yet effective methodology, this approach enables efficient 
phishing URL detection with minimal computational overhead.

### Key Methodological Choices:

  • URL-Based Feature Engineering: Extracting meaningful attributes from URLs.

  • Caching for Performance Optimization: We use Python’s @lru_cache(maxsize=None) from the functools module to store 
function results, improving computational efficiency.

  • Machine Learning Classifiers: Multiple models are trained to detect phishing URLs based on extracted features.

### Features Used for Detection:

  - URL Length<br>
  - Extracting the Fully Qualified Domain Name (FQDN)<br>
  - Top-Level Domain (TLD) Similarity Scores<br>
  
	      - Used A pandas DataFrame containing legitimate top level domains extracted from wikipedia<br>
	      - https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains<br>
		  
  - Probability Distribution of Special Characters<br>
  - Entropy-Based Analysis (Measures randomness in URLs)<br>
  - Obfuscation Detection (Encoded characters, hexadecimal IPs, hidden redirections)<br>
  - Text Similarity Metrics (To identify deceptive domain names)<br>
  - Word-Based Features (Using NLTK's English corpus)<br>
  - Log Transformations (To normalize skewed data)<br>

## Data Sources

We used a well-documented phishing and legitimate URL dataset from Kaggle, ensuring it was suitable for machine learning.

## Data Cleaning 

The dataset is of very good conditions. Only a few inconsistencies in the URLs, including some non-ASCII character, 
occasional non alphanumeric characters at the beginning of the URLS and additional https//:’s or www’s. 

## Feature Engineering

Since the raw dataset contained only URLs and their legitimacy labels, we applied various feature extraction techniques 
to transform the data into a structured format for machine learning.

### Key Feature Engineering Steps:

1. Extracting URL Components:
   - Fully Qualified Domain Name (FQDN)
   - Top-Level Domain (TLD)

2. Shannon Entropy-Based Features:
   - Phishing URLs tend to be more random than legitimate URLs. We used Shannon Entropy to quantify randomness in URL 
  structures.

3. Text Similarity-Based Features:
   - To detect deceptive domains, we compared TLDs against a legitimate TLD list from Wikipedia, using:

       a. Levenshtein Distance (Fuzzy Score)<br>
       b. Damerau-Levenshtein Normalized Distance<br>
       c. Jaro-Winkler Algorithm<br>

4. Unique Word Chunks:
   - Extracted distinctive word patterns from FQDNs to match against known phishing and legitimate word patterns.

5. URL Obfuscation Detection:
   - Identified techniques like hexadecimal/octal IP representations, encoded characters (%2F instead of /), and hidden 
     redirections.<br>
   - Calculated entropy to detect obfuscation attempts.

6. Log Transformations:
   Many ML algorithms perform better when features follow a normal distribution.<br>
   - Applied log transformation to reduce skewness in numerical features.


## Machine learning Algorithms

We implemented and evaluated multiple classifiers using Python’s scikit-learn library:

  - K-Nearest Neighbors (K-NN)
  - Support Vector Classifier (SVC)
  - XGBoost Classifier


### Feature Engineering with TF-IDF and Dimensionality Reduction:

In addition to URL-based features, we incorporated text-based features using Term Frequency-Inverse Document Frequency 
(TF-IDF).

### Why TF-IDF?
  - Phishing URLs often contain misleading terms to trick users.<br>
  - TF-IDF helps capture word patterns that indicate phishing attempts.
  
### Dimensionality Reduction with TruncatedSVD

Since TF-IDF creates high-dimensional sparse vectors, we applied Truncated Singular Value Decomposition (TruncatedSVD) 
to reduce dimensionality while preserving critical information.

The compressed features were combined with numerical features before training the XGBoost model.
This hybrid approach significantly improved classification accuracy while maintaining a balanced model.

## Future Improvements

URLs are primarily text-based, and there are many powerful techniques to extract more meaningful insights. For example, 
techniques like Word2Vec could be applied to compare URL components in more sophisticated ways. Currently, similarities 
are calculated based on exact matches due to limitations in computational power, but partial matching could yield 
better performance.

In future work, instead of using a static similarity index between top-level domains extracted from Wikipedia, we could 
dynamically compute the similarity between URLs extracted directly from the web and the URLs in our dataset. This would 
make the approach more adaptive and up-to-date.

Additionally, tools from NLTK, such as Latent Semantic Analysis (LSA), or even more advanced models like BERT, could be 
applied to improve the comparison and scoring process.

I’m particularly excited to explore TF-GNN from TensorFlow in the future, as it enables building Graph Neural Networks 
(GNNs). This would be especially useful for problems where the relationships between data points—such as URLs—can be 
effectively represented as a graph, allowing for deeper insights into phishing patterns and network structures.

## License
This project is licensed under the MIT License – see the LICENSE file for details.

## Contributions
If you'd like to contribute to this project, please fork the repository and submit a pull request. Ensure that your 
contributions follow the coding style and include tests where applicable.

## Credits
A special thanks to David Cournapeau and Matthieu Brucher for their contributions to the scikit-learn library. I also 
appreciate Kaggle for providing an excellent dataset that made this project possible. Lastly, my sincere gratitude to 
my Springboard mentor, Karthik Ramesh, for his invaluable support, guidance, and insightful feedback throughout this 
journey.