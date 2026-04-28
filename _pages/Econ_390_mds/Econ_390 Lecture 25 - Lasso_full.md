---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L25/
title: Econ 390 Lecture 25
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture25_Lasso_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture25_Lasso_full.ipynb)

# Econ 390 - Lecture 25: Least Absolute Shrinkage and Selection Operator (Lasso)
Today we'll be talking about Machine Learning, specifically the Lasso regression. You can find a chapter in [Turrell](https://aeturrell.github.io/coding-for-economists/ml-sup.html) that covers Lasso and other similar regression methods. I also used [this](https://geostatsguy.github.io/MachineLearningDemos_Book/MachineLearning_LASSO_regression.html) resource when creating this lecture. Machine Learning is a complicated topic, you can spend much much more time on Lasso alone. Regardless, I am hoping after this class you can have at least a basic understanding of how Lasso works and how it can be useful.

## The Lasso


```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# Reproducability
seed = 42
prng = np.random.default_rng(seed)
```


```python
# New library!
from sklearn.datasets import make_regression

# Creates a dataset based on a randomized regression
X, y, coef = make_regression(n_samples=500, n_features=6, noise=0.5, random_state=seed, coef=True)
```


```python
# What is X?
print(type(X))
print(X.shape)
```

    <class 'numpy.ndarray'>
    (500, 6)
    


```python
# Convert to DataFrame
reg_df = pd.DataFrame(X)
reg_df["y"] = y
reg_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.753965</td>
      <td>0.281191</td>
      <td>-0.062593</td>
      <td>-0.280675</td>
      <td>0.758929</td>
      <td>0.104201</td>
      <td>43.220530</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.031845</td>
      <td>-0.439731</td>
      <td>0.196555</td>
      <td>-1.485560</td>
      <td>-0.186872</td>
      <td>1.446978</td>
      <td>-9.556226</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.600639</td>
      <td>0.110923</td>
      <td>0.375698</td>
      <td>-0.291694</td>
      <td>-0.544383</td>
      <td>-1.150994</td>
      <td>-62.911906</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.998311</td>
      <td>-0.322320</td>
      <td>1.521316</td>
      <td>-0.431620</td>
      <td>1.615376</td>
      <td>1.217159</td>
      <td>307.752538</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.338496</td>
      <td>0.770865</td>
      <td>1.143754</td>
      <td>-0.415288</td>
      <td>0.235615</td>
      <td>-1.478586</td>
      <td>167.728761</td>
    </tr>
  </tbody>
</table>
</div>




```python
# x0 on y
reg_df.plot.scatter(x=0,y="y");
```


    
![png](output_6_0.png)
    



```python
# Supervised means training set and test set
from sklearn.model_selection import train_test_split

train_df, test_df = train_test_split(reg_df, random_state=seed, test_size=0.2)
train_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>249</th>
      <td>-1.116524</td>
      <td>1.533728</td>
      <td>-1.707358</td>
      <td>1.235812</td>
      <td>-0.629263</td>
      <td>-0.535801</td>
      <td>-85.096380</td>
    </tr>
    <tr>
      <th>433</th>
      <td>-2.123896</td>
      <td>-0.808298</td>
      <td>-0.599393</td>
      <td>-0.525755</td>
      <td>2.189803</td>
      <td>-0.839722</td>
      <td>-89.842998</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1.117399</td>
      <td>-0.548287</td>
      <td>0.501783</td>
      <td>1.448499</td>
      <td>-0.155898</td>
      <td>0.160018</td>
      <td>85.391162</td>
    </tr>
    <tr>
      <th>322</th>
      <td>0.484733</td>
      <td>1.281016</td>
      <td>0.852774</td>
      <td>-0.846357</td>
      <td>-0.447322</td>
      <td>0.067856</td>
      <td>165.681418</td>
    </tr>
    <tr>
      <th>332</th>
      <td>-0.019260</td>
      <td>-0.191028</td>
      <td>0.784604</td>
      <td>-0.262891</td>
      <td>-2.562334</td>
      <td>2.412615</td>
      <td>-99.893249</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>106</th>
      <td>1.059936</td>
      <td>-0.862776</td>
      <td>-0.392013</td>
      <td>0.617006</td>
      <td>-0.478837</td>
      <td>0.693479</td>
      <td>-76.958580</td>
    </tr>
    <tr>
      <th>270</th>
      <td>-0.742484</td>
      <td>0.003696</td>
      <td>1.341476</td>
      <td>-0.485306</td>
      <td>1.962587</td>
      <td>1.011463</td>
      <td>269.059898</td>
    </tr>
    <tr>
      <th>348</th>
      <td>1.083051</td>
      <td>-1.142970</td>
      <td>0.560785</td>
      <td>1.053802</td>
      <td>0.058209</td>
      <td>0.357787</td>
      <td>39.568143</td>
    </tr>
    <tr>
      <th>435</th>
      <td>-0.569833</td>
      <td>0.287329</td>
      <td>-0.424236</td>
      <td>0.329509</td>
      <td>-0.287448</td>
      <td>-0.045512</td>
      <td>-50.974463</td>
    </tr>
    <tr>
      <th>102</th>
      <td>0.871125</td>
      <td>-0.420984</td>
      <td>2.075401</td>
      <td>-0.326024</td>
      <td>0.394452</td>
      <td>0.289775</td>
      <td>226.545509</td>
    </tr>
  </tbody>
