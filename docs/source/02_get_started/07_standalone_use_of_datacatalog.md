# Standalone use of the `DataCatalog`

## Introduction

To make it easier to share a Jupyter notebook with others you need to avoid hard-coded file paths used to load or save data. One way to explore data within a shareable Jupyter notebook is take advantage of Kedro's [`DataCatalog`](https://kedro.readthedocs.io/en/stable/05_data/01_data_catalog.html), but in the early phases of a project, you may not want to use any other Kedro features.

The Kedro starter with alias `standalone-datacatalog` (formerly known as `mini-kedro`) provides this minimal functionality. You can specify the sources required to load and save data using a YAML API. For example:

 ```yaml
# conf/base/catalog.yml
example_dataset_1:
  type: pandas.CSVDataSet
  filepath: folder/filepath.csv

example_dataset_2:
  type: spark.SparkDataSet
  filepath: s3a://your_bucket/data/01_raw/example_dataset_2*
  credentials: dev_s3
  file_format: csv
  save_args:
    if_exists: replace
```

This makes it possible to interact with data within your Jupyter notebook, with code much like this:

```python
df = catalog.load("example_dataset_1")
df_2 = catalog.save("example_dataset_2")
```

## Usage

Create a new project using the [`standalone-datacatalog` starter](https://github.com/quantumblacklabs/kedro-starters/tree/master/standalone-datacatalog):

```bash
$ kedro new --starter=standalone-datacatalog
```

## Content

The starter comprises a minimal setup to use the traditional [Iris dataset](https://www.kaggle.com/uciml/iris) with Kedro's [`DataCatalog`](../05_data/01_data_catalog.md).

The starter contains:

* A `conf/` directory, which contains an example `DataCatalog` configuration (`catalog.yml`)
* A `data/` directory, which contains an example dataset identical to the one used by the [`pandas-iris`](https://github.com/quantumblacklabs/kedro-starters/tree/master/pandas-iris) starter
* An example notebook showing how to instantiate the `DataCatalog` and interact with the example dataset
* A blank `README.md` which points to this page of documentation

## Create a full Kedro project

When you later wish to build a full pipeline, you can use the same configuration, with the following steps:

***1. Create a new empty Kedro project in a new directory***

Let's assume that the new project is created at `/path/to/your/project`:

```bash
kedro new
```

***2. Copy the `conf/` and `data/` directories from your `standalone-datacatalog` starter project over to your new project***

```bash
cp -fR {conf,data} `/path/to/your/project`
```
