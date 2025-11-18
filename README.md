# Project
ML Final Project
Nichos Mol,nar 2025

## Ideas:

![Kamon Example - Toyotomi Clan](https://github.com/Machine-Learning-Parsons-Fall-2025/Project/blob/14b81d587e6fdb0950bf89d2d09328bee142b381/Kamon_Example.png)
**Japanese Kamon**:
- How does an untrained/unfamiliar person view Kamon?
- Japanese crests/emblem (Kamon) representing individuals or families (historically)
- Kamon have consistent structure and no color, and are made of shared motifts/symbols
  - kamon are traditionally classified by type (plant, animal, nature, tool, vehicle, building, etc)
  - motifs have specific meaning, and some are more popular than others
- A kamon dataset is ripe for machine learning techniques!
- Kamon datasets exist, and should be pretty easy to combine. However, these datasets are context sparse - dataset builders were likely more interested in the images themselves than the historical associations of each mon. 
  - pipe dream: enrich image dataset with historical/geographic context
  - example datasets:
    - Scrape here: https://kamondb.com/letter/45/ (unknown how large)
    - https://www.kaggle.com/datasets/bachrr/mon-white-224 (6425 total, 224x224 image size)
    - https://huggingface.co/datasets/kenthorvath/japanese-kamons (408 kamon)


<br></br>
**Revolutionary Faces**

![George Washington](https://github.com/nmolnar-parsons/revperiod_portraitfaces/blob/274fe68a33b4cafc0bb7142505a5f3c3b71087cd/Cropped_Faces/Image_0_face_0.jpg)
- How did artists depict eyes (or more generally, fatial features) in the post-revolutionary period of American History?
- Sense/extract facial features from revolutionary portraits -> unsupervised learning? 
- Building on a revolutionary period dataset used in MSDV Major Studio 1 (full dataset not linked here)
  - subset here: https://github.com/nmolnar-parsons/revperiod_portraitfaces
  - dataset size: between 158 and 3000+ images, depending on cleaning. Likely to be somewhere around 300 images once silhouettes that are classified as portraits are removed


**Something to do with mapping**
- not sure what this would be yet, but I like maps/geographical data 11/7/25



## Process:
Sticking with the Kamon dataset (scraped from KamonDB (https://kamondb.com) using Requests and BeautifulSoup4), I forged onwards. As of 11/17/2025, I have scraped and translated (using googletrans library) from Japanese to English 5360 total Kamon. Next steps:
- edge detection from Week 4
  - ideally to find similar shapes/patterns across Kamon categories
- Radial sampling/polar coordinate sampling (suggested by Thiago)
- combining text and image data? is this possible?
This dataset is entirely image and text. We have worked with image previously and are working with textual datasets in this week (11/17). 

- opencv for computer vision stuff
  - sift or search
    - finds features in image that are "descriptive"
- feature extraction
- blob (points become features)