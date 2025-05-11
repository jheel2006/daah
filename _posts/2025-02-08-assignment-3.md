---
title: "Assignment 3"
date: 2025-05-11
categories: 
  - Assignment
tags:
  - 
  - 
---

# Analyzing Teenage/Young Adult Book Covers

## Image Dataset

For this assignment, we chose to work with a dataset of teenage and young adult book covers sourced from Kaggle. I’ve always found book cover design intriguing—especially in the YA genre, where visual cues like typography, color palettes, and illustration styles often hint at the book’s mood, genre, and target audience. The covers tend to blend photography, digital painting, and bold design choices, making them a rich site for visual analysis. We selected 111 book covers that clearly fit the young adult category. This dataset felt like a strong match for the goals of the project because YA covers often follow recognizable patterns, while still allowing space for variety and nuance.

## Clustering and Visual Exploration in Orange Data Mining

Once the images were prepared, we loaded them into Orange Data Mining using the provided workflow. The first model we used for clustering was InceptionV3, which offered a fairly balanced distribution of the covers across the image plot. 

<!-- CHECKPOINT: Insert Inception Image -->

However, when we tried using OpenFace, the model didn’t detect any of the images. We also faced technical issues with the VGG model, as it wouldn’t download correctly on our system. To continue exploring, we turned to SqueezeNet—an offline model—which gave decent results and allowed us to compare how different models "see" the same dataset.

<!-- CHECKPOINT: Insert Squeezenet Image -->

One interesting experiment involved a model called Painter, which is trained on paintings. Even though it is not specifically designed for book covers, the visual similarities between painted compositions and some cover art made this a surprisingly effective choice. The Painter model tended to cluster covers by dominant color tones, and in several cases, even grouped images featuring animals or similar stylistic features. This opened up a new way of thinking about how artistic structure might influence the design of YA literature.

<!-- CHECKPOINT: Insert Painter Image -->

Another unexpected but fascinating model was Deeploc, which is actually trained on microorganism imagery. Despite its unrelated training data, it produced one of the most visually coherent image plots—especially in terms of brightness and contrast. Covers arranged themselves in a smooth gradient from dark to light, revealing how even a model trained outside the realm of cultural imagery can pick up on aesthetic patterns.

<!-- CHECKPOINT: Insert DeepLoc Image -->

What struck me most was how these models, although not trained specifically on book covers, still revealed meaningful groupings. This reinforces the idea from Impett & Offert that in reading a corpus through a neural network, we are also reading the network itself. Each model brought its own visual vocabulary to the task, and seeing which features it emphasized—color, texture, brightness—made me more aware of the visual language embedded in YA cover design. The differences between the clusters, and the moments when a cover seemed “misplaced,” were often where the most insight came from.

## Hierarchical Clustering

## Analyzing Confusion Matrices

For the classification portion of the assignment, we created two different category systems and generated confusion matrices using Orange Data Mining. The first classification system was based on the overall **color tone** of the book covers. We divided them into three categories: bright-colored covers (32 images), dark-colored covers (28 images), and pastel-toned covers (40 images). Coming up with these categories wasn’t easy—many covers combined multiple color styles, making it hard to place them definitively. Still, we tried to stay consistent and used our own visual judgment to assign each image.

Using the Inception model, the results were fairly strong. The confusion matrix showed that the model had a particularly high accuracy for the "Dark" and "Pastel" categories, with 21 and 33 correct classifications out of 28 and 40 respectively. Most of the confusion occurred between "Bright" and "Pastel" covers—ten pastel-toned covers were predicted as bright, and seven bright ones were misread as pastel. This made sense after looking more closely—many pastel covers include bold text or colorful elements that might resemble "bright" features, and vice versa. The dark-toned covers, on the other hand, were much more consistent and distinct, which probably made them easier for the model to identify. Seeing which images were misclassified made us rethink how cleanly separable these categories really are—even to a human eye.

<!-- CHECKPOINT: Insert Inception Confusion Matrix Image -->