</table>
<p>400 rows × 7 columns</p>
</div>




```python
# Let's run Lasso!
from sklearn import linear_model

reg_lasso = linear_model.Lasso(alpha=0.1, random_state=seed)
reg_lasso.fit(train_df.iloc[:,:-1],train_df["y"])
```




<style>#sk-container-id-1 {
  /* Definition of color scheme common for light and dark mode */
  --sklearn-color-text: #000;
  --sklearn-color-text-muted: #666;
  --sklearn-color-line: gray;
  /* Definition of color scheme for unfitted estimators */
  --sklearn-color-unfitted-level-0: #fff5e6;
  --sklearn-color-unfitted-level-1: #f6e4d2;
  --sklearn-color-unfitted-level-2: #ffe0b3;
  --sklearn-color-unfitted-level-3: chocolate;
  /* Definition of color scheme for fitted estimators */
  --sklearn-color-fitted-level-0: #f0f8ff;
  --sklearn-color-fitted-level-1: #d4ebff;
  --sklearn-color-fitted-level-2: #b3dbfd;
  --sklearn-color-fitted-level-3: cornflowerblue;

  /* Specific color for light theme */
  --sklearn-color-text-on-default-background: var(--sg-text-color, var(--theme-code-foreground, var(--jp-content-font-color1, black)));
  --sklearn-color-background: var(--sg-background-color, var(--theme-background, var(--jp-layout-color0, white)));
  --sklearn-color-border-box: var(--sg-text-color, var(--theme-code-foreground, var(--jp-content-font-color1, black)));
  --sklearn-color-icon: #696969;

  @media (prefers-color-scheme: dark) {
    /* Redefinition of color scheme for dark theme */
    --sklearn-color-text-on-default-background: var(--sg-text-color, var(--theme-code-foreground, var(--jp-content-font-color1, white)));
    --sklearn-color-background: var(--sg-background-color, var(--theme-background, var(--jp-layout-color0, #111)));
    --sklearn-color-border-box: var(--sg-text-color, var(--theme-code-foreground, var(--jp-content-font-color1, white)));
    --sklearn-color-icon: #878787;
  }
}

#sk-container-id-1 {
  color: var(--sklearn-color-text);
}

#sk-container-id-1 pre {
  padding: 0;
}

#sk-container-id-1 input.sk-hidden--visually {
  border: 0;
  clip: rect(1px 1px 1px 1px);
  clip: rect(1px, 1px, 1px, 1px);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  width: 1px;
}

#sk-container-id-1 div.sk-dashed-wrapped {
  border: 1px dashed var(--sklearn-color-line);
  margin: 0 0.4em 0.5em 0.4em;
  box-sizing: border-box;
  padding-bottom: 0.4em;
  background-color: var(--sklearn-color-background);
}

#sk-container-id-1 div.sk-container {
  /* jupyter's `normalize.less` sets `[hidden] { display: none; }`
     but bootstrap.min.css set `[hidden] { display: none !important; }`
     so we also need the `!important` here to be able to override the
     default hidden behavior on the sphinx rendered scikit-learn.org.
     See: https://github.com/scikit-learn/scikit-learn/issues/21755 */
  display: inline-block !important;
  position: relative;
}

#sk-container-id-1 div.sk-text-repr-fallback {
  display: none;
}

div.sk-parallel-item,
div.sk-serial,
div.sk-item {
  /* draw centered vertical line to link estimators */
  background-image: linear-gradient(var(--sklearn-color-text-on-default-background), var(--sklearn-color-text-on-default-background));
  background-size: 2px 100%;
  background-repeat: no-repeat;
  background-position: center center;
}

/* Parallel-specific style estimator block */

#sk-container-id-1 div.sk-parallel-item::after {
  content: "";
  width: 100%;
  border-bottom: 2px solid var(--sklearn-color-text-on-default-background);
  flex-grow: 1;
}

#sk-container-id-1 div.sk-parallel {
  display: flex;
  align-items: stretch;
  justify-content: center;
  background-color: var(--sklearn-color-background);
  position: relative;
}

#sk-container-id-1 div.sk-parallel-item {
  display: flex;
  flex-direction: column;
}

