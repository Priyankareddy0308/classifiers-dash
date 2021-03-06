# classifiers-dash-app
A Dash web app for binary classification model selection

![](https://github.com/taylorplumer/classifiers-dash/blob/master/resources/classifier-dash-app_screenshot.png)

A demo deployed to Heroku is available for viewing at the following address: <https://classifier-dash-app.herokuapp.com/>

The demo is not mobile friendly so please view on desktop/PC for full functionality.

### Summary
This repository contains working code for deploying a binary classificaiton model selection tool to a Dash app locally. 

The inspiration for this tool came from Issue #1044<sup>1</sup> of the Yellowbrick project "to create an at-a-glance representation of multiple model scores so that I can easily compare and contrast different model instances." The heatmap below is my solution, albeit outside the scope of the Yellowbrick project itself given the use of Dash/Plotly instead of Matplotlib. Utilizing the interactivity of Dash/Plolty, I extended the solution to incorporate existing yellowbrick classification visualizations, named visualizers. 

The web app consists of three components:
1. A dropdown allowing the user to view models with training data either as-is or synthetically upsampled to address any class imbalance. The default is no upsampling. The upsample.py module within the utils directory can provide details on the upsampling method.
2. A heatmap containing precision, recall, and f1 scores for each sklearn model along with the following:
    - macro average: averaging the unweighted mean per label
    - weighted average: averaging the support weighted mean per label<sup>2</sup>
3. When hovering over associated row in heatmap for sklearn model, model-specific images of matplotlib plots will appear that were populated from utilizing Yellowbrick classification visualizers.<sup>3</sup>
    - ROCAUC: Graphs the receiver operating characteristics and area under the curve.
    - Precision-Recall Curves: Plots the precision and recall for different probability thresholds.
    - Classification Report: A visual classification report that displays precision, recall, and F1 per-class as a heatmap.
    - Confusion Matrix: A heatmap view of the confusion matrix of pairs of classes in multi-class classification.

The data used in the example is the 'default of credit card clients Data Set' from the UCI Machine Learning Repository.<sup>4</sup> If you would like to use your own data then place the file in the Data/Input directory and provide the command line arguement as noted below in the Instructions.

### Instructions:
1. Review config.py file to select appropriate sklearn classifiers, yellowbrick visualizers, and filesystem structure for your needs
2. Input your data in the data input filepath directory with the target variable as the first column followed by the feature columns.
3. Run the following commands in the project's root directory to set up the data and images.

    - To create the yellowbrick classificaiton visualizer images and model scores output file named report_df.csv. Note that an input data filepath is needed as an arguement i.e. credit.csv
        
        `python process_data.py credit.csv`

4. To run the Dash Plotly web app.
    
        `python app.py`

5. Go to http://127.0.0.1:8050/


###  Installation
After creating a virtual environment (recommended), you can install the dependencies with the following command: 

```
pip install -r requirements.txt
```

### References
<sup>1</sup> https://github.com/DistrictDataLabs/yellowbrick/issues/1044

<sup>2</sup> https://scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html

<sup>3</sup> https://www.scikit-yb.org/en/latest/api/classifier/index.html

<sup>4</sup> http://archive.ics.uci.edu/ml/datasets/default+of+credit+card+clients
