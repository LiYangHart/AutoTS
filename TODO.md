# Basic Tenants
* Ease of Use > Accuracy > Speed (with speed more important with 'fast' selections)
* Availability of models which share information among series
* All models should be probabilistic (upper/lower forecasts)
* New transformations should be applicable to many datasets and models
* New models need only be sometimes applicable
* Fault tolerance: it is perfectly acceptable for model parameters to fail on some datasets, the higher level API will pass over and use others.
* Missing data tolerance: large chunks of data can be missing and model will still produce reasonable results (although lower quality than if data is available)

## Assumptions on Data
* Series will largely be consistent in period, or at least up-sampled to regular intervals
* The most recent data will generally be the most important
* Forecasts are desired for the future immediately following the most recent data.

# Latest
* add Transformer model to sklearn DNN models
* expanded and tuned KerasRNN model options
* added param space for RandomForest, ExtraTrees, Poisson, and RANSAC regressions
* removed Tensorflow models from UnivariateRegression as it can cause a crash with GPU training
* added create_regressor function
* two new impute methods (KNNImputer, IterativeImputerExtraTrees), but only with "all" transformers
* deletion of old TSFresh model, which was horribly slow and not going to get any faster
* optimizing scalability by tuning transformer and imputation defaults
* MultivariateRegression model (RollingRegression but 1d to models)
* fix for generate_score_per_series bug with all zeroes series
* bug fix for where horizontal ensembles failed if series_ids/column names were integers

### New Model Checklist:
	* Add to ModelMonster in auto_model.py
	* add to appropriate model_lists: all, recombination_approved if so, no_shared if so
	* add to model table in extended_tutorial.md (most columns here have an equivalent model_list)

## New Transformer Checklist:
	* Make sure that if it modifies the size (more/fewer columns or rows) it returns pd.DataFrame with proper index/columns
	* depth of recombination is?
	* add to "all" transformer_dict
	* add to no_params or external if so
	* add to no_shared if so, in auto_model.py
	* oddities_list for those with forecast/original transform difference