#sk-container-id-1 div.sk-parallel-item:first-child::after {
  align-self: flex-end;
  width: 50%;
}

#sk-container-id-1 div.sk-parallel-item:last-child::after {
  align-self: flex-start;
  width: 50%;
}

#sk-container-id-1 div.sk-parallel-item:only-child::after {
  width: 0;
}

/* Serial-specific style estimator block */

#sk-container-id-1 div.sk-serial {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: var(--sklearn-color-background);
  padding-right: 1em;
  padding-left: 1em;
}


/* Toggleable style: style used for estimator/Pipeline/ColumnTransformer box that is
clickable and can be expanded/collapsed.
- Pipeline and ColumnTransformer use this feature and define the default style
- Estimators will overwrite some part of the style using the `sk-estimator` class
*/

/* Pipeline and ColumnTransformer style (default) */

#sk-container-id-1 div.sk-toggleable {
  /* Default theme specific background. It is overwritten whether we have a
  specific estimator or a Pipeline/ColumnTransformer */
  background-color: var(--sklearn-color-background);
}

/* Toggleable label */
#sk-container-id-1 label.sk-toggleable__label {
  cursor: pointer;
  display: flex;
  width: 100%;
  margin-bottom: 0;
  padding: 0.5em;
  box-sizing: border-box;
  text-align: center;
  align-items: start;
  justify-content: space-between;
  gap: 0.5em;
}

#sk-container-id-1 label.sk-toggleable__label .caption {
  font-size: 0.6rem;
  font-weight: lighter;
  color: var(--sklearn-color-text-muted);
}

#sk-container-id-1 label.sk-toggleable__label-arrow:before {
  /* Arrow on the left of the label */
  content: "▸";
  float: left;
  margin-right: 0.25em;
  color: var(--sklearn-color-icon);
}

#sk-container-id-1 label.sk-toggleable__label-arrow:hover:before {
  color: var(--sklearn-color-text);
}

/* Toggleable content - dropdown */

#sk-container-id-1 div.sk-toggleable__content {
  max-height: 0;
  max-width: 0;
  overflow: hidden;
  text-align: left;
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-0);
}

#sk-container-id-1 div.sk-toggleable__content.fitted {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-0);
}

#sk-container-id-1 div.sk-toggleable__content pre {
  margin: 0.2em;
  border-radius: 0.25em;
  color: var(--sklearn-color-text);
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-0);
}

#sk-container-id-1 div.sk-toggleable__content.fitted pre {
  /* unfitted */
  background-color: var(--sklearn-color-fitted-level-0);
}

#sk-container-id-1 input.sk-toggleable__control:checked~div.sk-toggleable__content {
  /* Expand drop-down */
  max-height: 200px;
  max-width: 100%;
  overflow: auto;
}

#sk-container-id-1 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {
  content: "▾";
}

/* Pipeline/ColumnTransformer-specific style */

#sk-container-id-1 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {
  color: var(--sklearn-color-text);
  background-color: var(--sklearn-color-unfitted-level-2);
}

#sk-container-id-1 div.sk-label.fitted input.sk-toggleable__control:checked~label.sk-toggleable__label {
  background-color: var(--sklearn-color-fitted-level-2);
}

/* Estimator-specific style */

/* Colorize estimator box */
#sk-container-id-1 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-2);
}

#sk-container-id-1 div.sk-estimator.fitted input.sk-toggleable__control:checked~label.sk-toggleable__label {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-2);
}

#sk-container-id-1 div.sk-label label.sk-toggleable__label,
#sk-container-id-1 div.sk-label label {
  /* The background is the default theme color */
  color: var(--sklearn-color-text-on-default-background);
}

/* On hover, darken the color of the background */
#sk-container-id-1 div.sk-label:hover label.sk-toggleable__label {
  color: var(--sklearn-color-text);
  background-color: var(--sklearn-color-unfitted-level-2);
}

/* Label box, darken color on hover, fitted */
#sk-container-id-1 div.sk-label.fitted:hover label.sk-toggleable__label.fitted {
  color: var(--sklearn-color-text);
  background-color: var(--sklearn-color-fitted-level-2);
}

/* Estimator label */

#sk-container-id-1 div.sk-label label {
  font-family: monospace;
  font-weight: bold;
  display: inline-block;
  line-height: 1.2em;
}

#sk-container-id-1 div.sk-label-container {
  text-align: center;
}

/* Estimator-specific */
#sk-container-id-1 div.sk-estimator {
  font-family: monospace;
  border: 1px dotted var(--sklearn-color-border-box);
  border-radius: 0.25em;
  box-sizing: border-box;
  margin-bottom: 0.5em;
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-0);
}

#sk-container-id-1 div.sk-estimator.fitted {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-0);
}

