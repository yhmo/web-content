---
id: create_partition.md
related_key: Partition
summary: Learn how to create a partition in Milvus.
---

# Create a Partitions

<div class="alert note">
<h3>Milvus Docs 需要你的帮助</h3>
本文档暂时没有中文版本，欢迎你成为社区贡献者，协助中文技术文档的翻译。<br>
你可以通过页面右边的 <b>编辑</b> 按钮直接贡献你的翻译。更多详情，参考 <a href="https://github.com/milvus-io/milvus-docs/blob/v2.0.0/CONTRIBUTING.md">贡献指南</a>。如需帮助，你可以 <a href="https://github.com/milvus-io/milvus-docs/issues/new/choose">提交 GitHub Issue</a>。
</div>


This topic describes how to create a partition in Milvus.

Milvus allows you to divide the bulk of vector data into a small number of partitions. Search and other operations can then be limited to one partition to improve the performance.

A collection consists of one or more partitions. While creating a new collection, Milvus creates a default partition `_default`. See [Glossary - Partition](glossary.md#Partition) for more information.

The following example builds a partition `novel` in the collection `book`.


<div class="multipleCode">
  <a href="?python">Python </a>
  <a href="?java">Java</a>
  <a href="?go">GO</a>
  <a href="?javascript">Node.js</a>
  <a href="?shell">CLI</a>
</div>


```python
from pymilvus import Collection
collection = Collection("book")      # Get an existing collection.
collection.create_partition("novel")
```

```javascript
await milvusClient.partitionManager.createPartition({
  collection_name: "book",
  partition_name: "novel",
});
```

```go
err := milvusClient.CreatePartition(
    context.Background(),   // ctx
    "book",                 // CollectionName
    "novel"                 // partitionName
)
if err != nil {
    log.Fatal("failed to create partition:", err.Error())
}
```

```java
milvusClient.createPartition(
        CreatePartitionParam.newBuilder()
                .withCollectionName("book")
                .withPartitionName("novel")
                .build());
```

```shell
create partition -c book -p novel
```


<table class="language-python">
	<thead>
	<tr>
		<th>Parameter</th>
		<th>Description</th>
	</tr>
	</thead>
	<tbody>
	<tr>
		<td><code>partition_name</code></td>
		<td>Name of the partition to create.</td>
	</tr>
  <tr>
		<td><code>description</code> (optional)</td>
		<td>Description of the partition to create.</td>
	</tr>
	</tbody>
</table>


<table class="language-javascript">
	<thead>
    <tr>
      <th>Parameter</th>
      <th>Description</th>
    </tr>
	</thead>
	<tbody>
    <tr>
      <td><code>collection_name</code></td>
      <td>Name of the collection to create a partition in.</td>
    </tr>
    <tr>
      <td><code>partition_name</code></td>
      <td>Name of the partition to create.</td>
    </tr>
	</tbody>
</table>

<table class="language-go">
	<thead>
    <tr>
        <th>Parameter</th>
        <th>Description</th>
    </tr>
	</thead>
	<tbody>
    <tr>
        <td><code>ctx</code></td>
        <td>Context to control API invocation process.</td>
    </tr>
    <tr>
        <td><code>CollectionName</code></td>
        <td>Name of the collection to create a partition in.</td>
    </tr>
    <tr>
        <td><code>partitionName</code></td>
        <td>Name of the partition to create.</td>
    </tr>
  </tbody>
</table>

<table class="language-java">
	<thead>
    <tr>
        <th>Parameter</th>
        <th>Description</th>
    </tr>
	</thead>
	<tbody>
    <tr>
        <td><code>CollectionName</code></td>
        <td>Name of the collection to create a partition in.</td>
    </tr>
    <tr>
        <td><code>PartitionName</code></td>
        <td>Name of the partition to create.</td>
    </tr>
  </tbody>
</table>

<table class="language-shell">
    <thead>
        <tr>
            <th>Option</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>-c</td>
            <td>The name of the collection.</td>
        </tr>
        <tr>
            <td>-p</td>
            <td>The partition name.</td>
        </tr>
        <tr>
            <td>-d (Optional)</td>
            <td>The description of the partition.</td>
        </tr>
    </tbody>
</table>

## Limits
|Feature |Maximum limit|
|---|---|
|Number of partitions in a collection|4,096|

## What's next

- Learn more basic operations of Milvus:
  - [Insert data into Milvus](insert_data.md)
  - [Build an index for vectors](build_index.md)
  - [Conduct a vector search](search.md)
  - [Conduct a hybrid search](hybridsearch.md)
- Explore API references for Milvus SDKs:
  - [PyMilvus API reference](/api-reference/pymilvus/v2.0.1/tutorial.html)
  - [Node.js API reference](/api-reference/node/v2.0.1/tutorial.html)

