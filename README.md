<img src='https://raw.githubusercontent.com/Milenaafeworki/Tanzanian_water_well/master/images/new-handpump-mod-need-to-crop.png'>

[Image source](https://rwsn.blog/2016/06/17/water-spillovers-and-free-riding-the-economics-of-pump-functionality-in-tanzania/)



# Tanzanian Water Well Functionality Classification.

Tanzania, as a developing country, struggles with providing clean water to its population of over 57,000,000. There are many water points already established in the country, but some are in need of repair while others have failed altogether. Using data from Taarifa and the Tanzanian Ministry of Water, we need to predict which pumps are functional, which need some repairs, and which don’t work at all. A smart understanding of which water points will fail can improve maintenance operations and ensure that clean, potable water is available to communities across Tanzania. 


## Business Problem

This project aims to use the data to anticipate when a well needs repair or maintenance, ideally before it breaks and disrupts the local water supply. Failing to identify nonfunctional water supply lines could lead villagers to suffer in many ways, including traveling long distances to other water sources, increased time and effort to fetch water, or even being victims of different health-related issues that come with poor water quality. Accordingly,  though it is important to build a model that will accurately classify the wells, it is crucial that our model's tollerance to errors of misclassifying wells, especially the 'nonfunctional' and 'needs repair' groups, is as low as possible.  

## The OSMEN Process

For this project, we will follow the OSEMN process of data science inquiry. It is split into five stages which include:

- Obtain
- Scrub
- Explore
- Model
- Interpret


## The Data

The raw data from [Tanzanian Water Well](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/page/23/) contains the following columns:

- **amount_tsh** -     Total static head (amount water available to waterpoint)
- **date_recorded** -  The date the row was entered
- **funder** -         Who funded the well
- **gps_height** -     Altitude of the well
- **installer** -      Organization that installed the well
- **longitude** -      GPS coordinate
- **latitude** -       GPS coordinate
- **wpt_name** -       Name of the waterpoint if there is one
- **num_private** -
- **basin** -          Geographic water basin
- **subvillage** -     Geographic location
- **region** -         Geographic location
- **region_code** -    Geographic location (coded)
- **district_code** -  Geographic location (coded)
- **lga** -            Geographic location
- **ward** -           Geographic location
- **population** -     Population around the well
- **public_meeting** - True/False
- **recorded_by** -    Group entering this row of data
- **scheme_management** - Who operates the waterpoint
- **scheme_name** -       Who operates the waterpoint
- **permit** -            If the waterpoint is permitted
- **construction_year** - Year the waterpoint was constructed
- **extraction_type** -   The kind of extraction the waterpoint uses
- **extraction_type_group** - The kind of extraction the waterpoint uses
- **extraction_type_class** - The kind of extraction the waterpoint uses
- **management** -        How the waterpoint is managed
- **management_group** -  How the waterpoint is managed
- **payment** -           What the water costs
- **payment_type** -      What the water costs
- **water_quality** -     The quality of the water
- **quality_group** -     The quality of the water
- **quantity** -          The quantity of water
- **quantity_group** -    The quantity of water
- **source** -            The source of the water
- **source_type** -       The source of the water
- **source_class** -      The source of the water
- **waterpoint_type** -   The kind of waterpoint
- **waterpoint_type_group** - The kind of waterpoint



**Here is an image of the location of the wells classified according to their functionality.**

<img src='https://raw.githubusercontent.com/Milenaafeworki/Tanzanian_water_well/master/images/functionality%20map.png'>

## Modeling

After cleaning the data and dealing with missing values either by replacement or completely dropping irrelevant features, the next step was to explore different trends with the help of visualizations before moving on to modeling.

<img src='https://raw.githubusercontent.com/Milenaafeworki/Tanzanian_water_well/master/images/quantity.png'>

### Evalution metrics

Evaluation results were chosen using the f1_macro scorer considering it calculates f1 for each class and takes the average, meaning it will give the same importance to each label/class. This gives greater weight to smaller classes which are ideal for this project. F1 was also chosen as the metric because it gives a better measure of the incorrectly classified cases than the Accuracy Metric.


### Process

Modeling involved iterating through parameters of the following model types with GridSearchCV and SMOTE on the following model types:

- K-Nearest Neighbors - KNNClassifier

- Random Forest - RandomForestClassifier

- XGBoost - XGBClassifier

## Conclusions and Interpretation


The overall best model was Random Forrest which performed considerably better than other models at predicting which wells were functional but need repair.(Recall score)

**Random forest:** 

   1. Baseline model
    
    Non functional  (77%)     
    Functional      (87%)   
    Functional needs repair  (29%) 
    
    
   2. Gridsearch CV
    
    Non functional  (68%)     
    Functional      (92%)   
    Functional needs repair  (10%)
    
    
   3. SMOTE
    
    Non functional  (69%)     
    Functional      (79%)   
    Functional needs repair  (55%)

 Given more time and with some more tunning it may be able to increase its performance.
 
 ## Further Study

1. Identify and indicate wells that are no longer functional due to being past their life span.

2. Review which extraction types last longer in supply and quality of water.

3. Identify companies with a record of poor installation, and lack of maintenance.

4. Include date records of maintenance, accurate population size and Construction year.


```
├── images
├── notebook
├── presentation.pdf
├── tanzanian_water_wells.ipynb
├── README.md
├── SubmissionFormat.csv
├── test_set_values.csv
├── training_set_labels.csv
└── training_set_values.csv
```