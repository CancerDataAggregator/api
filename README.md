# CDA API Design and design documents

_The API is specified using [OpenAPI 3.0](http://spec.openapis.org/oas/v3.0.3)
syntax. It can be pre-viewed using VS Code plugins, or on the web with a variety
of web viewers. It is a text based format and can also be read on its own_


1. Queries can be done in a multi-step manner, each step refining the last.
1. Each query receives a unique query id which can be used when chaining
   multi-step queries, to retrieve the query or retrieve analyses about the
   query, or in case of asynchronous queries, retrieve the status of the query.
   This also mitigates issues related to URL lengths.
1. POST is used for security and query size/complexity considerations    


# Considerations and constraints

1. URL passed by client/browser should not be longer than 2048 characters to
   mitigate certain kinds of DDOS attacks ([1][url-length]). For this reason we use
   a query id when chaining queries and when referring to them, to avoid building
   up a very long URL. We also use a POST operation even though it's operation
   for idempotent queries is frowned upon. Arguably, most of the `/query` calls
   will not be strictly idempotent since they cache queries. 


[url-length]:
https://stackoverflow.com/questions/3091485/what-is-the-limit-on-querystring-get-url-parameters


# References

1. https://www.kennethlange.com/7-tips-for-designing-a-better-rest-api/
1. https://dropbox.tech/developers/limitations-of-the-get-method-in-http
1. https://evertpot.com/dropbox-post-api/

