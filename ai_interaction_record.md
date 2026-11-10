# AI Interaction Record - Phase I

We used ChatGPT to help develop and understand our Fashion-MNIST analysis. This record summarizes the main interactions from our chat. The "What we asked" entries summarize the context. Prompts labeled exact preserve the original chat wording. Prompts labeled paraphrased use revised wording agreed during our review. Short follow-up prompts refer to the surrounding conversation and notebook outputs.

## 1. Finding the main prediction error

This stage developed through short follow-up requests and shared notebook outputs; the request below is a summary.

**What we asked:** Help us collect predictions, create a confusion matrix, and find the most frequent mistake.

**What AI suggested:** Compare the correct labels with the model predictions, exclude the diagonal of the confusion matrix, and find the largest remaining count.

**What we used and checked:** We used the suggested code with our shared trained weights. The output showed 177 actual shirts predicted as coats. We selected this error for further investigation and displayed examples of correctly predicted shirts and shirts predicted as coats.

## 2. Developing the sleeve hypothesis

**Paraphrased prompt**

> How could we investigate the sleeve-length hypothesis automatically?

**What we asked:** Help us investigate why some shirts were predicted as coats without manually labeling many images.

**What AI suggested:** The displayed errors suggested long sleeves as a possible explanation. AI first proposed manually labeling sleeve lengths in a random sample of 60 shirts. After we asked for an automatic approach, it suggested measuring bright pixels near the lower sides of the images.

**What we accepted and changed:** We chose the automatic approach. For each of the 1,000 actual test shirts, the code measured the fraction of pixels above 0.2 in two regions, rows 15-23 and columns 2-7 and 20-25. We split the shirts at the median coverage value.

**What we checked:** The higher-coverage group contained 494 shirts, with 149 predicted as Coat (30.2%). The lower-coverage group contained 506 shirts, with 28 predicted as Coat (5.5%). Together, these accounted for the 177 Shirt-to-Coat errors.

**Limitation we identified:** Coverage is an indirect measure. Sleeve length, clothing width, and brightness could all affect it. We kept sleeve length as a hypothesis because we did not complete manual sleeve annotations or validate an automatic sleeve detector.

## 3. Checking correct Shirt predictions

**Paraphrased prompt**

> Can the model still correctly classify a shirt as Shirt?

**What we asked:** Can higher-coverage shirts still be correctly predicted as Shirt, and what do the percentages mean?

**What AI suggested:** Count correct Shirt predictions separately within the same two coverage groups.

**What we used and checked:** We added the calculation. Correct Shirt predictions were 303/506 (59.9%) for lower coverage and 205/494 (41.5%) for higher coverage. We clarified that the earlier 5.5% and 30.2% described only Coat predictions. Other predictions included both correct Shirt labels and errors involving other categories.

## 4. Reviewing the probability analysis

**Paraphrased prompt**

> How could we improve the analysis to address the TA’s feedback?

**What we asked:** Review the updated notebook in light of feedback about probability analysis and deeper brainstorming with AI.

**What AI reviewed:** The uploaded notebook already included softmax scores for Shirt and Coat on the 177 errors, and a comparison of Coat scores across all 1,000 shirts using the coverage groups. AI reviewed this addition and suggested corrections.

**What we checked:** The notebook outputs showed an average Coat score of 66.4% and Shirt score of 17.4% on the 177 errors. Across all shirts, the average Coat score was 8.0% for lower coverage and 30.5% for higher coverage.

**What we corrected:** AI identified that NumPy was used before its import, so we moved the import to the first cell. We also changed the histogram title from "Probability Margin" to "Predicted Probabilities" because the plot displayed separate scores. We revised the conclusion to describe an association between coverage and Coat scores.

**Limitation we identified:** Softmax scores describe the model's assigned probabilities. We did not test whether those scores accurately match real-world correctness rates. Group averages also do not establish how confident every individual prediction was.

## 5. Testing overall brightness as another explanation

**Exact prompt from our chat**

> how will be study this ?

**What we asked:** How can we check whether overall brightness helps explain the coverage result?

**What AI suggested:** Calculate the mean brightness of each shirt image, divide the shirts into four brightness ranges, and compare lower and higher coverage within each range.

**What we accepted and checked:** We added the suggested cell. When Colab could not provide a runtime, our teammate ran the notebook on her machine. We reviewed the saved results and added a short conclusion.

| Overall brightness range | Lower-coverage shirts | Average Coat score | Higher-coverage shirts | Average Coat score |
| --- | ---: | ---: | ---: | ---: |
| 1 - darkest | 198 | 10.1% | 52 | 21.1% |
| 2 | 135 | 6.8% | 115 | 31.0% |
| 3 | 122 | 7.1% | 128 | 33.3% |
| 4 - brightest | 51 | 4.8% | 199 | 30.9% |

**How this affected our analysis:** Higher coverage was associated with higher Coat scores in all four brightness ranges. This suggests overall brightness alone may not explain the pattern. The ranges are broad and contain different group sizes, so this is an exploratory comparison. Sleeve length and clothing width remain possible explanations.

## 6. Understanding and reviewing AI suggestions

**Exact prompt from our chat**

> step step explain breifly cell be cell let us begin without rush cell 1

We asked AI to explain the notebook one cell at a time, clarify the percentages, and explain why training images were shuffled. We questioned suggestions when their meaning was unclear and used the code and displayed outputs to check the explanations. AI helped us develop the analysis, but we needed to check terminology and avoid presenting a possible explanation as a confirmed cause.
