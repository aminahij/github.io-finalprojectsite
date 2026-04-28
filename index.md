---
# Do not edit the text between these lines!
layout: default
---

# COMP110 FINAL PROJECT (Leamsy Leon + Aminah Imran) 


## Introduction

For our final COMP110 exercise, we analyzed data collected from a student survey to explore ways in which to improve the course that are beneficial to its stakeholders (i.e. students, instructional team, academic institution and societal workforce). To begin, we brainstormed several ideas (listed below) on how to improve the course.

1. The course should implement recitations because it will give students a chance to review the content they learn every week in a more personal, classroom environment. # least analyzable
2. The course should implement different sections for different majors because it will work towards their strengths. # mentioned in survey somehow
3. The course should implement pre-class readings so students have a better understanding of what they will be doing in class. # pre class videos were mentioned in questions
4. The course should make a fun app that will enable students to learn and review the content in a more interactive way. # survey asked a lot about social media/technology use
5. The course slides should be more descriptive and contain more examples that will better aid students who are visual or linguistic learners. # mentioned in survey?


When we finished brainstorming, we went back to the data from the survey and evaluated which ideas it could support. We concluded that the idea of adding recitations cannot be fully analyzed because there is no current data showing whether recitations improve student performance or understanding in this course. 


To collect this data in the future, we could add a question to the student survey that inquires about their experiences in courses that include recitations and whether or not they believe recitations improve their learning. Additionally, we could experiment with offering optional recitation sessions and compare the performance and feedback of students who attend these sessions versus those who do not. 


From there, we chose to analyze the idea of implementing pre-class readings because there is existing data related to similar resources, such as pre-lecture videos, making it more feasible to analyze. Additionally, this idea has strong potential to improve student preparedness and engagement with relatively minimal changes to the course structure. 


## Analysis

To analyze whether pre-class readings could be beneficial, we examined three related variables from the dataset: "own_examples," "pre_lecture_videos," and "qz_effective." 


We selected these variables because: 


"pre_lecture_videos" serves as a proxy for pre-class readings, since both are preparatory materials. 

"own_examples" reflects how actively students engage with the material. 

"qz_effective" indicates whether study-related activities are helpful for learning. 


Before beginning our analysis, we previewed the dataset to better understand its structure. 


We then processed the data by combining survey datasets, selecting relevant columns, and converting values from strings to integers for numerical analysis. After cleaning the data, we calculated the frequency of responses for each variable. 


We visualized the data using bar plots, since the variables are based on Likert scale responses (1–7), which are categorical in nature. 


The bar plots show that both "pre_lecture_videos" and "qz_effective" have negatively skewed distributions, meaning most responses are concentrated at higher values (6–7). This suggests that students generally find pre-lecture videos and quiz preparation helpful for their learning. 


In contrast, "own_examples" has a more centered distribution, with many responses in the middle range (3–5). This indicates that students are less consistent in creating their own examples when learning new concepts. 


These patterns suggest that while students value structured learning resources (such as videos and quizzes), they may be less likely to independently engage in deeper learning strategies like creating their own examples. 

The code we wrote to complete this analysis can be found below. There are comments scattered throughout, explaining how some lines of code work and their purpose for the bigger picture.

import seaborn as sns
import matplotlib.pyplot as plt
from data_utils import convert_columns_to_int, read_csv_rows, columnar, concat, select, count, head

sns.set_theme() # part of seaborn fn.

izzi_rows = read_csv_rows("data/survey_izzi.csv")
alyssa_rows = read_csv_rows("data/survey_alyssa.csv")
# calls the data into our workspace.

izzi_cols = columnar(izzi_rows)
alyssa_cols = columnar(alyssa_rows)
combined = concat(izzi_cols, alyssa_cols)
# converts the data so we can concatenate it.

preview = head(combined, 10) # returns the first 10 rows of data.

selected = select(
    combined,
    ["own_examples", "pre_lecture_videos", "qz_effective"]
) # imports what we want from that data.

