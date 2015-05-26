MSAccessDBALDriver
==================

[![Build Status](https://travis-ci.org/royopa/MSAccessDBALDriver.svg?branch=master)](https://travis-ci.org/royopa/MSAccessDBALDriver)

DBAL Driver to use with Microsoft Access.

## Requiring/Loading

If you're using Composer to manage dependencies, you can include the following
in your composer.json file:

```json
{
    "require": {
        "royopa/ms-access-dbal-driver": "dev-master"
    }
}
```

## Usage

```php
<?php
header('Content-Type: text/html; charset=utf-8');

require 'vendor/autoload.php';

$dsn = 'odbc:Driver={Microsoft Access Driver (*.mdb, *.accdb)};Dbq=MyDatabase.mdb;';

try {
    $connPdo = new PDO($dsn);
} catch (PDOException $e) {
    echo $e->getMessage() . '</br>';
}

$config = new \Doctrine\DBAL\Configuration();
$connectionParams = array(
    'user'     => null,
    'password' => null,
    'pdo'      => $connPdo,
    'driverClass' => 'Royopa\Doctrine\DBAL\Driver\MSAccess\Driver\Driver',
);

$conn = \Doctrine\DBAL\DriverManager::getConnection($connectionParams, $config);

$sql = 'SELECT * FROM myTable';
$stmt = $conn->query($sql);

while ($row = $stmt->fetch()) {
    echo $row['columnName'] . '</br>';
}
```