We also ran the same classification using the Painter model, and the results shifted in interesting ways. This time, the confusion between “Bright” and “Dark” became more noticeable. For example, seven bright covers were misclassified as dark, and six dark ones were predicted as bright. Unlike Inception, which seemed to get tripped up more between soft tones and bolder ones, the Painter algorithm appeared to weigh composition and contrast more heavily—possibly due to its training on art. That could explain why the lines between high-contrast bright covers and shadow-heavy dark ones became less clear. Again, this reinforces what *Distant Viewing* emphasizes: our human ways of grouping things often don’t align with how machines calculate similarity. These experiments don’t just reveal what the models can or can’t do—they push us to think more carefully about the categories we take for granted and how those are shaped by cultural context rather than just visual data.

<!-- CHECKPOINT: Insert Painter Confusion Matrix Image -->


For the second classification system, we organized the covers based on whether or not a **character** appeared on them. This gave us two roughly equal groups: 56 covers with a visible character and 55 without. We ran the classification using both the Inception and Painter models. Between the two, the Inception model clearly performed better, correctly classifying 83 out of 111 images. The confusion matrix shows a relatively balanced prediction, with fewer mix-ups between the “characters” and “no-characters” categories. In contrast, the Painter model struggled more—likely due to its training on artworks, where the presence of figures is often more abstract or stylized. It misclassified 44 images, often confusing minimal silhouettes or decorative elements for characters. While it was possible to expect Painter to do better given its background, the results highlight how a model trained on fine art doesn’t always transfer well to more graphic and commercially styled designs like book covers. This again underscores how much the training context of a model influences its perception of seemingly straightforward features.

<!-- CHECKPOINT: Insert Inception/Painter Confusion Matrix Image -->


In both sets of categories, we tried moving some images around to test how much that would impact the results. Ultimately, the original groupings provided the most meaningful insights, and those are the ones shown in the screenshots we’ve included. The confusion matrices, particularly for the color-based categories, offered a useful window into how the model “sees” the images—and how that vision differs from mine.

Reflecting on these outcomes through the lens of *Distant Viewing* by Arnold & Tilton, I started to see how much my initial categories were shaped by subjective, aesthetic choices. What looks like a "pastel" to me is, to the model, just a set of pixel values. The algorithm forces me to step outside my own logic and confront the limits of visual categorization when it's translated into machine terms. These mismatches don’t just reveal where the model struggles—they also ask us to reconsider how reliable our own classification systems really are.

## DV Explorer: Zero Shot

For the multimodal part of the assignment, we explored the **Zero Shot** tool in DV Explorer. This tool allows you to upload your entire image set and then search with free-form text prompts. It ranks the images based on how well they match the description, using similarity scores. We tested several prompts such as *"mystery magic adventure," "crime thriller," "happy kids books," "romantic books," "books where random creatures exist," "birds," "dark covers,"* and *"pastel covers."* The results were surprisingly effective—even when the similarity scores were close to zero, many of the images returned still felt like accurate matches. For example, the prompt *"mystery magic adventure"* brought up Harry Potter and Percy Jackson covers, while *"romantic books"* highlighted titles like *To All the Boys I've Loved Before* and *The Fault in our Stars*. The model seemed to pick up on visual patterns, color schemes, and even font styles that matched the keywords we typed in. It was interesting to see how well the tool understood abstract ideas like “romance” or “magic” without any prior training on our specific dataset. This exercise showed how the words we use can really change the way we look at and understand images.


## DV Explorer: Image Captioning

We also tested the **Image Captioning** tool in DV Explorer, which tries to generate short captions for each image. The results were sometimes accurate but often very off. For example, the cover of *Wonder* was described as “a cartoon of a bear with a picture of a man on it,” and *Six of Crows* was labeled “a painting of a bear with a sign on it.” It was interesting (and kind of funny) how often the model mentioned bears, even when there weren’t any. 



It also seemed to recognize things like fire hydrants or cats even if there was just fire or dark shapes. In general, the tool did better when the cover included real people or photo-like elements, but struggled a lot with illustrated or abstract designs. This made us think that the model is probably trained more on real-world photos than on stylized or drawn content like book covers.

