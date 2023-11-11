# Instagram Account Classifier

## Overview

This project aims to classify Instagram accounts into two categories: "Individual" or "Brand/Organization". The classification is based on the analysis of the user's profile picture and biography. The code utilizes the Instaloader library for Instagram data retrieval, OpenCV for image processing, and Hugging Face's Transformers library for Named Entity Recognition (NER).

## Instaloader

Instaloader is a Python module to download pictures (or videos) along with their captions and other metadata from Instagram. In this project, Instaloader is used to retrieve an Instagram user's profile data, including information about their posts, followers, and following.


## Features

### Profile Data Retrieval

The `fetch_instagram_data(username)` function initializes an Instaloader instance and retrieves an Instagram user's profile data, including information about their posts, followers, and following.

### Profile Picture Analysis

The `analyze_profile_picture(profile)` function starts by obtaining the URL of the user's profile picture using the `get_profile_pic_url()` method. It then sends an HTTP request to retrieve the picture data. If successful, the image is decoded using OpenCV, grayscaled, and analyzed for faces using a Haar Cascade classifier. The function returns the count of faces detected in the profile photo.

### Named Entity Recognition (NER)

The `analyze_nlp_text(text)` function utilizes Hugging Face's pre-trained NER pipeline to process a text input and extract named entities. In this project, it specifically processes the user's biography and returns the identified named entities.

### Account Classification

The `classify_account(profile)` function combines the results of profile picture analysis and NER to classify the Instagram account as either "Individual" or "Brand/Organization". It first calls `analyze_profile_picture(profile)` to get the count of faces in the profile picture and then uses `analyze_nlp_text(profile.biography)` to extract named entities from the user's biography. The function returns the classification based on the presence of faces and named entities.

## Usage

1. Install the required libraries:

   ```bash
   pip install instaloader
   pip install opencv-python
   pip install requests
   pip install numpy
   pip install transformers 

## Features

### Profile Data Retrieval

The following code initializes an Instaloader instance and retrieves an Instagram user's profile data:

```python
import instaloader

def fetch_instagram_data(username):
    L = instaloader.Instaloader()
    profile = instaloader.Profile.from_username(L.context, username)
    return profile
