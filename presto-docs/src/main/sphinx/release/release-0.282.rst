=============
Release 0.282
=============

**Details**
===========

General Changes
_______________
* Fix ``TEMPORARY`` defination :doc:`/sql/create-function` and :doc:`/sql/drop-function`.
* Fix a bug where ``cardinality(map_keys(x))`` and ``cardinality(map_values(x))`` would return wrong results.
* Fix several issues when building Presto on ARM based processors.
* Fix schema support in resource group static selector.
* Fix Explain (TYPE VALIDATE) to return after the analysis and ACL checks. It no longer executes the dummy query. It now returns the  ``true`` in the output column ``result`` instead of ``valid`` in case of successful execution.
* Improve error handling when using custom ``FunctionNamespaceManagers``.
* Improve null inferencing for join nodes. ``optimize_nulls_in_join`` session property is deprecated and is instead replaced with a new ``joins_not_null_inference_strategy`` session property (and corresponding configuration property ``optimizer.joins-not-null-inference-strategy``) to control null inferencing.
* Add a new UDF :func:`array_cum_sum` to return the array whose elements are the cumulative sum of the input array.
* Add a query optimization to rewrite left join with null check on right join key with semi join. It's controlled by session property `rewrite_left_join_null_filter_to_semi_join`.
* Add an optimization for queries with empty input. The optimization is controlled by session property `simplify_plan_with_empty_input`.
* Add an optimization to convert applicable cross join with an or filter to inner join. It's controlled by session property `rewrite_cross_join_or_to_inner_join`.
* Add an optimization to optimize cross join with array contains filter, it's controlled by session parameter `rewrite_cross_join_array_contains_to_inner_join`.
* Add an optimization to push down filter expression evaluation through cross join. It's controlled by session property `push_down_filter_expression_evaluation_through_cross_join`.
* Add option to use ``selectAuthorizedIdentity`` API for Presto on Spark when ``permissions.authorized-identity-selection-enable`` set to ``true``.
* Add parquet metadata caching in Apache Iceberg.
* Add preprocessing for metadata calls required for analysis. This feature is disabled by default and controlled by session property `pre_process_metadata_calls`.
* Add an additional field  ``attemptNumber`` in ``TaskId`` which is used to capture task retries in presto-on-spark. For presto classic this field will be set to ``0`` by default.
* Remove :doc:`/sql/create-function` and :doc:`/sql/drop-function` support from Presto-on-Spark.
* Upgrade Joda version to 2.12.2. Note: a corresponding update to the Java runtime should also be made to ensure consistent timezone data.
* Upgrade AWS SDK version to 1.12.261.

Hive Changes
____________
* Remove the implementation of Alluxio's metadata store because this feature won't be supported in Alluxio 300.
* Upgrade Alluxio version from 2.8.1 to 2.9.3.

JDBC Changes
____________
* Fix Truncate Table for JDBC connector.

Resource Group Changes
______________________
* Add schema support in resource group Static Selector.

**Credits**
===========

397090770, Adele Okoubo, Aditi Pandit, Ajay George, Ali Parsaei, Amit Dutta, Anant Aneja, Arpit Porwal, Arun Thirupathi, Beinan, Bin Fan, Chandrashekhar Kumar Singh, Christian Zentgraf, Chunxu Tang, Deepak Majeti, Deepak Majeti, Eduard Tudenhoefner, Facebook Community Bot, Ge Gao, George Wang, GuChangyang, HolyLow, Ivan Sadikov, Jalpreet Singh Nanda (:imjalpreet), Jaromir Vanek, Jialiang Tan, Jiayan Wei, Jon Janzen, Karteek Murthy Samba Murthy, Ke, Krishna Pai, Linsong Wang, Lisheng Guan, Lyublena Antova, Mahadevuni Naveen Kumar, Masha Basmanova, Matthew Peveler, Miaojiang (MJ) Deng, Michael Shang, Nikhil Collooru, Orri Erling, Pedro Eugenio Rocha Pedreira, Pranjal Shankhdhar, Pratyaksh Sharma, Pratyush Verma, Rebecca Schlussel, Reetika Agrawal, Rohan Pednekar, Rohit Jain, Sagar Sumit, Sanchit Kashyap, Sergey Pershin, Sergii Druzkin, Shrinidhi Joshi, Steve Burnett, Swapnil Tailor, Timothy Meehan, Vivek, Ying, Yiqun (Ethan) Zhang, Zac, Zhenxiao Luo, dnskr, ellison840611, feilong-liu, frankobe, jaystarshot, v-jizhang, xiaoxmeng