/* on hover */
#sk-container-id-1 div.sk-estimator:hover {
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-2);
}

#sk-container-id-1 div.sk-estimator.fitted:hover {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-2);
}

/* Specification for estimator info (e.g. "i" and "?") */

/* Common style for "i" and "?" */

.sk-estimator-doc-link,
a:link.sk-estimator-doc-link,
a:visited.sk-estimator-doc-link {
  float: right;
  font-size: smaller;
  line-height: 1em;
  font-family: monospace;
  background-color: var(--sklearn-color-background);
  border-radius: 1em;
  height: 1em;
  width: 1em;
  text-decoration: none !important;
  margin-left: 0.5em;
  text-align: center;
  /* unfitted */
  border: var(--sklearn-color-unfitted-level-1) 1pt solid;
  color: var(--sklearn-color-unfitted-level-1);
}

.sk-estimator-doc-link.fitted,
a:link.sk-estimator-doc-link.fitted,
a:visited.sk-estimator-doc-link.fitted {
  /* fitted */
  border: var(--sklearn-color-fitted-level-1) 1pt solid;
  color: var(--sklearn-color-fitted-level-1);
}

/* On hover */
div.sk-estimator:hover .sk-estimator-doc-link:hover,
.sk-estimator-doc-link:hover,
div.sk-label-container:hover .sk-estimator-doc-link:hover,
.sk-estimator-doc-link:hover {
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-3);
  color: var(--sklearn-color-background);
  text-decoration: none;
}

div.sk-estimator.fitted:hover .sk-estimator-doc-link.fitted:hover,
.sk-estimator-doc-link.fitted:hover,
div.sk-label-container:hover .sk-estimator-doc-link.fitted:hover,
.sk-estimator-doc-link.fitted:hover {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-3);
  color: var(--sklearn-color-background);
  text-decoration: none;
}

/* Span, style for the box shown on hovering the info icon */
.sk-estimator-doc-link span {
  display: none;
  z-index: 9999;
  position: relative;
  font-weight: normal;
  right: .2ex;
  padding: .5ex;
  margin: .5ex;
  width: min-content;
  min-width: 20ex;
  max-width: 50ex;
  color: var(--sklearn-color-text);
  box-shadow: 2pt 2pt 4pt #999;
  /* unfitted */
  background: var(--sklearn-color-unfitted-level-0);
  border: .5pt solid var(--sklearn-color-unfitted-level-3);
}

.sk-estimator-doc-link.fitted span {
  /* fitted */
  background: var(--sklearn-color-fitted-level-0);
  border: var(--sklearn-color-fitted-level-3);
}

.sk-estimator-doc-link:hover span {
  display: block;
}

/* "?"-specific style due to the `<a>` HTML tag */

#sk-container-id-1 a.estimator_doc_link {
  float: right;
  font-size: 1rem;
  line-height: 1em;
  font-family: monospace;
  background-color: var(--sklearn-color-background);
  border-radius: 1rem;
  height: 1rem;
  width: 1rem;
  text-decoration: none;
  /* unfitted */
  color: var(--sklearn-color-unfitted-level-1);
  border: var(--sklearn-color-unfitted-level-1) 1pt solid;
}

#sk-container-id-1 a.estimator_doc_link.fitted {
  /* fitted */
  border: var(--sklearn-color-fitted-level-1) 1pt solid;
  color: var(--sklearn-color-fitted-level-1);
}

/* On hover */
#sk-container-id-1 a.estimator_doc_link:hover {
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-3);
  color: var(--sklearn-color-background);
  text-decoration: none;
}

#sk-container-id-1 a.estimator_doc_link.fitted:hover {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-3);
}
</style><div id="sk-container-id-1" class="sk-top-container"><div class="sk-text-repr-fallback"><pre>Lasso(alpha=0.1, random_state=42)</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden><div class="sk-item"><div class="sk-estimator fitted sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-1" type="checkbox" checked><label for="sk-estimator-id-1" class="sk-toggleable__label fitted sk-toggleable__label-arrow"><div><div>Lasso</div></div><div><a class="sk-estimator-doc-link fitted" rel="noreferrer" target="_blank" href="https://scikit-learn.org/1.6/modules/generated/sklearn.linear_model.Lasso.html">?<span>Documentation for Lasso</span></a><span class="sk-estimator-doc-link fitted">i<span>Fitted</span></span></div></label><div class="sk-toggleable__content fitted"><pre>Lasso(alpha=0.1, random_state=42)</pre></div> </div></div></div></div>




```python
# Results:
reg_lasso.coef_
```




    array([43.04444381, 98.23909293, 96.83389336, 34.68124549, 81.74516152,
           25.85780195])




