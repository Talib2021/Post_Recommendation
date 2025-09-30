
# Post_Recommendation System Report

## Approach

We designed a **content + engagement-based recommendation system** to suggest the top 3 posts for each user.  
The pipeline works as follows:

1. **User Profile Matching**  
   - Each user has `top_3_interests` and a `past_engagement_score`.
   - Posts are tagged with multiple topics. We calculate **interest overlap** between user interests and post tags.

2. **Post Filtering**  
   - Exclude posts that the user has already engaged with (from the Engagements dataset).

3. **Scoring Function**  
   - Score = (Number of matching interests) + (Content-type weight).  
   - Content type weights:  
     - Video = 1.0  
     - Image = 0.8  
     - Text = 0.6  
   - Example: If a user is interested in "sports" and a post has "sports, art" tags with content type *video*, the score = 2 (interests matched) + 0.2*1.0 = 2.2.

4. **Top-3 Selection**  
   - For each user, posts are ranked by score.  
   - The top 3 highest-scoring posts are recommended.

---

## Metrics

To evaluate this system, we can use:

1. **Precision@k**: Of the top-k recommendations, how many were actually engaged with by users?
2. **Recall@k**: Of all relevant posts, how many were recommended within the top-k?
3. **Engagement Uplift**: Compare average engagement rate of recommended posts vs. random baseline.
4. **Diversity Score**: Ensure recommended posts span different content types and topics.

---

## Possible Extensions

1. **Hybrid Modeling**: Combine content-based approach with collaborative filtering (user-user or item-item similarity from engagement history).
2. **Personalization Weights**: Learn optimal weights for content types and interest overlap using machine learning on past engagement data.
3. **Temporal Dynamics**: Factor in time (recent posts, recent user activity) to keep recommendations fresh.
4. **Cold Start Handling**: Use demographic similarity (age, gender) when engagement data is sparse.
5. **Explainability**: Provide reasons like "Recommended because you liked *sports* videos" to improve user trust.

---

## Example Recommendation (User U1)

- Top interests: **sports, art, gaming**  
- Recommended posts:  
  1. **P78** – sports, art (video) → Score 2.2  
  2. **P49** – tech, gaming (video) → Score 1.2  
  3. **P97** – travel, sports (video) → Score 1.2  

