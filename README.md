# SparkML_EMR_Network_Intrusion_detector
## Introduction
This is the data set used for The Third International Knowledge Discovery and Data Mining Tools Competition, which was held in conjunction with KDD-99 The Fifth International Conference on Knowledge Discovery and Data Mining. The competition task was to build a network intrusion detector, a predictive model capable of distinguishing between ``bad'' connections, called intrusions or attacks, and ``good'' normal connections.

## Scope and objective
Use SparkML and AWS EMR to train a model and predict the intrusion. The traning shows accptable accuracy given a small number of trees, larger trees will consume more resources of time (single nodes) or larger cluster. A SOP to instruct people on how to use the SparkMl also provide here.

## Data source
[UCI KDD Archive](http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html)


## Ppseudocode of the SOP
    1. define label column and feature columns of the dataset, example: vectorized_rdd=rdd.map(lambda x: [x[-1], Vectors.dense(x[:-1])]).toDF([‘label’, ‘features’])
    2. StringinIndexer on label, example: labelIndexer = StringIndexer(inputCol="label", outputCol="indexedLabel").fit(vectorized_rdd)
    3. VectorIndexer on features, example similar to step 2.
    4. train test split; (traningData, testData)=vectorized_rdd.randomSplit([0.7,0.3])
    5. define a classifer rf=RandomForestClasifer(labelCol=, featureCol=, numTrees=)
    6. convert back the prediction from index to original name, labelConverter=IndexToString
    7. build a pipeline, Pipeline(stages=[labelIndexer, featureIndexer, rf, labelConverter])
    8. training, model=pipeline.fit(trainingData)
    
## Deployment
Use AWS EMR notebook.
