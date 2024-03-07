# DLW-Hackathon-Tiktok-Pipeline
Submission for NTU's MLDA Deep Learning Week (DLW) Hackathon, for the Tiktok problem statement


## Problem Statement
- To create a data filtering pipeline that could remove low-quality text-video pairs from the dataset and thus improve video generation quality with less cost of model training.

## Approach
- Loading and Parsing given Json data
- Automating the Download of videos using YTDL
- Splitting the Youtube videos according to timestamps given using provided Python script
- Using State-of-the-Art (SOTA) Video Captioning model Video-ChatGPT to generate a "groundtruth" caption
  - VideoChatGPT combines a pretrained visual encoder using CLIP, and a LLM (LLaVA-7B-Lightening-v1-1). We obtain the latter from HuggingFace.
  - VideoChatGPT obtains SOTA performance on several video captioning benchmarks, such as VideoInstruct (paperswithcode.com/sota/video-based-generative-performance?p=video-chatgpt-towards-detailed-video)
- Generating a semantic similarity score between the groundtruth caption generated in the previous step, against the provided caption from the noisy TikTok dataset. We use another model (a wrapper around ChatGPT3.5-turbo) to do so. The approach is based on the paper Quantitative Evaluation Framework for Video-based Conversational Models, 2023
  - Other metrics were considered (such as n-grams matching/overlap), but we focus on semantic similarity instead of syntatic similarity. This is important as there are >1 ways to express the same idea in natural language, therefore syntatic similarity metrics are not a good method to evaluate the provided caption.
- Sorting and Filtering the provided dataset of 1M captions, to retain the top 10% based on the scoring metric above
  - This was not implemented due to constraints of time and computation. A toy example of 4 video snippets are provided instead, to illustrate the pipeline and scoring metrics above

## Team Members:
- Ng Zheng Xun (CSC Y4)
- Kevin Hu (EEE Masters)
- Lyu XingXiao (EEE Masters)


## Additional Links:
Submission on DevPost: https://devpost.com/software/tiktok-data-pipeline-team-xponential
Youtube Video: https://youtu.be/yRsulorvWWE
