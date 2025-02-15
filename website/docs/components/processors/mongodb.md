---
title: mongodb
slug: mongodb
type: processor
status: experimental
categories: ["Services"]
---

<!--
     THIS FILE IS AUTOGENERATED!

     To make changes please edit the corresponding source file under internal/impl/<provider>.
-->

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

:::caution EXPERIMENTAL
This component is experimental and therefore subject to change or removal outside of major version releases.
:::
Performs operations against MongoDB for each message, allowing you to store or retrieve data within message payloads.

Introduced in version 3.43.0.


<Tabs defaultValue="common" values={[
  { label: 'Common', value: 'common', },
  { label: 'Advanced', value: 'advanced', },
]}>

<TabItem value="common">

```yml
# Common config fields, showing default values
label: ""
mongodb:
  url: mongodb://localhost:27017 # No default (required)
  database: "" # No default (required)
  username: ""
  password: ""
  collection: "" # No default (required)
  operation: insert-one
  write_concern:
    w: ""
    j: false
    w_timeout: ""
  document_map: ""
  filter_map: ""
  hint_map: ""
  upsert: false
```

</TabItem>
<TabItem value="advanced">

```yml
# All config fields, showing default values
label: ""
mongodb:
  url: mongodb://localhost:27017 # No default (required)
  database: "" # No default (required)
  username: ""
  password: ""
  collection: "" # No default (required)
  operation: insert-one
  write_concern:
    w: ""
    j: false
    w_timeout: ""
  document_map: ""
  filter_map: ""
  hint_map: ""
  upsert: false
  json_marshal_mode: canonical
```

</TabItem>
</Tabs>

## Fields

### `url`

The URL of the target MongoDB server.


Type: `string`  

```yml
# Examples

url: mongodb://localhost:27017
```

### `database`

The name of the target MongoDB database.


Type: `string`  

### `username`

The username to connect to the database.


Type: `string`  
Default: `""`  

### `password`

The password to connect to the database.
:::warning Secret
This field contains sensitive information that usually shouldn't be added to a config directly, read our [secrets page for more info](/docs/configuration/secrets).
:::


Type: `string`  
Default: `""`  

### `collection`

The name of the target collection.


Type: `string`  

### `operation`

The mongodb operation to perform.


Type: `string`  
Default: `"insert-one"`  
Options: `insert-one`, `delete-one`, `delete-many`, `replace-one`, `update-one`, `find-one`.

### `write_concern`

The write concern settings for the mongo connection.


Type: `object`  

### `write_concern.w`

W requests acknowledgement that write operations propagate to the specified number of mongodb instances.


Type: `string`  
Default: `""`  

### `write_concern.j`

J requests acknowledgement from MongoDB that write operations are written to the journal.


Type: `bool`  
Default: `false`  

### `write_concern.w_timeout`

The write concern timeout.


Type: `string`  
Default: `""`  

### `document_map`

A bloblang map representing the records in the mongo db. Used to generate the document for mongodb by mapping the fields in the message to the mongodb fields. The document map is required for the operations insert-one, replace-one and update-one.


Type: `string`  
Default: `""`  

```yml
# Examples

document_map: |-
  root.a = this.foo
  root.b = this.bar
```

### `filter_map`

A bloblang map representing the filter for the mongo db command. The filter map is required for all operations except insert-one. It is used to find the document(s) for the operation. For example in a delete-one case, the filter map should have the fields required to locate the document to delete.


Type: `string`  
Default: `""`  

```yml
# Examples

filter_map: |-
  root.a = this.foo
  root.b = this.bar
```

### `hint_map`

A bloblang map representing the hint for the mongo db command. This map is optional and is used with all operations except insert-one. It is used to improve performance of finding the documents in the mongodb.


Type: `string`  
Default: `""`  

```yml
# Examples

hint_map: |-
  root.a = this.foo
  root.b = this.bar
```

### `upsert`

The upsert setting is optional and only applies for update-one and replace-one operations. If the filter specified in filter_map matches, the document is updated or replaced accordingly, otherwise it is created.


Type: `bool`  
Default: `false`  
Requires version 3.60.0 or newer  

### `json_marshal_mode`

The json_marshal_mode setting is optional and controls the format of the output message.


Type: `string`  
Default: `"canonical"`  
Requires version 3.60.0 or newer  

| Option | Summary |
|---|---|
| `canonical` | A string format that emphasizes type preservation at the expense of readability and interoperability. That is, conversion from canonical to BSON will generally preserve type information except in certain specific cases.  |
| `relaxed` | A string format that emphasizes readability and interoperability at the expense of type preservation. That is, conversion from relaxed format to BSON can lose type information. |



