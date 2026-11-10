# Midpoint Reflection on GenAI Usage — Phase I

**AI-assisted pair (Pair A):**

- Omar Ibrahim — Student ID: k12406569
- Ruqaya Mubarak — Student ID: K12007247

## How we used GenAI

We used ChatGPT to help us investigate the behavior of our shared Fashion-MNIST CNN. We treated the model as a black box and studied its predictions and softmax scores. AI helped us write analysis cells, create visualizations, develop questions, and understand the results. We also used it to help draft this reflection and summarize the important interactions in our interaction record.

## What helped us

AI helped us move from finding an error to investigating a possible explanation. The confusion matrix showed that the largest individual error was Shirt predicted as Coat, with 177 examples. After looking at images, we considered whether long sleeves might be related to this mistake.

AI first suggested manually labeling sleeve lengths. We chose an automatic alternative: measuring the fraction of bright pixels near the lower sides of each of the 1,000 test shirts. The higher-coverage group had more Coat errors than the lower-coverage group (30.2% versus 5.5%). Checking correct Shirt predictions separately also helped us understand that the remaining shirts were not necessarily classified correctly.

After the TA's feedback, we reviewed the probability analysis and investigated overall brightness as another possible explanation. Higher-coverage shirts received higher average Coat scores within all four brightness ranges. This helped us go beyond a confusion matrix and ask a further question about the pattern.

## What needed care and checking

The main difficulty was understanding exactly what the measurements meant. Pixel coverage is not a direct measurement of sleeve length. Clothing width, brightness, and other image details can affect it. We therefore kept long sleeves as a possible explanation rather than a confirmed cause.

We also needed to distinguish error percentages from average softmax scores. For example, 30.2% was the percentage of higher-coverage shirts classified as Coat, while 30.5% was their average Coat score. Softmax scores are the model's assigned probabilities; we did not test their calibration.

Working code alone was not enough to understand the analysis. We asked for short explanations, questioned unclear statements, and went through the cells step by step. During review, we moved the NumPy import before its first use, corrected a plot title that said "Probability Margin" although it showed separate probabilities, and revised wording that could imply causation. When Colab could not provide a runtime, a teammate ran the notebook locally, and we reviewed the saved outputs.

## Decisions we made

We accepted AI's suggestions for visualizations and calculations after checking the outputs. We changed the manual-labeling plan to an automatic pixel measure, while acknowledging that it could not directly test sleeve length. We also limited our conclusion to an association between coverage and model behavior. The brightness comparison provides additional evidence, but broad brightness ranges do not fully control for brightness or rule out other explanations.

## Comparison with the non-AI analysis

Both pairs used the same trained weights and test data and found the same 177 Shirt-to-Coat errors. Pair B measured average brightness in the side regions, while we measured the fraction of pixels above a threshold. Their brighter-side group had a Coat error rate of 29.0%, compared with 6.4% for their less-bright group. Both approaches therefore showed a similar direction of association, although the measurements and group memberships differed.

Our notebook also compared coverage groups within four ranges of overall brightness. The notebook results allow us to compare the analyses, but they do not show how much time each pair spent or prove that AI produced a better outcome.

## What we learned

GenAI was useful for suggesting next questions, writing code, and explaining unfamiliar concepts. However, it could move the analysis forward faster than we understood it. Our main lesson was to ask what each measurement actually represents and check whether the conclusion is supported by the output. For the next phase, we will continue using small, specific questions, reviewing each suggested step, and separating observations from possible explanations.