```python
# Predictions:
print(reg_lasso.predict(test_df.iloc[:5,:-1]))
test_df.head()
```

    [ 163.08609994 -169.85887763  -66.33847724  -35.00337041 -262.31589457]
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>361</th>
      <td>0.414866</td>
      <td>0.342338</td>
      <td>0.853976</td>
      <td>0.463289</td>
      <td>-0.335138</td>
      <td>1.554160</td>
      <td>163.401193</td>
    </tr>
    <tr>
      <th>73</th>
      <td>-0.822220</td>
      <td>-0.321386</td>
      <td>-0.563725</td>
      <td>0.243687</td>
      <td>-0.825497</td>
      <td>0.412931</td>
      <td>-170.729725</td>
    </tr>
    <tr>
      <th>374</th>
      <td>0.014273</td>
      <td>0.892597</td>
      <td>0.730764</td>
      <td>-0.953939</td>
      <td>-1.970104</td>
      <td>-1.211172</td>
      <td>-67.471072</td>
    </tr>
    <tr>
      <th>155</th>
      <td>-0.170185</td>
      <td>-0.551186</td>
      <td>-0.003374</td>
      <td>-0.453228</td>
      <td>0.778361</td>
      <td>-0.818199</td>
      <td>-34.828869</td>
    </tr>
    <tr>
      <th>104</th>
      <td>-0.999302</td>
      <td>-0.607822</td>
      <td>-0.022868</td>
      <td>-0.504775</td>
      <td>-2.121855</td>
      <td>1.296995</td>
      <td>-262.404723</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Mean Square Error (MSE):
from sklearn.metrics import mean_squared_error

mean_squared_error(y_true=test_df["y"], y_pred=reg_lasso.predict(test_df.iloc[:,:-1]))
```




    0.39654453453700406




```python
# Compare MSE in and out of sample
mse_df = pd.DataFrame(index=["out-of-sample","in-sample"],columns=["Lasso"])
mse_df.loc["out-of-sample","Lasso"] = mean_squared_error(y_true=test_df["y"],y_pred=reg_lasso.predict(test_df.iloc[:,:-1]))
mse_df.loc["in-sample","Lasso"] = mean_squared_error(y_true=train_df["y"], y_pred = reg_lasso.predict(train_df.iloc[:,:-1]))
mse_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Lasso</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>out-of-sample</th>
      <td>0.396545</td>
    </tr>
    <tr>
      <th>in-sample</th>
      <td>0.317716</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Prediction vs. Truth
results_df = pd.DataFrame()

results_df["prediction"] = reg_lasso.predict(test_df.iloc[:,:-1])
results_df["actual"] = test_df["y"].values

results_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>prediction</th>
      <th>actual</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>163.086100</td>
      <td>163.401193</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-169.858878</td>
      <td>-170.729725</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-66.338477</td>
      <td>-67.471072</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-35.003370</td>
      <td>-34.828869</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-262.315895</td>
      <td>-262.404723</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Plot the errors
fig, ax = plt.subplots()

ax.scatter(results_df["actual"], results_df["actual"]-results_df["prediction"], alpha=0.9, label = "Lasso")
ax.legend()
ax.set_title(r"Error in prediction, $y -\hat{y}$")
plt.show()
```


    
![png](output_14_0.png)
    



```python
# Different values of alpha
mse_all = []
alpha_all = []
for i in range(1, 100, 1):
    reg_lasso = linear_model.Lasso(alpha=i/100, random_state=seed)
    reg_lasso.fit(train_df.iloc[:,:-1],train_df["y"])
    mse = mean_squared_error(y_true=test_df["y"],y_pred=reg_lasso.predict(test_df.iloc[:,:-1]))
    mse_all = mse_all + [mse]
    alpha_all = alpha_all + [i/100]
plt.plot(alpha_all, mse_all);
```


    
![png](output_15_0.png)
    


## UCI Machine Learning Repository
UC Irvine has a [website](https://archive.ics.uci.edu/) full of datasets that are useful for Machine Learning! Today we will be using the [Default of Credit Cards](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients) dataset.


```python
econ390path = "https://m-mcmain.github.io/files/Econ390SP26/"
```


```python
# Read in the data
default = pd.read_csv(econ390path + "default_of_credit_card_clients_cut.csv")
log_columns = ["LIMIT_BAL", "BILL_AMT1", "BILL_AMT2", "BILL_AMT3", "BILL_AMT4", "BILL_AMT5", "BILL_AMT6", 
               "PAY_AMT1", "PAY_AMT2", "PAY_AMT3", "PAY_AMT4", "PAY_AMT5", "PAY_AMT6"]
