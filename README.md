# Project
ML Final Project
Nichos Molnar 2025

# <a href = "https://github.com/Machine-Learning-Parsons-Fall-2025/Project/blob/main/kamon_final_notebook.ipynb">Final Notebook found here: </a>

Presented on 12/15/2025.


## Ideas:

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


### Progress Made:

- Imported images and started to process with openCV
    - learned that you usually detect a white shape on a black background in openCV
    - added border along edge of images 
    - tooled around with erosion/dilation 
- things I need to solve:
    - not all images are greyscale/go through the black/white filtering and color inverting properly
    - how much/when should I dilate/erode?


Trying to use openCV to process and detect shapes in my images. I'm running into more difficulty than expected in setting up my images for detection. I thought they would all be black and white, but apparently they're shaded, and some are not greyscale at all. The findContours() / finding the outline code that Thiago gave to me. I'm having success with some kamon, not that much with others. Many kamon have delicate or thin, low-res lines, which can get eroded away and end up "breaking" the outline of the kamon. This means there is no longer a dominant contour, and the kamon is broken up into a bunch of little shapes. I'm not sure if I want this.

I think once I punch through this image processing step, the next steps (maybe dimensionality reduction, and then K-means clustering, I think) should be more straightforward.


### Milestone 3:
- Pipeline from Kamon image -> processed contour
  - Open Kamon
  - Thresholding
    - converting images to greyscale
    - pixel insenity on 0 to 255 scale, instead of 0 to 30 (as some images were in that format)
    - add border of 10 pixels around edge
  - Dilate Kamon to "unite" small lines/shapes into overall contour
  - Search for contour
  - Validate contour
    - Not valid if:
      - has points touching the edges of the image
      - larger than 70% of the image area
      - smaller than 15% of the image area
    - around ~60% of Kamons pass
  - KMeans clustering of points for equal length contours
  - Ordering points clockwise
  - centering points (this step also scales? I think?)

This process gives me a dataframe with 3000 Kamons and their clusters. KMeans Clustering of these Kamons shows that these Kamon can be grouped into 2-5 cluters (3 clusters gives the highest Balance Score), which can be seen in the Contour_and_KMeans.ipynb notebook. It's hard to tell what the clustering algorithm is picking up on, but observing the results of n=3 clusters, it might be picking up oblong diamond contours, round contours with lumps, and round contours with fewer lumps. 

#### <u>Next Steps</u>:
  - Alternative methods of extracting features from images?
    - Lara is using CLIP model to identify features from image-description pairs. I could use the Kamon descriptions along with the image to get new features
    - Interior contours?
      - if larger contours are present within the Kamon, could use these as features
      - as not all Kamon have interior contours, could even add a "interior contour present True/False"
    - Fine tuning validation process to pick up on Kamon that don't pass muster
      - maybe decrease how big the largest contour should be 
      - dialate even more?
    - Erode Kamon into "chunks" 
      - some Kamon are made up of more than one shape. Dilating and contouring unites these shapes, but could be interesting to consider the opposite process.  
  - More ways to process features
    - PCA of contour data, and then clustering
    - maybe Classification Network (wk13?)
  - Further Machine Learning
    - t-SNE
    - dive deeper into K-Means

