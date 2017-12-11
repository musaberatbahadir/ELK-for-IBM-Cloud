<a name="intro"></a> Perform CRUD operations with Compose for Elasticsearch
==

Elasticsearch is basically an analytics and full-text search engine. It's often used for enabling search functionality for applications. Besides providing lots of functionality and flexibility in regards to searching data, Elasticsearch is also highly scalable. [IBM Compose for Elasticsearch](https://www.ibm.com/cloud/compose/elasticsearch) makes Elasticsearch even better by managing it for you. This includes offering an easy, auto-scaling deployment system which delivers high availability and redundancy, automated no-stop backups and much more.

This tutorial will demonstrate how to perform Create, Read, Update and Delete operations with [IBM Compose for Elasticsearch](https://www.ibm.com/cloud/compose/elasticsearch).

### Table of Contents
1. [Introduction](#intro)
2. [Prerequsites](#preq) 
	1. [Download Postman](#preq1)
	2. [A Billable account](#preq2)
3. [Steps](#steps)
	1. [Create a Elasticsearch service on IBM Cloud](#create-service)
	2. [Get your Endpoint](#get-link)
	3. [Put your Index](#put-index)
	4. [Add a document to your index](#add-doc)
	5. [Add a document with id](#add-doc-id)
	6. [Get a document](#get-doc)
	7. [Update a document](#update-doc)
	8. [Delete a Document](#delete-doc)
4. [Conclusion](#conclusion)

----------


<a name="preq"></a> Prerequsites
-------------

#### <a name="preq1"></a> 1- Download Postman
Postman is a useful tool when trying to dissect RESTful APIs made by others or test ones you have made yourself. It offers a sleek user interface with which to make HTML requests, without the hassle of writing a bunch of code just to test an API's functionality.

You can dowload [here](https://www.getpostman.com/).


#### <a name="preq2"></a> 2- A Billable account 
Unfortunately IBM Compose for Elasticsearch is not available for Lite Accounts, so you are not able to follow this guide with a Lite Account. 
You can look at Billable Account types [here](https://console.bluemix.net/docs/pricing/billable.html).

<a name="steps"></a> Steps
-------------

#### <a name="create-service"></a> 1- Create a Elasticsearch service on IBM Cloud
After clicking the Catalog, you should select Data&Analystics from the menu on the left. Then you can select Compose for Elasticsearch service.
![create_service](img/0-select_from_catalog.png)

Before creating service, you should select a valid Region, Organization and Space.
  
#### <a name="get-link"></a> 2- Get your Endpoint
Your elasticsearch service will be hosted on yellow rectangular area. You will use this link as **"yourlink"** in the whole scenario.
![copy_cred](img/2-copy_endpoint)

#### <a name="put-index"></a> 3- Put your Index
Now you are finally ready to send your first request to the Elasticsearch cluster.
Open Postman application on your computer.
1. Select "PUT" from request types.
2. Paste your endpoint + indexname. It should be something like this:
https://admin:ASDFGHJKLQWERTYU@portal-ddl888-8.bmix-dal-yp-123esed2-23ss-1111-333a-32352451.asdasda-us-ibm-com.composedb.com:12345/myindex
3. You can send your request by clicking Send.
4. When you select the body, result will be seen.
![put_index](img/3-put_index.png)

#### <a name="add-doc"></a> 4- Add a document to your index
Now that you have an index, Let's add some some documents to it. You do that by sending a POST request to a URI consisting of index name, followed by a type. In this how-to our index name is "myindex" and type name is "default", that make the request URI "myindex/default".
1. Select "POST" from request types and add your endpoint /myindex/default
2. Select Body and choose Raw option to write your document.
3. You should write a json document for adding to index. In the example document has been written like:
```json
{
	"name": "Musa Berat Bahadir",
	"contents": {
		"topic": "Compose for Elasticsearch",
		"details": "CRUD operations"
	}
}
``` 
![add_doc](img/4.0-add_a_doc.png)
4. You can send your request and result will be shown when you click the Header on the left the Body.
![add_doc_res](img/4.1-add_a_doc_res.png)

Since you did not identify an id, Elasticsearch gives your document a random id.

#### <a name="add-doc-id"></a> 5- Add a document with id
For avoiding to automatically generated id, you should trace the steps below.
1. You need to change the HTTP verb to PUT and specify the id.
2. Again select Body and choose Raw option to write your document.
3. You should write a json document for adding to index. In the example document has been written like: 
```json
{
	"name": "Musa Berat Bahadir 2",
	"contents": {
		"topic": "Compose for Elasticsearch",
		"details": "CRUD operations"
	}
}
```
![add_doc_id](img/4.2-add_a_doc_with_id.png)
4. You can send your request and result will be shown when you click the Header on the left the Body.
![add_doc_id](img/4.3-add_a_doc_with_id_res.png)

#### <a name="get-doc"></a> 6- Get a document
Now, you have a couple of documents available within your index. For retrieving a document with id from your index:
1. Select "GET" from request types and add your endpoint to /myindex/default/1 to URI area.
2. Send your request.
3. Click Header to see the result.
![get_doc](img/5-retrieve_a_doc.png)

#### <a name="update-doc"></a> 7- Update a document
Instead of replacing the entire document, you can patch it by only specifying what you want.
1. Select "POST" from request types and add your endpoint to /myindex/default/1/_update
2. Select Body and choose Raw option to add your document.
3. Update API expects a JSON object and within this object you should add a "doc" property, which itself should be an object. In the example document has been written like: 
```json
{
	"doc": {
		"name": "Unidentified Flying Object",
		"tags": ["Elasticsearch", "IBM Cloud"]
	}
}
```
Within this object you can specify the fields that you would like to change ("name") or you can also add new fields with this approach("tags").
4. Now you can send your request.
![updat_doc](img/6.0-update_a_doc.png)
5. Click Headers to see the result.
![update_doc_res](img/6.1-update_a_doc_res.png)

#### <a name="delete-doc"></a> 8- Delete a Document
Deleting document is easist operation in all.
1. Select "DELETE" from request types and add your endpoint to /myindex/default/1
2. Send your request then result will appear below.
![delete_doc](img/7-delete_a_doc_res.png)

<a name="conclusion"></a> Conclusion
------
At the end of this how-to, you created an index and learned CRUD operations in Elasticsearch without installation Elasticsearch locally. 

For further, when you creating a Compose for Elasticsearch service, you are able to choose your Elasticsearch version and you are able to control your security with:
SSL incoming connections with certificate confirmation, IP whitelisting, and mandatory creation of users with passwords ensure the Elasticsearch database.