default[log_columns] = np.arcsinh(default[log_columns])
default
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>LIMIT_BAL</th>
      <th>SEX</th>
      <th>AGE</th>
      <th>BILL_AMT1</th>
      <th>BILL_AMT2</th>
      <th>BILL_AMT3</th>
      <th>BILL_AMT4</th>
      <th>BILL_AMT5</th>
      <th>BILL_AMT6</th>
      <th>PAY_AMT1</th>
      <th>PAY_AMT2</th>
      <th>PAY_AMT3</th>
      <th>PAY_AMT4</th>
      <th>PAY_AMT5</th>
      <th>PAY_AMT6</th>
      <th>default payment next month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10.596635</td>
      <td>2</td>
      <td>24</td>
      <td>8.965207</td>
      <td>8.732950</td>
      <td>7.228389</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>7.228389</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12.388394</td>
      <td>2</td>
      <td>26</td>
      <td>8.587465</td>
      <td>8.146130</td>
      <td>8.587465</td>
      <td>8.786304</td>
      <td>8.840725</td>
      <td>8.782936</td>
      <td>0.000000</td>
      <td>7.600903</td>
      <td>7.600903</td>
      <td>7.600903</td>
      <td>0.000000</td>
      <td>8.294050</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>12.100712</td>
      <td>2</td>
      <td>34</td>
      <td>10.976406</td>
      <td>10.241887</td>
      <td>10.207953</td>
      <td>10.263327</td>
      <td>10.305480</td>
      <td>10.344899</td>
      <td>8.018296</td>
      <td>8.006368</td>
      <td>7.600903</td>
      <td>7.600903</td>
      <td>7.600903</td>
      <td>9.210340</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11.512925</td>
      <td>2</td>
      <td>37</td>
      <td>11.450837</td>
      <td>11.476946</td>
      <td>11.498644</td>
      <td>10.944259</td>
      <td>10.966783</td>
      <td>10.986885</td>
      <td>8.294050</td>
      <td>8.303505</td>
      <td>7.783224</td>
      <td>7.696213</td>
      <td>7.667626</td>
      <td>7.600903</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>11.512925</td>
      <td>1</td>
      <td>57</td>
      <td>9.754639</td>
      <td>9.336092</td>
      <td>11.179828</td>
      <td>10.642564</td>
      <td>10.552996</td>
      <td>10.552213</td>
      <td>8.294050</td>
      <td>11.203161</td>
      <td>9.903488</td>
      <td>9.798127</td>
      <td>7.228389</td>
      <td>7.213769</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>29995</th>
      <td>12.994530</td>
      <td>1</td>
      <td>39</td>
      <td>12.842374</td>
      <td>12.862634</td>
      <td>12.940194</td>
      <td>12.078285</td>
      <td>11.042506</td>
      <td>10.372240</td>
      <td>9.740969</td>
      <td>10.596635</td>
      <td>9.210940</td>
      <td>8.715060</td>
      <td>9.210340</td>
      <td>7.600903</td>
      <td>0</td>
    </tr>
    <tr>
      <th>29996</th>
      <td>12.611538</td>
      <td>1</td>
      <td>43</td>
      <td>8.121480</td>
      <td>8.204125</td>
      <td>8.854237</td>
      <td>9.795791</td>
      <td>9.247636</td>
      <td>0.000000</td>
      <td>8.209036</td>
      <td>8.861067</td>
      <td>9.797905</td>
      <td>5.552975</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>29997</th>
      <td>11.002100</td>
      <td>1</td>
      <td>37</td>
      <td>8.872067</td>
      <td>8.811652</td>
      <td>8.615408</td>
      <td>10.639598</td>
      <td>10.625319</td>
      <td>10.563957</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>10.691945</td>
      <td>9.035987</td>
      <td>8.294050</td>
      <td>8.732305</td>
      <td>1</td>
    </tr>
    <tr>
      <th>29998</th>
      <td>11.982929</td>
      <td>1</td>
      <td>41</td>
      <td>-8.098643</td>
      <td>11.962458</td>
      <td>11.935628</td>
      <td>11.566921</td>
      <td>10.073652</td>
      <td>11.491579</td>
      <td>12.054086</td>
      <td>8.827321</td>
      <td>7.764721</td>
      <td>8.256348</td>
      <td>11.570515</td>
      <td>8.190909</td>
      <td>1</td>
    </tr>
    <tr>
      <th>29999</th>
      <td>11.512925</td>
      <td>1</td>
      <td>46</td>
      <td>11.470623</td>
      <td>11.490782</td>
      <td>11.508194</td>
      <td>11.199173</td>
      <td>11.079925</td>
      <td>10.329605</td>
      <td>8.332308</td>
      <td>8.188689</td>
      <td>7.958577</td>
      <td>7.600903</td>
      <td>7.600903</td>
      <td>7.600903</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>30000 rows × 16 columns</p>
</div>




