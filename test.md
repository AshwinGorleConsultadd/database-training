
## Understanding the Problem
Due to not belonging from data Science background unable to understand the intution behind performing this sampling, hence first understanding the intution through terminologies like what we are trying to achieve here.

## Sampling
Sampling means choosing a small group from a larger set or large data, in order to learn something about the whole group — without having to look at each and every data item.

**Example :** Imagine we have a giant bowl of popcorn. we can’t eat all of it to check if it’s salty enough or good in teast, so we will take a few pieces and taste them. If they are salty, we assume most of the popcorn is salty.

**Types of Sampling**

- Random Sampling – Every data point has an equal chance. Best for generalization.
- Stratified Sampling – Ensures proportions of key subgroups (e.g., male/female, classes) are preserved.
- Systematic Sampling – Pick every kth item (e.g., every 10th record).
- Cluster Sampling – Select whole groups instead of individuals.

*//Here the question is saying to get Stratified Sampling//*

**Things to take care while Sampling**
- Avoid biosness
- Sample sizze matters
- Divercity should be present in the sample

## Weak Label
for example we have thousands of images, and we want to sort them into “high quality” and “low quality” But labeling each image by hand would take too long and sometime it is not practical. So instead we use a model (a computer program ) to guess the image quality. If the model is pretty confident (say, 95% sure it high quality), we accept that guess as a label.

Since it is not varified by human and we are not 100% sure about the result but still it is usable because most probably the label is correct hence it is called **weak label**


## Solution
we are using cte here for simplicity and readeablity of the query.

    WITH ranked_desc AS (
        SELECT image_id, score,
            ROW_NUMBER() OVER (ORDER BY score DESC) AS rn
        FROM unlabeled_image_predictions
    ),
    ranked_asc AS (
        SELECT image_id, score,
            ROW_NUMBER() OVER (ORDER BY score ASC) AS rn
        FROM unlabeled_image_predictions
    ),
    positive_samples AS (
        SELECT image_id, 1 AS weak_label
        FROM ranked_desc
        WHERE rn % 3 = 1
        LIMIT 10000
    ),
    negative_samples AS (
        SELECT image_id, 0 AS weak_label
        FROM ranked_asc
        WHERE rn % 3 = 1
        LIMIT 10000
    )
    SELECT image_id, weak_label
    FROM (
        SELECT * FROM positive_samples
        UNION ALL
        SELECT * FROM negative_samples
    ) AS combined
    ORDER BY image_id;

### Step-by-Step Query Explaination

- **Step 1** : Creating *"ranked_desc"* table which orders the images in desending order of their quality score hence we will use it for taking positive samples.
- **Step 2** : Creating *"ranked_asce"* table which orders the images in ascending order of their quality score hence we will use it for taking negative samples.
- **Step 3** : creating *"positive_samples"* table from *"ranked_desc"*  which is taking each thired record starting from 1
- **Step 4** :creating *"negative_samples"* table from *"ranked_asce"*  which is taking each thired record starting from 1
- **Step 5** :simple combining the results of both *"positive_samples"* and *"nagative_samples"* table
