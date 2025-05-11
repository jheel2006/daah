---
title: "Assignment 3"
date: 2025-05-10
categories: 
  - Assignment
tags:
  - 
  - 
---
# Analyzing Teenage/Young Adult Book Covers

## Image Dataset

[**Click here to view the image dataset on Google Drive**](https://drive.google.com/drive/folders/1mQ4RD0AYxqcl08ynx9fue_wjwER5Irhg?usp=sharing)

For this assignment, we chose to work with a dataset of teenage and young adult book covers sourced from Kaggle. I’ve always found book cover design intriguing—especially in the YA genre, where visual cues like typography, color palettes, and illustration styles often hint at the book’s mood, genre, and target audience. The covers tend to blend photography, digital painting, and bold design choices, making them a rich site for visual analysis. We selected 111 book covers that clearly fit the young adult category. This dataset felt like a strong match for the goals of the project because YA covers often follow recognizable patterns, while still allowing space for variety and nuance.

## Clustering and Visual Exploration in Orange Data Mining

Once the images were prepared, we loaded them into Orange Data Mining using the provided workflow. The first model we used for clustering was InceptionV3, which offered a fairly balanced distribution of the covers across the image plot. 

<!-- CHECKPOINT: Insert Inception Image -->
![Image Grid - Inception Model](https://github.com/user-attachments/assets/da1f0b3a-5851-4ef2-97e3-ffc9bca8b79d)

However, when we tried using OpenFace, the model didn’t detect any of the images. We also faced technical issues with the VGG model, as it wouldn’t download correctly on our system. To continue exploring, we turned to SqueezeNet—an offline model—which gave decent results and allowed us to compare how different models "see" the same dataset.

<!-- CHECKPOINT: Insert Squeezenet Image -->
![Image Grid - SqueezeNet](https://github.com/user-attachments/assets/202e05f6-5d0e-4f1e-8b2a-d6e5e0220b45)


One interesting experiment involved a model called Painter, which is trained on paintings. Even though it is not specifically designed for book covers, the visual similarities between painted compositions and some cover art made this a surprisingly effective choice. The Painter model tended to cluster covers by dominant color tones, and in several cases, even grouped images featuring animals or similar stylistic features. This opened up a new way of thinking about how artistic structure might influence the design of YA literature.

<!-- CHECKPOINT: Insert Painter Image -->
![Image Grid - Painter](https://github.com/user-attachments/assets/dae94cb5-e75b-4874-a8ae-aa2f8f27bcb5)


Another unexpected but fascinating model was Deeploc, which is actually trained on microorganism imagery. Despite its unrelated training data, it produced one of the most visually coherent image plots—especially in terms of brightness and contrast. Covers arranged themselves in a smooth gradient from dark to light, revealing how even a model trained outside the realm of cultural imagery can pick up on aesthetic patterns.

<!-- CHECKPOINT: Insert DeepLoc Image -->
![Image Grid - Deeploc](https://github.com/user-attachments/assets/d6ec7526-c1ea-4620-9b2b-c67caa82c099)


What struck me most was how these models, although not trained specifically on book covers, still revealed meaningful groupings. This reinforces the idea from Impett & Offert that in reading a corpus through a neural network, we are also reading the network itself. Each model brought its own visual vocabulary to the task, and seeing which features it emphasized—color, texture, brightness—made me more aware of the visual language embedded in YA cover design. The differences between the clusters, and the moments when a cover seemed “misplaced,” were often where the most insight came from. As Arnold and Tilton argue in *Distant Viewing*, computer vision models only capture surface-level visual features, and never the full meaning of an image. Their emphasis on analyzing patterns across large image sets—rather than relying on individual tags or annotations—helped us interpret the groupings in a more thoughtful way. For instance, seeing how the models clustered by brightness or color reminded us that we’re not just seeing the images—we’re also seeing what the model is capable of recognizing.


## Hierarchical Clustering

![Heirachial Clustering](https://github.com/user-attachments/assets/4f4dde8e-cc5f-4fca-b2da-bbb47496d7e4)


Most of the covers in our dataset were scattered across the hierarchical clustering tree, often grouped in pairs or small clusters. But there was one cluster that stood out because it had a noticeably larger group of books grouped tightly together. Naturally, we were curious to see what these books had in common, so we gathered the covers from that section to look more closely. It quickly became clear why the model had grouped them—they shared a lot of strong visual similarities. Most of these covers featured a cartoon-like illustration style, with bold outlines and minimal detail, like *Diary of a Wimpy Kid*, *The World’s Worst Children*, and *Brain Games for Clever Kids*. They also used bright, flat colors like red, yellow, and blue, which likely caught the model’s attention since dominant color areas often guide clustering. Many had a similar composition as well—large centered text, a character or object in the middle, and not much else going on in the background. Even though the model doesn’t actually "know" what a children’s book is, the visual tone across these covers was clearly similar enough for it to group them. This cluster was a good reminder that models often pick up on surface-level design traits—like layout, color, and illustration style—more than content or meaning.

![Hierarchical Clustering Books](https://github.com/user-attachments/assets/51c6db1f-fb10-4699-ba6e-14e0c2a53101)

![HC - Isolating Specific Cluster](https://github.com/user-attachments/assets/92e9fc72-503b-4331-aa3f-ee561170bb4f)


## Analyzing Confusion Matrices

For the classification portion of the assignment, we created two different category systems and generated confusion matrices using Orange Data Mining. The first classification system was based on the overall **color tone** of the book covers. We divided them into three categories: bright-colored covers (32 images), dark-colored covers (28 images), and pastel-toned covers (40 images). Coming up with these categories wasn’t easy—many covers combined multiple color styles, making it hard to place them definitively. Still, we tried to stay consistent and used our own visual judgment to assign each image.

Using the Inception model, the results were fairly strong. The confusion matrix showed that the model had a particularly high accuracy for the "Dark" and "Pastel" categories, with 21 and 33 correct classifications out of 28 and 40 respectively. Most of the confusion occurred between "Bright" and "Pastel" covers—ten pastel-toned covers were predicted as bright, and seven bright ones were misread as pastel. This made sense after looking more closely—many pastel covers include bold text or colorful elements that might resemble "bright" features, and vice versa. The dark-toned covers, on the other hand, were much more consistent and distinct, which probably made them easier for the model to identify. Seeing which images were misclassified made us rethink how cleanly separable these categories really are—even to a human eye.

<!-- CHECKPOINT: Insert Inception Confusion Matrix Image -->
![Confusion Matrix - Inception](https://github.com/user-attachments/assets/362d2db3-55aa-472b-b4f8-272d8f532dfc)


We also ran the same classification using the Painter model, and the results shifted in interesting ways. This time, the confusion between “Bright” and “Dark” became more noticeable. For example, seven bright covers were misclassified as dark, and six dark ones were predicted as bright. Unlike Inception, which seemed to get tripped up more between soft tones and bolder ones, the Painter algorithm appeared to weigh composition and contrast more heavily—possibly due to its training on art. That could explain why the lines between high-contrast bright covers and shadow-heavy dark ones became less clear. This reinforces what *Distant Viewing* by Arnold & Tilton emphasizes: our human ways of grouping things often don’t align with how machines calculate similarity. These experiments don’t just reveal what the models can or can’t do—they push us to think more carefully about the categories we take for granted and how those are shaped by cultural context rather than just visual data.

<!-- CHECKPOINT: Insert Painter Confusion Matrix Image -->
![Confusion Matrix - Painters Model](https://github.com/user-attachments/assets/186ba8e8-a7f3-483d-b6e7-4de0df9c4385)



For the second classification system, we organized the covers based on whether or not a **character** appeared on them. This gave us two roughly equal groups: 56 covers with a visible character and 55 without. We ran the classification using both the Inception and Painter models. Between the two, the Inception model clearly performed better, correctly classifying 83 out of 111 images. The confusion matrix shows a relatively balanced prediction, with fewer mix-ups between the “characters” and “no-characters” categories. In contrast, the Painter model struggled more—likely due to its training on artworks, where the presence of figures is often more abstract or stylized. It misclassified 44 images, often confusing minimal silhouettes or decorative elements for characters. While it was possible to expect Painter to do better given its background, the results highlight how a model trained on fine art doesn’t always transfer well to more graphic and commercially styled designs like book covers. This again underscores how much the training context of a model influences its perception of seemingly straightforward features.

<!-- CHECKPOINT: Insert Inception/Painter Confusion Matrix Image -->
![Confusion Matrix - Inception Model](https://github.com/user-attachments/assets/6f776f2d-d3e4-4e6d-a7fd-d1548f88c67d)

![Confusion Matrix - Painters Model (2)](https://github.com/user-attachments/assets/4d3968c2-be70-4b55-81c3-672f361f468f)

In both sets of categories, we tried moving some images around to test how much that would impact the results. Ultimately, the original groupings provided the most meaningful insights, and those are the ones shown in the screenshots we’ve included. The confusion matrices, particularly for the color-based categories, offered a useful window into how the model “sees” the images—and how that vision differs from mine.

Reflecting on these outcomes through the lens of *Distant Viewing*, I started to see how much my initial categories were shaped by subjective, aesthetic choices. What looks like a "pastel" to me is, to the model, just a set of pixel values. The algorithm forces me to step outside my own logic and confront the limits of visual categorization when it's translated into machine terms. These mismatches don’t just reveal where the model struggles—they also ask us to reconsider how reliable our own classification systems really are.

## DV Explorer: Zero Shot

For the multimodal part of the assignment, we explored the **Zero Shot** tool in DV Explorer. This tool allows you to upload your entire image set and then search with free-form text prompts. It ranks the images based on how well they match the description, using similarity scores. We tested several prompts such as *"mystery magic adventure," "crime thriller," "happy kids books," "romantic books," "books where random creatures exist," "birds," "dark covers,"* and *"pastel covers."* The results were surprisingly effective—even when the similarity scores were close to zero, many of the images returned still felt like accurate matches. For example, the prompt *"mystery magic adventure"* brought up Harry Potter and Percy Jackson covers, while *"romantic books"* highlighted titles like *To All the Boys I've Loved Before* and *The Fault in our Stars*. The model seemed to pick up on visual patterns, color schemes, and even font styles that matched the keywords we typed in. It was interesting to see how well the tool understood abstract ideas like “romance” or “magic” without any prior training on our specific dataset. This exercise showed how the words we use can really change the way we look at and understand images.

![DV Explorer Zero Shot model](https://github.com/user-attachments/assets/6a82a70e-ebf4-4f61-bf6a-5e825e5e8006)

![DV Explorer Zero Shot model (2)](https://github.com/user-attachments/assets/d72e2b9e-0900-422b-a2fa-5240233b1be4) 

![DV Explorer Zero Shot model (3)](https://github.com/user-attachments/assets/02fca8c1-c608-4ebd-b4b5-b7890f046e78)

![DV Explorer Zero Shot model (4)](https://github.com/user-attachments/assets/af793138-3de7-4bf0-af68-338ed51f8ba0)

## DV Explorer: Image Captioning

We also tested the **Image Captioning** tool in DV Explorer, which tries to generate short captions for each image. The results were sometimes accurate but often very off. For example, the cover of *Wonder* was described as “a cartoon of a bear with a picture of a man on it,” and *Six of Crows* was labeled “a painting of a bear with a sign on it.” It was interesting (and kind of funny) how often the model mentioned bears, even when there weren’t any. 

![Screenshot 2025-05-11 170512](https://github.com/user-attachments/assets/7eb74be9-6413-47fd-b56b-db862f9611b0)

![Screenshot 2025-05-11 174827](https://github.com/user-attachments/assets/e7e41a09-59af-4c3a-b861-ec853bd1d552)

![Screenshot 2025-05-11 174657](https://github.com/user-attachments/assets/0159dfae-cb76-4ca9-a729-587554bf451a)

![Screenshot 2025-05-11 174512](https://github.com/user-attachments/assets/1337a528-3a17-474a-b49f-e22a9b5d558a)

It also seemed to recognize things like fire hydrants or cats even if there was just fire or dark shapes. In general, the tool did better when the cover included real people or photo-like elements, but struggled a lot with illustrated or abstract designs. This made us think that the model is probably trained more on real-world photos than on stylized or drawn content like book covers.

### Examples of (decently) accurate captions:

A few of the generated captions were surprisingly accurate or at least close enough to make sense. For example, the caption for *To All the Boys I’ve Loved Before* was “a woman sitting on a bed with a book,” which is a good description of the cover. *P.S. I Still Love You* was labeled “a woman is standing in front of a sign,” which also somewhat fits the layout and pose. The cover of *All the Bright Places* was described as “a collage of a couple of different colored stickers on a white paper”—not perfect, but still a fair guess based on the design. Even *The Assassin’s Blade* being described as “a man in a black suit with a pirate theme” feels like a reasonable interpretation, even though the character is a woman. These moments showed that the model can sometimes pick up on the overall setting, layout, or vibe of the image, especially when the design is straightforward or photo-based.


![Screenshot 2025-05-11 180042](https://github.com/user-attachments/assets/7256c445-94fe-483c-b562-1ceaa5d16dac)

![Screenshot 2025-05-11 180104](https://github.com/user-attachments/assets/731679b4-6b94-42a7-a961-b6e810c273ce)

![Screenshot 2025-05-11 180204](https://github.com/user-attachments/assets/e94f9a2d-c2c9-48f0-ae06-cbc7f168edd4)

![Screenshot 2025-05-11 180219](https://github.com/user-attachments/assets/1e30326e-25cc-4afe-95ad-62c8064ed1cd)

![Screenshot 2025-05-11 180256](https://github.com/user-attachments/assets/33c698cc-c367-457f-a3c7-48ef868eaed9)

### Examples of completely inaccurate (but interesting) captions:

Some of the captions generated were completely off, which made the results both funny and surprising. For example, the cover of *Harry Potter and the Half-Blood Prince* was described as “a painting of a man with a fire hydrant,” probably because the swirling fire effects were mistaken for something else. *The Fault in Our Stars* was labeled as “a sign for a food stand with a picture of a dog,” which had nothing to do with the actual image or theme. *Paper Towns* was captioned as “a red and white fire hydrant on a table,” even though it’s a red push pin but it also makes sense why the model might mistake it for a fire hydrant. These examples show how the model often defaults to certain repeated objects when it can’t fully make sense of the visual content. This makes it seem like the model is trained mostly on real-world photos, so when it sees stylized or abstract book cover art, it tries to fit those images into categories it already knows.


![Screenshot 2025-05-11 170531](https://github.com/user-attachments/assets/b07820dc-1e50-479d-86da-83243bda62cb)

![Screenshot 2025-05-11 180124](https://github.com/user-attachments/assets/cbe8c351-dbb3-42e8-8ddf-74cd9c2ac2fa)

![Screenshot 2025-05-11 180841](https://github.com/user-attachments/assets/3b1bdc17-f6e1-405e-8c83-8ff0af7207f8)

![Screenshot 2025-05-11 180820](https://github.com/user-attachments/assets/c24de88d-9702-457e-967a-d3dbef4afc41)

## Conclusion

Working with this dataset of young adult book covers gave us a new appreciation for how machine learning models interpret visual content. Even though many of the tools weren’t trained specifically on book covers, they still found patterns—especially when it came to color, composition, and contrast. Through tools like Orange Data Mining and DV Explorer, we could see how models clustered, categorized, and captioned the images based on features we may not have noticed ourselves. At the same time, the mistakes the models made reminded us that visual understanding is complex, and often deeply tied to cultural knowledge that these systems don’t have. The idea of *distant viewing*, where we step back and look at broad patterns across many images, helped us think about this project not just in terms of what we saw, but in terms of how the models see. It also made us more aware of how we form our own categories, and how different that process is from what algorithms do.

## References

- [Kaggle. (n.d.). *Book Covers Dataset*](https://www.kaggle.com/datasets/lukaanicin/book-covers-dataset)  
- [Arnold, T., & Tilton, L. (2023). *Distant Viewing: Computational Exploration of Digital Images*. The MIT Press](https://doi.org/10.7551/mitpress/14046.001.0001)  
- [Impett, L., & Offert, F. (2024). "There Is a Digital Art History."](https://www.tandfonline.com/doi/full/10.1080/01973762.2024.2362466#d1e113)  