```python
# Create the training and testing set
train_default, test_default = train_test_split(default, random_state=seed, test_size = 0.2)
train_default.rename(columns={"default payment next month":"default"}, inplace=True)
train_default
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>LIMIT_BAL</th>
      <th>SEX</th>
      <th>AGE</th>
      <th>BILL_AMT1</th>
      <th>BILL_AMT2</th>
      <th>BILL_AMT3</th>
      <th>BILL_AMT4</th>
      <th>BILL_AMT5</th>
      <th>BILL_AMT6</th>
      <th>PAY_AMT1</th>
      <th>PAY_AMT2</th>
      <th>PAY_AMT3</th>
      <th>PAY_AMT4</th>
      <th>PAY_AMT5</th>
      <th>PAY_AMT6</th>
      <th>default</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>21753</th>
      <td>11.982929</td>
      <td>2</td>
      <td>24</td>
      <td>11.920056</td>
      <td>11.949282</td>
      <td>11.961718</td>
      <td>11.901326</td>
      <td>11.280817</td>
      <td>11.276114</td>
      <td>8.854522</td>
      <td>9.210540</td>
      <td>8.339023</td>
      <td>7.798113</td>
      <td>7.969012</td>
      <td>7.470794</td>
      <td>0</td>
    </tr>
    <tr>
      <th>251</th>
      <td>11.002100</td>
      <td>1</td>
      <td>28</td>
      <td>10.976508</td>
      <td>10.985530</td>
      <td>10.973529</td>
      <td>10.829927</td>
      <td>10.691990</td>
      <td>0.000000</td>
      <td>9.211540</td>
      <td>7.819235</td>
      <td>7.439560</td>
      <td>7.554859</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>22941</th>
      <td>12.793859</td>
      <td>2</td>
      <td>44</td>
      <td>10.641417</td>
      <td>0.000000</td>
      <td>7.438384</td>
      <td>0.000000</td>
      <td>9.529666</td>
      <td>9.936922</td>
      <td>0.000000</td>
      <td>7.438384</td>
      <td>0.000000</td>
      <td>9.529666</td>
      <td>9.936922</td>
      <td>5.897161</td>
      <td>0</td>
    </tr>
    <tr>
      <th>618</th>
      <td>11.695247</td>
      <td>1</td>
      <td>25</td>
      <td>11.675707</td>
      <td>11.575619</td>
      <td>11.252417</td>
      <td>11.280716</td>
      <td>11.280211</td>
      <td>11.268047</td>
      <td>8.303009</td>
      <td>8.242756</td>
      <td>8.294050</td>
      <td>8.006368</td>
      <td>8.242756</td>
      <td>8.294050</td>
      <td>0</td>
    </tr>
    <tr>
      <th>17090</th>
      <td>12.468437</td>
      <td>2</td>
      <td>25</td>
      <td>12.315707</td>
      <td>12.322504</td>
      <td>12.343519</td>
      <td>12.370086</td>
      <td>12.395486</td>
      <td>12.420410</td>
      <td>9.011889</td>
      <td>9.035987</td>
      <td>9.210340</td>
      <td>9.210340</td>
      <td>9.210340</td>
      <td>9.971146</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>29802</th>
      <td>11.512925</td>
      <td>1</td>
      <td>32</td>
      <td>11.561239</td>
      <td>11.582452</td>
      <td>11.621583</td>
      <td>11.625486</td>
      <td>10.976372</td>
      <td>9.412301</td>
      <td>8.294050</td>
      <td>8.699515</td>
      <td>8.065265</td>
      <td>4.969862</td>
      <td>7.726654</td>
      <td>11.897112</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5390</th>
      <td>12.899220</td>
      <td>1</td>
      <td>37</td>
      <td>12.657982</td>
      <td>12.716438</td>
      <td>12.727161</td>
      <td>12.701878</td>
      <td>12.730973</td>
      <td>12.748885</td>
      <td>10.203592</td>
      <td>9.392662</td>
      <td>0.000000</td>
      <td>9.615805</td>
      <td>9.392662</td>
      <td>8.987197</td>
      <td>1</td>
    </tr>
    <tr>
      <th>860</th>
      <td>11.512925</td>
      <td>1</td>
      <td>26</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>15795</th>
      <td>11.849398</td>
      <td>2</td>
      <td>25</td>
      <td>11.904143</td>
      <td>11.856345</td>
      <td>11.535704</td>
      <td>11.159730</td>
      <td>10.955462</td>
      <td>10.934499</td>
      <td>8.699515</td>
      <td>8.294050</td>
      <td>9.104980</td>
      <td>7.783224</td>
      <td>0.000000</td>
      <td>7.783224</td>
      <td>1</td>
    </tr>
    <tr>
      <th>23654</th>
      <td>12.676076</td>
      <td>2</td>
      <td>36</td>
      <td>-3.689504</td>
      <td>-3.689504</td>
      <td>8.892886</td>
      <td>8.677610</td>
      <td>8.072779</td>
      <td>10.249132</td>
      <td>0.000000</td>
      <td>8.898366</td>
      <td>8.743532</td>
      <td>8.101678</td>
      <td>10.254144</td>
      <td>8.006368</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>24000 rows × 16 columns</p>
</div>




```python
# Standard OLS
import statsmodels.formula.api as smf
all_columns = "+".join(train_default.columns[:-1])
formula = "default ~ "+all_columns
print(smf.ols(formula, data=train_default).fit().summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                default   R-squared:                       0.105
    Model:                            OLS   Adj. R-squared:                  0.104
    Method:                 Least Squares   F-statistic:                     187.7
    Date:                Tue, 28 Apr 2026   Prob (F-statistic):               0.00
    Time:                        15:18:48   Log-Likelihood:                -11641.
    No. Observations:               24000   AIC:                         2.331e+04
    Df Residuals:                   23984   BIC:                         2.344e+04
    Df Model:                          15                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept      0.8012      0.038     21.365      0.000       0.728       0.875
    LIMIT_BAL     -0.0367      0.003    -12.358      0.000      -0.042      -0.031
    SEX           -0.0210      0.005     -4.003      0.000      -0.031      -0.011
    AGE            0.0016      0.000      5.663      0.000       0.001       0.002
    BILL_AMT1     -0.0049      0.001     -4.937      0.000      -0.007      -0.003
    BILL_AMT2      0.0116      0.001      8.958      0.000       0.009       0.014
    BILL_AMT3      0.0122      0.001      9.131      0.000       0.010       0.015
    BILL_AMT4      0.0083      0.001      6.372      0.000       0.006       0.011
    BILL_AMT5      0.0025      0.001      1.961      0.050    1.33e-06       0.005
    BILL_AMT6      0.0101      0.001      8.569      0.000       0.008       0.012
    PAY_AMT1      -0.0217      0.001    -19.880      0.000      -0.024      -0.020
    PAY_AMT2      -0.0187      0.001    -16.776      0.000      -0.021      -0.016
    PAY_AMT3      -0.0136      0.001    -12.383      0.000      -0.016      -0.011
    PAY_AMT4      -0.0089      0.001     -8.214      0.000      -0.011      -0.007
    PAY_AMT5      -0.0077      0.001     -7.047      0.000      -0.010      -0.006
    PAY_AMT6      -0.0025      0.001     -2.841      0.005      -0.004      -0.001
    ==============================================================================
    Omnibus:                     3616.634   Durbin-Watson:                   2.007
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):             5570.553
    Skew:                           1.180   Prob(JB):                         0.00
    Kurtosis:                       2.990   Cond. No.                         707.
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    


