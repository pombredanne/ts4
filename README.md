# ts4: time series simple storage service

A blob store backed by S3 and indexed by SimpleDB accessible via a simple HTTP API.

Backup a stream of blobs and retrieve it in chronological order.

## API

### /api/upload

A multipart/form-data endpoint, sha1 of the blob must be computed and used as name.

	$ curl -v -include  --form aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d=hello http://localhost:8010/api/upload	

### /api/blob/{hash}

Get the raw blob data.

	$ curl http://localhost:8010/api/blob/aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d
	hello

### /api/blobs?start=&end=

Retrieves blobs saved during the given range (start/end).

Start defaults to 0 and end to time.Now().UTC().

The time attributed is sorted lexicographically so any subset of time.RFC3339Nano will works.

	$ curl http://localhost:8010/api/blobs?start=2015-01
	{
    		"data": [
        	  {
        	    "hash": "aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d", 
        	    "time": "2015-01-06T23:21:47.718317501Z"
        	  }
    		], 
    		"end": "2015-01-06T23:23:12.069583002Z", 
    		"start": "2015-01"
	}

## License

MIT

