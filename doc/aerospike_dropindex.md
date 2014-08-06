
# Aerospike::dropIndex

Aerospike::dropIndex - drops a secondary index

## Description

```
public int Aerospike::dropIndex ( string $ns, string $name )
```

**Aerospike::dropIndex()** will drop a secondary index from
a namespace with a specified index *name*.

## Parameters

**ns** the namespace

**name** the name of the index

## Return Values

Returns an integer status code.  Compare to the Aerospike class status
constants.  When non-zero the **Aerospike::error()** and
**Aerospike::errorno()** methods can be used.

## Examples

```php
<?php

$config = array("hosts"=>array(array("addr"=>"localhost", "port"=>3000)));
$db = new Aerospike($config, 'prod-db');
if (!$db->isConnected()) {
   echo "Aerospike failed to connect[{$db->errorno()}]: {$db->error()}\n";
   exit(1);
}

$res = $db->dropIndex("test", "user_email_idx");
if ($res == Aerospike::OK) {
    echo "Index user_email_idx was dropped from namespace 'test'\n";
else if ($res == Aerospike::ERR_INDEX_NOT_FOUND) {
    echo "No such index exists.\n";
} else {
    echo "[{$db->errorno()}] ".$db->error();
}

?>
```

We expect to see:

```
Index user_email_idx was dropped from namespace 'test'
```
