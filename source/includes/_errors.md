# Errors

<aside class="notice">
Here is how to interpret errors you might encounter. <code>error</code>. Errors below are no reason for panic.
</aside>

The RAYPACK API uses the following error codes:


Error Code | Meaning
---------- | -------
200 | Upload successful -- Your file was uploaded successfully.
500 | Unauthorized -- Your API key is wrong.
501 | Forbidden -- There is a problem with your API key.
502 | Invalid key format -- Please check the format of your key.
503 | Internal server error -- There has been a problem with our server. Please contact us for further support.
505 | No api keys -- Your requests have been used up. Please purchase additional requests.
506 | Invalid model ID -- The model ID in your request is invalid.
507 | Model Response error --
508 | Model returns no data -- Please check if the file you uploaded is correct.
