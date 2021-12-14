# DSI25 Capstone Project

# Background and Problem Statement
Mixed Martial Arts (MMA) is currently one of the fastest, if not the fastest growing sport in the world. It's growth is hugely led by Ultimate Fighting Championship (UFC). Closer to home, we also have the One Championship that aims to emulate the success of the UFC. Either way, the sport is growing rapidly. However, it seems that usage of video for analysis is not as prevalent as in other sports such as tennis, football, American football, and such.

As such, this project aims to cover that gap, utilizing Computer Vision to analayse striking attempts by fighters. The result can then be used for a variety of use-case such as assistive CV tool for judges or even to analyse fighter's techniques. For this project, we will focus on the former.

45% of fights in the UFC ends in Decision, which means both fighters last through 3 or 5 rounds, leaving the judges to decide on the eventual winner. It can be tricky for the judges to score the rounds especially when both fighters are equally matched up. There is bound to be some subjectivity involved. As such, this assistive CV tool can potentially bring some objectivity in the decision-making process.

---
# Executive Summary
Frames of different types of MMA strikes were collected from Youtube and edited using Davinci Resolve to mask the fighters such that only one person can be inside the frame. This is to allow for pose estimation to be applied, which will be discussed furrther later.

OpenCV and Mediapipe were used together to extract pose estimation keypoint values for these frames. The angles were then computed from these keypoint values. The keypoint values themselves were excluded as it were deemed to bring too much 'noise' to the modelling. Also, by having 99 additional keypoint features, it may lead to overfitting.

These angle values were converted into a dataframe and PyCaret was used to classify the different strikes.
- right high kick
- left high kick
- right low kick
- left low kick
- right punch
- left punch

PyCaret produced the following as the top 3 models:
1. Extra Tree Classifiers
2. Extreme Gradient Boosting
3. Light Gradient Boosting

The decision was made to use the Extra Trees Classifier as the final model.
The data set was train/test split by 0.7/0.3.
With the train set, the model achieved accuracy of 0.95 and F1 of 0.95.
With the test set, the model achieved accuracy of 0.93 and F1 of 0.93.
This shows that the model is capable of correctly classifying the different types of strikes using angles alone.

---

## Data Dictionary


|        Variable Name                |    Data Type   |        Description         |
|:-----------------------------------:|:--------------:|:--------------------------:|
|         right_elbow_angle           |      float     |angle of right elbow        |
|         right_shoulder_angle        |      float     |angle of right shoulder     |    
|         right_hip_angle             |      float     |angle of right hip          |
|         right_knee_angle            |      float     |angle of right knee         |
|         right_ankle_angle           |      float     |angle of right ankle        |
|         left_elbow_angle            |      float     |angle of left elbow         |
|         left_shoulder_angle         |      float     |angle of left shoulder      |
|         left_hip_angle              |      float     |angle of left hip           |
|         left_knee_angle             |      float     |angle of left knee          |
|         left_ankle_angle            |      float     |angle of left ankle         |
|         attack_type                 |   categorical  |label of type of strike     |



---

# Conclusion and Recommendation

In conclusion ,the model was able to successfully classify different types of strikes using Computer Vision and Pose Estimation, with very high accuracy and other metrics.
