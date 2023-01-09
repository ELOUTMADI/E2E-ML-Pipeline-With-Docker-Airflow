# ml_pipeline

This code defines a DAG in [Airflow](https://airflow.apache.org/) that represents an end-to-end machine learning pipeline. The pipeline includes the following tasks:

## Task 1: Creating Storage Structures
This task group consists of two sub-tasks:
1. Creating an "experiment tracking" table in a PostgreSQL database using the `creating_experiment_tracking_table` operator.
2. Creating a "batch data" table in the same database using the `creating_batch_data_table` operator.

## Task 2: Fetching Data
This task uses the `fetching_data` operator, which is a Python operator that calls the `load_data` function to fetch data.

## Task 3: Preparing Data
This task group consists of two sub-tasks:
1. Preprocessing the data using the `preprocessing` operator, which is a Python operator that calls the `preprocess_data` function.
2. Saving the preprocessed data to the "batch data" table using the `saving_batch_data` operator, which is a Python operator that calls the `save_batch_data` function.

## Task 4: Hyperparameter Tuning
This task uses the `hyperparam_tuning` operator, which is a Python operator that calls the `experiment` function to tune the hyperparameters of a machine learning model.

## Task 5: After Cross-Validation
This task group consists of two sub-tasks:
1. Saving the results of the hyperparameter tuning process to the "experiment tracking" table using the `saving_results` operator, which is a Python operator that calls the `track_experiments_info` function.
2. Fitting the best model using the `fitting_best_model` operator, which is a Python operator that calls the `fit_best_model` function.

The pipeline has a schedule interval of `@daily`, which means that it will run once a day. It has a default start date of November 22, 2022, and the `catchup` parameter is set to `False`, which means that the pipeline will only run for the current date and not for past dates. If any task in the pipeline fails, the `email_on_failure` parameter is set to `False`, so no email will be sent. If a task succeeds, an email will be sent to `eloutmadiabderrahim@gmail.com`. The owner of the pipeline is `Me`.
