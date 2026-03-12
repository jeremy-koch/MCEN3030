# Machine Learning Project

We are going to scratch the surface of machine learning in this class, without talking too much about the math. We'll focus on a classification problem -- not [neural networks](https://en.wikipedia.org/wiki/Neural_network_(machine_learning)), probably no [gradient boosting](https://en.wikipedia.org/wiki/Gradient_boosting), just a gentle introduction.

All data sets will come from the [UC Irvine Machine Learning Repository](https://archive.ics.uci.edu). This site and the authors who contribute to it provide us with opportunities develop our machine learning skills, both in terms of developing the code and interpreting the results.

## Important Topics/Some Vocabulary

I am going to reference a hypothetical machine learning problem in which we try to predict whether a fruit is an apple, peach, nectarine, plum, blueberry, or kiwi based physical measurements.

"Classification"
: Classification problems are about taking measurements or attributes and using those to predict the class of an output. If we pick a random fruit and measure: a weight of 192 grams, a radius of 5.1 cm, an eccentricity of 0.04, and a hardness of 1.8 whatever-the-units-of-hardness-are, our model might predict it's a plum.

"Features"
: These are the attributes the model is trained on... here, the basic measurements of weight, radius, eccentricity, and hardness are probably good features. We sometimes need to pre-process measurements to produce meaningful features: maybe we collected the day-to-day growth rate of our fruits, but didn't have the final radius explicitly in the data. The growth rate over time might be interesting in itself, but integrating the growth rate to determine the final radius is probably be a more direct predictor.

"Confusion matrices"
: These help us to assess where our machine learning model is making incorrect predictions. It is common to randomly break a data set up into a portion for "training" and a portion for "validation". The confusion matrix summarizes the validation results, showing us e.g. that 21% of the plums were incorrectly identified as nectarines. In the fruit case, with 6 fruits, it would be a $6\times 6$ matrix.

```{figure} conf.png
:alt: 
:width: 300px
:align: center

A confusion matrix. This made-up data reveals that the model has a harder time discerning peaches, nectarines, and plums.
```


"Feature Importance"
: In the end we can ask about "feature importance": which feature is most predictive of the classification? This can be "global" or "item-level" importance -- e.g., in general, the hardness measurement is the best way to distinguish between fruits ("global"), unless it is a fruit with a small radius, in which case it is almost certainly a blueberry ("item-level").


All the topics below are classification problems with information about the sample features collected in a csv file. You will produce and interpret a confusion matrix and will assess the feature importance. You might even include this in your initial 

## LLM use

See [LLM use](LLM_use.md).

:::{dropdown} If you do not want to use an LLM...
:open:
If you are averse to using an LLM, let's talk.
:::


## Project topics

You may choose from the following projects. The analyses will end up being quite similar, regardless: take the spreadsheet of features and targets, randomly divide it into training data and validation data, and produce a confusion matrix. Iterate with the LLM to modify parameters to improve your model.

### [Predicting Robot Faults](https://archive.ics.uci.edu/dataset/963/ur3+cobotops)

The history of electrical current, temperature, and speed is used to predict the conditions that lead to robot error (either a shutdown or loss of grip).

Hints:
- You might need to "clean" the data, there are some NaNs around. You won't need to do this immediately: wait for the error message and ask the LLM for help!
- The LLM might recommend "trend features" that can be built from this time series. If it doesn't, maybe you should ask about them...

### [Dry Bean Identification](https://archive.ics.uci.edu/dataset/602/dry+bean+dataset)

This is a genuine [computer vision](https://en.wikipedia.org/wiki/Computer_vision) project (with the image processing already done), the lessons from which could apply to any sort of factory production. Predict the type of bean from geometric measurements.

Hints:
- The inputs of this data set might be [highly correlated](../5_fitting/vif.md). This does not make it harder to fit, but will dilute the feature importance. Maybe ask the LLM about a "correlation heatmap". When you get the results, ask how to interpret it and the effect on the feature importance rankings.

### [Age Prediction of Abalone](https://archive.ics.uci.edu/dataset/1/abalone)



One of the features in this data set is "shucked weight", which involves killing the clam. Ignoring that point, I think this project could be interpreted as a [nondestructive testing method](https://en.wikipedia.org/wiki/Nondestructive_testing) -- the "old" way of doing the measurement is time-consuming and involves staining the abalone, perhaps ruining it. With this data-centric method, a few quick measurements might help us predict the age, and maybe it will turn out that the most important features are length and diameter, meaning we don't need to kill it to estimate its age. I imagine a similar strategy could be implemented to see, e.g., how much lifetime is left in a product before it needs replaced.

Hints:
- The data comes as a .data file, but it contains comma-separated values. You can open the file with a text editor and add a first row that includes the column names, and then change the file extension to .csv.
- This one, too, might have highly correlated inputs. Talk to the LLM about it.
- The "confusion matrix" here will be little bit different because our output is a number. It will likely recommend a "random forest regressor" and will produce a plot of predicted vs. actual age.
:::{aside}
I was intentionally trying to avoid regression problems but there are enough tricky things about this, e.g. the first feature is M/F/I, that I decided to keep it.
:::








## Instructions

:::{important}
You cannot upload your data set to an AI tool. You must describe the problem and data to the LLM in your own words and then implement the code on your own computer.
:::




Your interaction should look something like this.
1. Describe the problem, including what is in the data set. An example prompt: "I would like to do a machine learning project whose the goal is to predict whether a fruit is an apple, peach, nectarine, plum, or kiwi based physical measurements. I have a spreadsheet with columns 'fruit', 'weight', 'avg_radius', 'eccentricity', and 'hardness_value'. There are approximately 4000 rows. I will ask for Python scikit-learn code soon, but first: Can we talk about the best way to model this data set?"
2. The LLM will likely suggest [random forest](https://en.wikipedia.org/wiki/Random_forest). Hopefully it will give a good explanation, and you can ask follow-up questions. I encourage you to ask it questions about "random forest" -- in your report, you will need to explain why you chose your path, and this is your opportunity to get some information.
3. Once you feel OK about the background, go ahead and ask for the code. Be specific: "OK, generate the python code that implements the random forest scheme we discussed. Can you confirm that the standard validation scheme is to randomly divide the data into training and validation, and then produce a confusion matrix". 

:::{tip}
You can use code files (.m, .py, .jl) or [notebook files](../1_prog-basics/notebooks.md) (.mlx, .ipynb, and Pluto uses .jl again I think). Just ask it.
:::

:::{tip}
You may need to download it, but MATLAB has a machine learning toolbox.

For Python users, I strongly recommend scikit-learn. TensorFlow and PyTorch are more common for professionals. (I couldn't get TensorFlow to work on my machine.)

For Julia users, Lu and Flux
:::




### Step 3: Implement the code





:::{tip}
Sometimes the LLM will say "replace section 4 of the code with this". Try to work with it, but if it is getting confusing you can always say "give me a summary of all the current code". 
:::





### Step 4: Feature Importance

Once you have 















## Deliverables

All of these are described in more detail below.

- Your repository