```python
# Collect the results for many different alpha
alpha_all = []
coef_all = []
for i in range(1,100,1):
    reg_lasso = linear_model.Lasso(alpha=i/100, random_state=seed)
    reg_lasso.fit(train_default.iloc[:,:-1], train_default.iloc[:,-1])
    coef = reg_lasso.coef_
    coef_all = coef_all + [coef]
    alpha_all = alpha_all + [i/100]
```


```python
# Plot the MSE over alpha

```


```python
# Plot the coefficients for different values of alpha, natural Feature Selection
plt.figure(figsize=(10,6),dpi=80)
plt.plot(alpha_all[:24], coef_all[:24], label=test_default.columns[:-1])
plt.legend();
```


    
![png](output_23_0.png)
    


## Optional Extra Credit Posted
You've likely noticed the new "assignment" on Canvas. It is a completely optional extra credit that will cover the Lasso and is worth 5 Assignment points. These points will be added on *after* the curve is applied. So, importantly, not doing this extra credit will have **no negative impact** on your grade. This is just a way to give people who are right on the edge of a grade cutoff to get that little boost necessary to get "bumped" up. 

Here's the calculation:
1. I will do the standard curve, splitting up the class into bins based on percentiles.
   - This will set the grade cutoffs for each letter
2. I will then add any extra credit after the cutoffs are set
   - If the extra credit pushes you above the cutoff, your letter grade will go up
3. I will then compare that grade to the grade your numerical score would earn and choose the higher of the two

## End of Content
We made it! Before we leave, I'd appreciate if you could take 5-10 minutes here completing the [course evaluation](https://heliocampusac.wisc.edu/) if you haven't already. You should be able to click on the link, login, and look for the "Available Forms" tile and click on this course. 

Since this is my first time as an instructor and first time teaching this course, you can have a very big impact on what this course looks like if I teach it again. So I would appreciate any honest, constructive feedback you have for me!

Thanks for spending part of your semester with me in Econ 390 and on Thursday we will review for the Final Exam.
