This section describes how to manage the configurations of certain advanced cluster features, such as customizing dictionaries for IK analysis plugin and modifying the `elasticsearch.yml` parameter.
On the cluster list page, click a cluster ID to enter the cluster details page, and click **Advanced Configuration** to enter the advanced configuration management page.  

## Plugin configuration

### IK analysis plugin

In the plugin configuration section, you can see the IK analysis plugin pre-installed in the cluster. For more information on this plugin, see [IK Analysis Plugin for Elasticsearch](https://github.com/medcl/elasticsearch-analysis-ik). You can use it to create an index of Chinese keywords for your data stored in the ES cluster to implement searches.
![Plugin list](https://main.qcloudimg.com/raw/154b2967d33d4c35194d26bf3600c9b0.png)

Click **Update Dictionary** to enter the dictionary update page, where you can see two options: non-stopwords and stopwords. After selecting the dictionary file to be updated, click **Save** to update it. 
![Dictionary update page](https://main.qcloudimg.com/raw/4e95c5d4daec6b4e3933a8bf2e599869.png)

Requirements for dictionary files:  

- **Dictionary type:** There are two categories of words: "non-stopwords" and "stopwords". The "non-stopwords" dictionary specifies IK as the analyzer when data is stored to the ES cluster for index creation. If the data stored contains a word in this category, an index will be created and can be queried and found using keywords. "Stopwords" will be deliberately avoided and will not be indexed.  
- **Restrictions and requirements:** There are certain restrictions and requirements for dictionary files. For example, a dictionary file should contain one word per line and be encoded in UTF-8. For avoidance of confusion, the name of a non-stopword file should not be the same as that of a stopword file. In addition, as dictionary files will be loaded into the memory, you are allowed to upload a maximum of 10 files of up to 10 MB in size each.  
- **Update process:** The list displays the dictionaries that have been uploaded and updated. A new dictionary will be blocked during upload if it does not meet the requirements. After a file is uploaded, it will be displayed in "pending activation" status. After all dictionaries to be updated are uploaded, click **Save**, and they will be saved to your cluster and take effect. If there is a file that fails to be uploaded or is not in UTF-8 format, a failure will be prompted, and you need to delete the failing file before you can click Save for other ones to take effect.

## YML configuration

### Viewing configuration items

In the cluster details, click **Advanced Configuration** to view the configuration items.

![Advanced configuration](https://main.qcloudimg.com/raw/23295ca21c455935da183884a538b2f6.png)  

| Configuration Item | Description | Value Range |
| ----------------------------------- | ------------------------------------------ | --------------------------------- |
| action.destructive_requires_name | Whether it is required to specify the index name when deleting an index | true or false. Default value: true |
| indices.fielddata.cache.size | Specifies the percentage of Java heap space allocated to the field data | Percentage in the format of 1-100%. Default value: 15% |
| indices.query.bool.max_clause_count | Specifies the maximum number of clauses allowed in a Lucene Boolean query | Positive integer. Default value: 1024 |

For more information on the configuration items, see [Elasticsearch's official documentation](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/index.html).

### Modifying a configuration item
Click **Batch Modify** to modify configuration items. Applicable restrictions are as described above.  
![Batch modify](https://main.qcloudimg.com/raw/23295ca21c455935da183884a538b2f6.png)
>If the cluster health status is YELLOW or RED, or there is an index in the cluster that has no replicas, you will be prompted to force restart if you try to modify the configuration items. In this case, there will be a high risk if you update the configuration, and you are recommended to repair the cluster status first by adding replicas to all indices.

If you are aware of the risk and still want to update the configuration, you can check the "Force Restart" box and click **OK** to restart. For more information, see the figure below:

![Force modify configuration](https://main.qcloudimg.com/raw/d6b085413a583953f5454d9d144057a9.png)

Click **Batch Modify** to modify the corresponding configuration items. Applicable restrictions are as described above.  
![Batch modify](https://main.qcloudimg.com/raw/ec66e8a0364cbcfd5494bbb51cdf5e34.png)  

If you want to customize other configuration items, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
