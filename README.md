The pull API is provided on a HTTPS endpoint with access credentials being verified via a HTTP BASIC auth. The endpoint location is provided to you upon a successful application.

By default, the API operates in our simple mode only. You can enable detailed mode by contacting us.

All request responses should have gzip compression applied to them before leaving the server. Most clients and libraries should be able to handle this elegantly.

Responses may be returned in JSON format. The version selected can be determined using the request URI.

Responses will, generally, only contain information which is different from the default value, or is empty, in order to conserve space. The documentation details the default value for each property returned.
