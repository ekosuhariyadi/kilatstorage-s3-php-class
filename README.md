## KilatStorage S3 PHP Class

- - - -

About | Description
------------ | -------------
License | GPLv2 or later
License URI | http://www.gnu.org/licenses/gpl-2.0.html

### Description

This class is a standalone S3 REST implementation for PHP 5.2.x (using CURL), that supports large file uploads and doesn�t require PEAR.

This is fork from project https://github.com/CloudKilat/kilatstorage-s3-php-class
as composer project, so can be easily integrated via composer
including code update from project https://github.com/tpyo/amazon-s3-php-class

### Notes

* Not tested yet on HTTPS endpoint.

### Installation

1.  The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

    Add

    ```
    "repositories":[
        {
            "type": "git",
            "url": "https://github.com/ekosuhariyadi/kilatstorage-s3-php-class.git"
        }
    ]
    ```

    Then

    Either run

    ```
    php composer.phar require --prefer-dist codeimpact/kilatstorage-s3 "dev-master"
    ```

    or add

    ```
    "codeimpact/kilatstorage-s3": "dev-master"
    ```

    to the require section of your `composer.json` file.

### Usage

OO method (e,g; $s3->getObject(...)):

```php
$s3 = new S3($awsAccessKey, $awsSecretKey);
```

Statically (e,g; S3::getObject(...)):

```php
S3::setAuth($awsAccessKey, $awsSecretKey);
```

### Object Operations

#### Uploading objects

Put an object from a file:

```php
S3::putObject(S3::inputFile($file, false), $bucketName, $uploadName, S3::ACL_PUBLIC_READ)
```

Put an object from a string and set its Content-Type:

```php
S3::putObject($string, $bucketName, $uploadName, S3::ACL_PUBLIC_READ, array(), array('Content-Type' => 'text/plain'))
```

Put an object from a resource (buffer/file size is required - note: the resource will be fclose()'d automatically):

```php
S3::putObject(S3::inputResource(fopen($file, 'rb'), filesize($file)), $bucketName, $uploadName, S3::ACL_PUBLIC_READ)
```

#### Retrieving objects

Get an object:

```php
S3::getObject($bucketName, $uploadName)
```

Save an object to file:

```php
S3::getObject($bucketName, $uploadName, $saveName)
```

Save an object to a resource of any type:

```php
S3::getObject($bucketName, $uploadName, fopen('savefile.txt', 'wb'))
```

#### Copying and deleting objects

Copy an object:

```php
S3::copyObject($srcBucket, $srcName, $bucketName, $saveName, $metaHeaders = array(), $requestHeaders = array())
```

Delete an object:

```php
S3::deleteObject($bucketName, $uploadName)
```

### Bucket Operations

Get a list of buckets:

```php
S3::listBuckets()  // Simple bucket list
S3::listBuckets(true)  // Detailed bucket list
```

Create a bucket:

```php
S3::putBucket($bucketName)
```

Get the contents of a bucket:

```php
S3::getBucket($bucketName)
```

Delete an empty bucket:

```php
S3::deleteBucket($bucketName)
```
