## Search Service
Search services are everywhere, such as Google search in daily life, wiki search in work, and product search in shopping. Data in such scenarios is generally large in size and structured and has more reads than writes. However, due to their transaction characteristics, traditional databases cannot well utilize space in search scenarios and are slow in full-text searches (such as LIKE statement). Elasticsearch thus came into being.

Elasticsearch is an open-source search engine widely used in full-text search. It can quickly index, search, and analyze a massive amount of text data. Tencent Cloud ES is a highly available and scalable cloud-hosted Elasticsearch service. It well supports both structured and non-structured data and provides easy-to-use RESTful APIs and clients in multiple languages to help you quickly build stable search services.

This document describes how to use ES and SCF to quickly build a search service with the following page by referring to the official Tencent Cloud ES documentation.

## Resource Preparations
Purchase an ES cluster. The cluster scale is subject to the search service QPS and data size of the stored documents. For more information, see [Evaluation of Cluster Specification and Capacity Configuration](https://intl.cloud.tencent.com/document/product/845/19551).

## Deploying Search Service
Use the **free** SCF tool provided by Tencent Cloud to deploy the frontend page and backend service of the search service.
1. In the top-left corner of the **[Function Service](https://console.cloud.tencent.com/scf/list?rid=1&ns=default)** page in the **SCF console**, select the region of the purchased ES cluster.
![](https://qcloudimg.tencent-cloud.cn/raw/5c3424bc5c5870da166f4e3f5f032895.png)
2. Create a function service, **remember the configured function name**, and select **Next** > **Complete**.
![](https://qcloudimg.tencent-cloud.cn/raw/a7069e9ec94c74aafc03782142078268.png)
3. On the **Function Configuration** page, click **Edit** in the top-right corner, enable **Private Network Access**, select the VPC selected during ES cluster creation, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/b8d7e97e7d4a61c2b81ce772d5b183c4.png)
4. Download the [Code ZIP package](https://es-bot-1254139681.cos.ap-guangzhou.myqcloud.com/myserver.zip) to the local disk first. In **Submitting Method** on the **Function Code** page, select **Upload local ZIP package**, select the ZIP package just downloaded, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/6f2bf000c6ee0c369526fef4f502bbb7.png)
5. Modify the code on the **Function Code** page. You need to modify the `index.py` and `index.html` files:
 - Change `es_endpoint` in `index.py` to the private network address of your ES cluster, such as `http://10.0.3.14:9200`.
 - Change `es_password` in `index.py` to the password of ES Platinum Edition; if your ES is not Platinum Edition, leave it unchanged.
 - Change `server_name` in `index.html` to the name of the created SCF function, which is `myserver` by default.
>!`es_corpus_0126` is used as the index name by default in the sample. Make sure that the index is not used by other businesses. To modify it, modify the `es_index` variable in `index.py`.
6. Click **Add Trigger Method** on the **Trigger Method** page, add an API Gateway trigger as shown below, enable integration response, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/e92f88ed037542208b62e920d9d8cd03.png)
7. You can find the function **access path** in **Trigger Method** and access the page by clicking the path.
![](https://qcloudimg.tencent-cloud.cn/raw/5c93ecad3eaf7490c3a038f3e6662cc6.png)
8. Upload the sample data of [Elasticsearch Service](https://intl.cloud.tencent.com/zh/document/product/845). Click the text above the search box to automatically import data.
9. At this point, you have deployed a simple ES-based Q&A search service backend.

## More Information
### Importing stopword and custom dictionary
Stopwords will not be searched by ES, and words in the custom dictionary will be retained during segmentation. In the previous sample, the default [stopword dictionary](https://es-bot-1254139681.cos.ap-guangzhou.myqcloud.com/stopwords.dic) and [custom dictionary](https://es-bot-1254139681.cos.ap-guangzhou.myqcloud.com/user_dict.dic) are imported. You can also import your own stopword and custom dictionaries in **Plugin List** > **Update Dictionary** on the ES cluster details page.

### Synonym configuration
To configure synonyms, you need to specify them when creating an index. Synonyms in Solr and WordNet formats are supported. For more information on the format, see [Solr synonyms](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/analysis-synonym-tokenfilter.html#_solr_synonyms).
