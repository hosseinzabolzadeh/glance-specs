Image API v2 listing
====================

**Pagination**

This call is designed to return a subset of the larger collection of
images while providing a link that can be used to retrieve the next. You
should always check for the presence of a 'next' link and use it as the
URI in a subsequent HTTP GET request. You should follow this pattern
until there a 'next' link is no longer provided. The next link will
preserve any query parameters you send in your initial request. The
'first' link can be used to jump back to the first page of the
collection.

If you prefer to paginate through images manually, the API provides two
query parameters: 'limit' and 'marker'. The limit parameter is used to
request a specific page size. Expect a response to a limited request to
return between zero and *limit* items. The marker parameter is used to
indicate the id of the last-seen image. The typical pattern of limit and
marker is to make an initial limited request then to use the id of the
last image from the response as the marker parameter in a subsequent
limited request.

**Filtering**

The list operation accepts several types of query parameters intended to
filter the results of the returned collection.

A client can provide direct comparison filters using *most* image
attributes (i.e. name=Ubuntu, visibility=public, etc). A client cannot
filter on tags or anything defined as a 'link' in the json-schema (i.e.
self, file, schema).

The 'size\_min' and 'size\_max' query parameters can be used to do
greater-than and less-than filtering of images based on their 'size'
attribute ('size' is measured in bytes and refers to the size of an
image when stored on disk). For example, sending a size\_min filter of
1048576 and size\_max of 4194304 would filter the container to include
only images that are between one and four megabytes in size.

**Sorting**

The results of this operation can be ordered using the 'sort\_key' and
'sort\_dir' parameters. The API uses the natural sorting of whatever
image attribute is provided as the 'sort\_key'. All image attributes can
be used as the sort\_key (except tags and link attributes). The
sort\_dir parameter indicates in which direction to sort. Acceptable
values are 'asc' (ascending) and 'desc' (descending). Defaults values
for sort\_key and sort\_dir are 'created\_at' and 'desc'.

