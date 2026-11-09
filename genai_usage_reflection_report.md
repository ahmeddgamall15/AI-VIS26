# AI Interaction Record — Phase 1

This log summarizes how we used GenAI while working on Phase 1, moving from identifying the model's main error bottleneck to testing our sleeve hypothesis and running the probability checks from Lecture 2.

### 1. Finding the Main Error Bottleneck

* **What we wanted to do:** We needed to see where our CNN was struggling the most on Fashion-MNIST instead of just looking at the overall accuracy score.

* **Prompting the AI:** We asked the AI to look at the test set predictions, generate a confusion matrix, and pull out the pair of classes with the highest number of mistakes.

* **What the AI gave us:** It identified that 177 shirts were incorrectly classified as coats (Shirt = class 6, Coat = class 4) and gave us code to filter out those specific images.

* **What we did / verified:** We plotted some of those misclassified shirts alongside shirts the model got right. Looking at them side-by-side made it obvious that the shape and silhouette of certain shirts were throwing the model off, rather than completely random image corruption.

### 2. Formulating the "Lower Lateral Coverage" Proxy

* **What we wanted to do:** After looking through shirts in the dataset, we noticed that shirts predicted as coats often had longer sleeves or wider bodies. We wanted a concrete way to measure this without having to manually label hundreds of images.

* **Prompting the AI:** We brainstormed with the AI on how to capture outer sleeve presence on a 28×28 grayscale grid using simple NumPy slicing.

* **What the AI gave us:** It suggested cropping the lower-side borders—specifically rows 15 to 23 and columns 2–7 (left) and 20–25 (right)—and summing up the pixel intensities. It also provided code to split the 1,000 test shirts at the median into "lower coverage" (506 images) and "higher coverage" (494 images).

* **What we did / verified:** We manually inspected a grid of 60 shirts to check if this metric actually matched what human eyes see as longer sleeves. While it worked well in general, we noticed that lighter-colored shirts or broader silhouettes also increased the brightness score. Because of that, we made sure to write an explicit note in our notebook stating that this is an intensity proxy, not a real sleeve segmentation tool.

### 3. Adding Softmax Probability Analysis (Feedback)

* **What we wanted to do:** Our instructor pointed out that relying only on discrete counts from a confusion matrix wasn't enough, and that we needed to look at conditional probabilities and uncertainty as discussed in Lecture 2.

* **Prompting the AI:** We asked the AI how to extract the raw softmax output values from our PyTorch model and visualize prediction confidence on the 177 mistakes, as well as how $P(\text{Coat})$ changes across all test shirts based on our coverage split.

* **What the AI gave us:** It provided the code to extract softmax scores, plot a histogram of the probability margins for the error cases, and draw a boxplot comparing $P(\text{Coat})$ between low- and high-coverage shirts.

* **What we did / verified:** We ran the code locally with our saved weights (`fashion_cnn.pth`) to verify the numbers. The results showed that the model wasn't making close 50/50 guesses on the 177 mistakes—it was confident, giving Coat an average of 66.4% and Shirt only 17.4%. Across all 1,000 shirts, higher side coverage pushed the average $P(\text{Coat})$ from 8.0% up to 30.5%, confirming that this visual feature systematically shifts the model's confidence.