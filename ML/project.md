# Machine Learning Project

We are going to scratch the surface of machine learning in this class, without talking too much about the math. We'll focus on a classification problem -- not [neural networks](https://en.wikipedia.org/wiki/Neural_network_(machine_learning)), probably no [gradient boosting](https://en.wikipedia.org/wiki/Gradient_boosting), just a gentle introduction.

All data sets will come from the [UC Irvine Machine Learning Repository](https://archive.ics.uci.edu). This site and the authors who contribute to it provide us with opportunities develop our machine learning skills, both in terms of developing the code and interpreting the results.

## Important Topics/Some Vocabulary

I am going to reference a hypothetical machine learning problem in which we try to predict whether a fruit is an apple, peach, nectarine, plum, blueberry, or kiwi based physical measurements.

Classification
: Classification problems are about taking measurements or attributes and using those to predict the class of an output. If we pick a random fruit and measure: a weight of 192 grams, a radius of 5.1 cm, an eccentricity of 0.04, and a hardness of 1.8 whatever-the-units-of-hardness-are, our model might predict it's a plum.

Features
: These are the attributes the model is trained on... here, the basic measurements of weight, radius, eccentricity, and hardness are probably good features. We sometimes need to pre-process measurements to produce meaningful features: maybe we collected the day-to-day growth rate of our fruits, but didn't have the final radius explicitly in the data. The growth rate over time might be interesting in itself, but integrating the growth rate to determine the final radius is probably be a more direct predictor.

Confusion matrices
: These help us to assess where our machine learning model is making incorrect predictions. It is common to randomly break a data set up into a portion for "training" and a portion for "validation". The confusion matrix summarizes the validation results, showing us e.g. that 21% of the plums were incorrectly identified as nectarines. In the fruit case, with 6 fruits, it would be a $6\times 6$ matrix.

```{figure} conf.png
:alt: 
:width: 500px
:align: center

A confusion matrix. This made-up data reveals that the model has a harder time discerning peaches, nectarines, and plums.
```


Feature Importance
: In the end we can ask about feature importance: which feature is most predictive of the classification? This can be "global" or "item-level" importance -- e.g., in general, the hardness measurement is the best way to distinguish between fruits (global), unless it is a fruit with a small radius, in which case it is almost certainly a blueberry (item-level).


All the topics below are classification problems with information about the sample features collected in a csv file. You will produce and interpret a confusion matrix and will assess the feature importance. You might even include this in your initial 

## LLM use

See [LLM use](LLM_use.md) for policies and recommendations on prompting.

:::{note} 
If you do not want to use an LLM... let's talk.
:::


## Project topics

You may choose from the following projects. The analyses will end up being quite similar, regardless: take the spreadsheet of features and targets, randomly divide it into training data and validation data, and produce a confusion matrix. Iterate with the LLM to modify parameters to improve your model.

### [Predicting Robot Faults](https://archive.ics.uci.edu/dataset/963/ur3+cobotops)

The history of electrical current, temperature, and speed is used to predict the conditions that lead to robot error (either a shutdown or loss of grip).

Hints:
- You might need to "clean" the data, there are some NaNs around. You won't need to do this immediately: wait for the error message and ask the LLM for help!
- The LLM might recommend "trend features" that can be built from this time series. If it doesn't, maybe you should ask about them...

### [Dry Bean Identification](https://archive.ics.uci.edu/dataset/602/dry+bean+dataset)

This is a genuine [computer vision](https://en.wikipedia.org/wiki/Computer_vision) project (with the image processing already done). Predict the type of bean from geometric measurements. The lessons could apply to any sort of factory production.

Hints:
- The inputs of this data set might be [highly correlated](../5_fitting/vif.md). This does not make it harder to fit, but will dilute the feature importance. Maybe ask the LLM about a "correlation heatmap", and when you get the results, ask how to interpret it and the effect on the feature importance rankings.

### [Age Prediction of Abalone](https://archive.ics.uci.edu/dataset/1/abalone)

Predict the age (number of rings) of sea snails based on their size and weight. One of the features in this data set is "shucked weight", which involves killing the snail. Ignoring that point, I think this project could be interpreted as a [nondestructive testing method](https://en.wikipedia.org/wiki/Nondestructive_testing): the old way of doing the measurement is time-consuming and destroys the snail; the new data-centric method might get us the same result with no damage. Maybe it will turn out that the most important features are length and diameter, meaning we don't need to kill it at all! Similar strategies could be implemented to see, e.g., how much lifetime is left in a product before it needs to be replaced.

Hints:
- The data comes as a .data file, but it contains comma-separated values. You can open the file with a text editor and add a first row that includes the column names (see the .names file), and then manually change the file extension to .csv.
- This one, too, might have highly correlated inputs. Talk to the LLM about it.
- The "confusion matrix" here will be little bit different because our output is a number. It will likely recommend a "random forest regressor" and will produce a plot of predicted vs. actual age.
:::{aside}
I was intentionally trying to avoid regression problems but there are enough tricky things about this one, e.g. the first feature is not a number.
:::








## Instructions/Deliverables

:::{important}
You cannot upload your data set to an AI tool. You must describe the problem and data to the LLM in your own words and then implement the code on your own computer. See [LLM use](LLM_use.md) for a recommended first prompt.
:::

We will again be creating a GitHub repository, though this one you will build up from scratch (in our GitHub Classroom -- I'll provide a link). The main directory will have a ```README.md``` report, including all the details asked about below. You should cite the data set. There will be sub-folders that contain code, as described below. You will describe the problem to the LLM using the strategy described [here](LLM_use.md#a-good-first-prompt)
:::{note} Deliverable 1
Your README will include this initial prompt.
:::

The LLM will likely suggest [random forest](https://en.wikipedia.org/wiki/Random_forest). Hopefully it will give a good explanation, and you can ask follow-up questions. I encourage you to ask it questions about "random forest" -- in your report, you will need to explain why you chose your path, and this is your opportunity to get some information.
:::{note} Deliverable 2
You will summarize this discussion, describing the random forest method and why it is appropriate in your own words. (You may quote the LLM. "Use quotes.")
:::

Once you feel OK about the background, go ahead and ask for the code. Be specific: "OK, generate the python code that implements the random forest scheme we discussed. Can you confirm that the standard validation scheme is to randomly divide the data into training and validation, and then produce a confusion matrix?"

The code may have a few bugs in it, as described [here](LLM_use.md#the-initial-follow-up-prompts). Work those out, and then...
:::{note} Deliverable 3
You will create a folder within your repository called ```code_1```. This is the first iteration of your model. Within your README, you should include your confusion matrix (an image) and some discussion. You might also include other metrics provided by the code in the discussion.
:::

You will iterate on the model as described [here](LLM_use.md#iterating-on-the-model). The goal is to wisely modify [hyperparameters](https://en.wikipedia.org/wiki/Hyperparameter_(machine_learning)) or perhaps build new features to improve upon your predictions. When you (and the LLM) are satisfied...
:::{note} Deliverable 4
Include some discussion of these prompts, and the responses, in your README. Then,
you will create a folder within your repository called ```code_2``` which includes your tuned model. Within your README, you should include your (improved) confusion matrix and some discussion about what changed between the models.
:::

Lastly, with your tuned model, you will produce a feature importance plot.
:::{note} Deliverable 5
Your README will include the feature importance plot and some discussion about the results.
:::

