Entity Resolution Experiment: Similarity Search Algorithm Comparison Overview


This project explores and compares two unsupervised learning models for entity resolution, focusing on both accuracy and computational performance. The goal is to inform high-level system design for production environments by evaluating direct string comparison and vector-based similarity search methods.

Models Tested
1. Native String Similarity Search (Levenshtein Distance)
Description:
Calculates the minimum number of single-character edits required to change one string into another.

Advantages:

Operates directly on raw string data.

Provides interpretable similarity scores (e.g., fuzz ratio) without the need for preprocessing.

Chosen for its accuracy and direct use of original data.

2. Vector Similarity Search (Nearest Neighbors)
Description:
Converts each string or record into a numeric vector using TF-IDF vectorization, then uses the nearest neighbor algorithm to identify the closest matches in vector space.

Advantages:

Enables efficient similarity search.

Highly scalable to large datasets.

Outcome & Analysis
Accuracy:

String-to-string matching (Levenshtein) was more accurate but slower, with a computation time of approximately 0.03 seconds per record.

KNN-based vector similarity was about 300 times faster (0.00009 seconds per record).

Vector-based methods may lose some information during transformation, but increasing the number of neighbors (k) from 3 to 15 improved accuracy, as more true matches were included.

Performance:

Calculating distances between vectors is significantly more efficient than string operations, making KNN suitable for large-scale applications.

Recommendations
With Ground Truth:
If ground truth labels are available (e.g., true combinations of first name, last name, date of birth, city, and email), more accurate and tunable models can be developed. Initial clusters can be set for supervised evaluation and hyperparameter tuning.

Hybrid Approach:
In production, consider a hybrid approach:

Use string similarity for candidate generation (high accuracy for initial filtering).

Use vector similarity for scaling to large datasets (high speed for final matching).

This approach balances speed and accuracy for robust entity resolution.