clean = convert_columns_to_int(
    selected,
    ["own_examples", "pre_lecture_videos", "qz_effective"]
) # cleans the data.

def filter_high_values(column: list[int], threshold: int) -> list[int]:
    """Returns values greater than a threshold.""" 
    result: list[int] = [] 
    for value in column: 
        if value > threshold: 
            result.append(value) 
    return result 
# creates images.
 
high_pre = filter_high_values(clean["pre_lecture_videos"], 5) # also does something with images.

def count(values):
    freq = {}
    for v in values:
        freq[v] = freq.get(v, 0) + 1
    return freq
# searches for recurring values.

own_freq = count(clean["own_examples"])
pre_freq = count(clean["pre_lecture_videos"])
qz_freq = count(clean["qz_effective"])
# counts how often a value recurs in the data, used to make the bar graphs.

plt.figure() # makes it so we can have 3 different graphs.
sns.barplot(
    x=list(own_freq.keys()), # pulls own_examples data keys into a list.
    y=list(own_freq.values())) # pulls own_examples data values into a list.
plt.title("Own Examples")
# creates the bar graph for own_examples.

plt.figure() # makes it so we can have 3 different graphs.
sns.barplot(
    x=list(pre_freq.keys()), # pulls pre_lecture_videos data keys into a list.
    y=list(pre_freq.values())) # pulls pre_lecture_videos_ data values into a list.
plt.title("Pre-Lecture Videos")
# creates the bar graph for pre_lecture_videos

plt.figure() # makes it so we can have 3 different graphs.
sns.barplot(
    x=list(qz_freq.keys()), # pulls qz_effective data keys into a list.
    y=list(qz_freq.values())) # pulls qz_effective values into a list.
plt.title("Quiz Effectiveness")
# creates the bar graph for qz__effective

<!-- This is a comment. Below, you'll see code for inserting an image. To make this image appear, update <custom-path>. To add an image, save it inside the imgs folder of this repository. -->
<img src="<custom-path>/static/imgs/logo.png" alt="Image of Comp110 rainbow logo. "  width="500"/>

## Visualizations 


### Own Examples 
<img src="/static/imgs/own_examples.png" width="500" alt="Bar chart showing student responses for how often they create their own examples when learning"> 


### Pre-Lecture Videos 
<img src="/static/imgs/prelecture.png" width="500" alt="Bar chart showing student ratings of pre-lecture video effectiveness"> 


### Quizzes 
<img src="/static/imgs/quizzes.png" width="500" alt="Bar chart showing student ratings of quiz effectiveness in helping learning"> 

## Conclusion

The results from our research was ultimately inconclusive on whether or not pre-class readings would have improved the course because this data was not collected. While the data that has been collected suggests that students generally find pre-class lecture videos and preparing for quizzes to be an effective study tool, we cannot conclude from that alone that pre-class readings would produce the same outcome.


However, the data does suggest that structured learning resources are highly valuable to students, which indicates that pre-class readings have the potential to support student understanding; especially if they are designed to reinforce key concepts and provide clear guidance. 

 
That being said, there are trade-offs to consider. Adding required readings would increase the workload for students in an already time-consuming course. It may also require additional effort from the instruction team to create or procure the effective materials. Furthermore, if the readings took the form of a textbook, this would introduce additional financial costs. 


Some possible refinements to this idea would be to make the readings optional. concise, or to reduce the workload in other areas of the course to balance the added time commitment. 


To further evaluate this idea, future experiments could involve implementing pre-class readings in some sections of the course and comparing outcomes such as quiz performance, assignment grades, and student feedback. Additionally, surveys could directly ask students whether or not readings improved their understanding of the course or their engagement with the content. 


To conclude, while the data does not provide a definitive answer to the question we were asking, it does suggest that structured preparatory materials have value. This in turn implies that pre-class readings could be a promising direction for future course improvements. 