# pluto-s3
S3 client library written in Pluto, including AWS4 and HMAC algorithms.

## Exports
```lua
function aws4_date()
function aws4_sign(user, pass, method, encoded_path, signed_headers, region = "us-east-1", service = "s3")
function aws4_auth(user, pass, method, encoded_path, signed_headers, region = "us-east-1", service = "s3")

class S3
    function __construct(url)
    function request(method, path, content, headers = {})
    function ListBuckets()

class S3Bucket extends S3
    function ListObjects()
    function PutObject(name, mime_type, content)
    function GetObject(name)
    function DeleteObject(name)
```

## Examples
These examples assume a local minio setup with default credentials. Note that minio buckets don't have their own hostname so are accessed by adding a base path.

### List buckets
```lua
local { S3 } = require "s3"
local s3 = new S3("http://minioadmin:minioadmin@localhost:9000")
print(dumpvar(s3:ListBuckets()))
```

### List objects in bucket
```lua
local { S3Bucket } = require "s3"
local mybucket = new S3Bucket("http://minioadmin:minioadmin@localhost:9000/mybucket")
print(dumpvar(mybucket:ListObjects()))
```

### Put object
```lua
local { S3Bucket } = require "s3"
local mybucket = new S3Bucket("http://minioadmin:minioadmin@localhost:9000/mybucket")
mybucket:PutObject("pluto-hello.txt", "text/plain", "Hello from Pluto!")
```

### Get object
```lua
local { S3Bucket } = require "s3"
local mybucket = new S3Bucket("http://minioadmin:minioadmin@localhost:9000/mybucket")
print(mybucket:GetObject("pluto-hello.txt")) --> Hello from Pluto!
```

### Delete object
```lua
local { S3Bucket } = require "s3"
local mybucket = new S3Bucket("http://minioadmin:minioadmin@localhost:9000/mybucket")
mybucket:DeleteObject("pluto-hello.txt")
```
