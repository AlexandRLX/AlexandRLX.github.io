---
title: Boosting方法中的特征重要性
author: c cm
layout: post
permalink: /feature_importance_in_boosting_methods/
categories:
tags:
description:
---
## XGBOOST
[source](https://github.com/dmlc/xgboost/blob/master/python-package/xgboost/core.py)

```python
   def get_score(self, fmap='', importance_type='weight'):
        """Get feature importance of each feature.
        Importance type can be defined as:
            'weight' - the number of times a feature is used to split the data across all trees.
            'gain' - the average gain of the feature when it is used in trees
            'cover' - the average coverage of the feature when it is used in trees
        Parameters
        ----------
        fmap: str (optional)
           The name of feature map file
        """
```

* weight 在tree中用到的次数计数
* gain 在tree中用到时的gain之和/在tree中用到的次数计数

## LightGBM
[source](http://lightgbm.readthedocs.io/en/latest/_modules/lightgbm/basic.html#Booster.feature_importance)

```python
    def feature_importance(self, importance_type='split'):
        """
        Get feature importances

        Parameters
        ----------
        importance_type : str, default "split"
            How the importance is calculated: "split" or "gain"
            "split" is the number of times a feature is used in a model
            "gain" is the total gain of splits which use the feature

        Returns
        -------
        result : array
            Array of feature importances.
        """
```


## CATBoosting

[source](https://github.com/catboost/catboost/blob/37378d278a57a2464547e07e48a2c779d888e174/catboost/libs/algo/calc_fstr.cpp)

#### 1. Regular feature importance

[参考](https://tech.yandex.com/catboost/doc/dg/concepts/output-data_feature-importance-docpage/)

$$feature\_total\_importance_j = feature\_importance + \sum average\_feature\_importance_i$$

* $feature\_total\_importance_j$ is the individual feature importance of the j-th feature.
* $average\_feature\_importance$ is the average feature importance of the j-th feature in the i-th combinational feature.

#### 2. Internal feature importance

[参考](https://tech.yandex.com/catboost/doc/dg/concepts/output-data_feature-interaction-strength-docpage/)

