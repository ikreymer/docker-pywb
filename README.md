# pywb Docker setup

Docker setup for [pywb Python Wayback](https://github.com/ikreymer/pywb).

pywb is a web archive replay and live web proxy rewriting system.


### Running With Live Web Proxy

To run a container of this image:

```
docker run -it ikeymer/pywb
```

This will start pywb with a live web proxy configured at `http://[DOCKER_HOST]:8080/live/`
For example, the live rewrite of `http://example.com/` can be viewed at `http://[DOCKER_HOST]:8080/live/http://example.com/'


### Creating a Web Archive With Pywb

pywb supports creating collections with the `wb-manager` utility, which can be run from Docker as well.

For example, the following can be used to add a WARC from `/path/to/mywarc/warc_file.warc.gz` to a new collection called `test`
and store it in a Docker volume, mapped to local `/path/to/my_collection/`

```
# Init Collection 'test'
docker run -it -v /path/to/collection:/webarchive ikeymer/pywb wb-manager init test

# Add warc to collection 'test'
docker run -it -v /path/to/collection:/webarchive -v /path/to/mywarc/:/warcs/ ikeymer/pywb wb-manager init add /warcs/warc_file.warc.gz`

# run pywb
docker run -it -p 8080:8080 -v /path/to/collection:/webarchive ikreymer/pywb
```

The contents of the warc can now be browsed at `http://[DOCKER_HOST]:8080/test/[url]`


The mapping to `/webarchive` volume can be omitted if the collection need not be accessed outside of Docker.


### Running with An Existing Web Archive

This image exposes the `/webarchive` volume which can be used to store all the pywb collections and config files.

It can be used to create a new archive as shown above or map an existing web archive for pywb.


Refer to  [pywb documentation](https://github.com/ikreymer/pywb) for additional pywb usage info.





