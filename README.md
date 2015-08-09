# jedi-server


This package provides a server interface to jedi. This way
jedi can be easily integrated into other projects, even if the python
versions don't match.

The system is started by calling

    server.py #portnumber# #hmac_secret#

Each call is an http POST request, where the data is sent in the post body
as json. There is also a url parameter ? hmac_signature, which contains a
hex-encoded sha256 hash of (path + json + hmac_secret). This is to filter out
calls coming from anywhere but the owner.

The response is again JSON. The result will have 1 top-level element
"result", if the http status code is 200, which will contain the result,
or "error" if the https

There is for now one endpoint, mostly because I don't care too much (yet) for
GoTo.... abilities


    /getCompletions
        {
            "filepath": str
            "filedata": str
            "line": int,
            "column": int, 0-based
        }

    response:
        {
            "result": [
                {
                    "name": str,
                    "description": str,
                    "docstring": str
                    "filepath": str|null,
                    "line_num": int|null,
                    "column_num": int|null, 0-based
                }, ....
            ]
        }
