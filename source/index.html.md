---
title: API Reference

language_tabs:
  - php

toc_footers:
  - <a href='mailto:apikeyrequest@callingallpapers.com>Request an API-Token</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the API powering [callingallpapers.com](https://api.callingallpapers.com)!
You can use this API to access Call for Paper (CfP) endpoints to get information
on currently open CfPs.

We currently have examples for language bindings in PHP but you can consume this API
with any language you like. You can view code examples in the dark area to the right,
and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```php
$client = new GuzzleHttp\Client(['header' => [
    'Authorize' => 'Bearer myVeryOwnApiKey',
]]);
```

> Make sure to replace `myVeryOwnApiKey` with your API key.

Callingallpapers uses API keys to allow write access to the API. You can
request your Callingallpapers-API key by sending an Email to
[apikeyrequest@callingallpapers.com](mailto:apikeyrequest@callingallpapers.com)
together with a short description what you'd like to do with it.

Callingallpapers expects for the API key to be included in all API requests to
the server (except GET) in a header that looks like the following:

`Authorization: myVEryOnwApiKey`

<aside class="notice">
Remember to replace <code>myVeryOwnApiKey</code> with your personal API key.
</aside>

# Calls for Papers

## Get All Calls for Papers

```php
$client = new GuzzleHttp\Client(['header' => [
    'Authorize' => 'Bearer myVeryOwnApiKey',
]]);
$result = $client->request('GET', 'https://example.com/v1/cfp');
```

> The above command returns JSON structured like this:

```json
{
  "cfps" : [
    {
      "_rel": {
        "cfp_uri": "v1/cfp/da39a3ee5e6b4b0d3255bfef95601890afd80709"
      },
      "dateCfpEnd": "2016-01-02T13:24:35+02:00",
      "dateCfpStart": "2016-01-01T12:13:14+02:00",
      "dateEventEnd": "-001-11-30T00:00:00+00:00",
      "dateEventStart": "-001-11-30T00:00:00+00:00",
      "description": null,
      "eventUri": null,
      "iconUri": null,
      "lastChange": "2016-02-18T12:00:00+00:00",
      "latitude": null,
      "location": null,
      "longitude": null,
      "name": "foo",
      "tags": [
        ""
      ],
      "timezone": "Europe/Berlin",
      "uri": "http://example.com"
    }
  ],
  "meta" : {
    "count" : 1
  }
}
```

This endpoint retrieves all CfPs.

### HTTP Request

`GET http://example.com/v1/cfp`

### Content-Types

This endpoint can return differntly prepared data for different Content-Types.

MIME-Type | Content
----------|---------
application/json (default) | JSON-Data as described
application/rss+xml | RSS-Feed for the currently open CfPs
text/calendar | iCalendar-File for subscription in your calendaring-application
text/html | HTML-Representation


### Query Parameters

Not yet implemented!

## Get a Specific CfP

```php
$client = new GuzzleHttp\Client(['header' => [
    'Authorize' => 'Bearer myVeryOwnApiKey',
]]);
$result = $client->request('GET', 'https://example.com/v1/cfp/<HASH>');
```


> The above command returns JSON structured like this:

```json
{
  "cfps" : [
    {
      "_rel": {
        "cfp_uri": "v1/cfp/<HASH>"
      },
      "dateCfpEnd": "2016-01-02T13:24:35+02:00",
      "dateCfpStart": "2016-01-01T12:13:14+02:00",
      "dateEventEnd": "-001-11-30T00:00:00+00:00",
      "dateEventStart": "-001-11-30T00:00:00+00:00",
      "description": null,
      "eventUri": null,
      "iconUri": null,
      "lastChange": "2016-02-18T12:00:00+00:00",
      "latitude": null,
      "location": null,
      "longitude": null,
      "name": "foo",
      "tags": [
        ""
      ],
      "timezone": "Europe/Berlin",
      "uri": "http://example.com"
    }
  ],
  "meta" : {
    "count" : 1
  }
}
```

This endpoint retrieves a specific CfP. The CfP is identified by a hash which is
the sha1-sum of the URI of the event that opened the CfP.

## Create a new CfP

```php
$client = new GuzzleHttp\Client(['header' => [
    'Authorize' => 'Bearer myVeryOwnApiKey',
]]);
$result = $client->request('POST', 'https://example.com/v1/cfp', [
    'form_params' => <POST-Parameters>
]);
```

> The above command returns a Location Header with the URL of the newly created resource



### HTTP Request

`POST http://example.com/v1/cfp`

### POST Parameters

Parameter | Required | Description
--------- | -------- | -----------
dateCfpEnd | * | The date the CfP ends. This needs to be a date that can be parsed by php's ```date```function
dateCfpStart | * | The date the CfP starts. This needs to be a date that can be parsed by php's ```date```function
dateEventEnd | | The date the Event ends. This needs to be a date that can be parsed by php's ```date```function
dateEventStart | | The date the Event starts. This needs to be a date that can be parsed by php's ```date```function
description | | A description of the Conference
eventUri | * | The URI of the events homepage
iconUri | | an URI where we can find an icon for the conference. squared is prefered ;)
latitude | | The latitude of the conference-venue
location | | The longitude of the conference-venue
longitude | | The name of the conference-venue
name | * | The name of the conference
tags | | A comma-separated list of tags for the event
timezone | | A timezone name. All dates are assumed to be in that timezone. If no timezone is given "UTC" is assumed
uri | * | the URI of the CfP



## Update an existing CfP

```php
$client = new GuzzleHttp\Client(['header' => [
    'Authorize' => 'Bearer myVeryOwnApiKey',
]]);
$result = $client->request('PUT', 'https://example.com/v1/cfp/<HASH>', [
    'form_params' => <PUT-Parameters>
]);
```

> The above command returns a Location Header with the URL of the newly created resource



### HTTP Request

`PUT http://example.com/v1/cfp/<HASH>`

### PUT Parameters

Parameter | Required | Description
--------- | -------- | -----------
dateCfpEnd | * | The date the CfP ends. This needs to be a date that can be parsed by php's ```date```function
dateCfpStart | * | The date the CfP starts. This needs to be a date that can be parsed by php's ```date```function
dateEventEnd | | The date the Event ends. This needs to be a date that can be parsed by php's ```date```function
dateEventStart | | The date the Event starts. This needs to be a date that can be parsed by php's ```date```function
description | | A description of the Conference
eventUri | * | The URI of the events homepage
iconUri | | an URI where we can find an icon for the conference. squared is prefered ;)
latitude | | The latitude of the conference-venue
location | | The longitude of the conference-venue
longitude | | The name of the conference-venue
name | * | The name of the conference
tags | | A comma-separated list of tags for the event
timezone | | A timezone name. All dates are assumed to be in that timezone. If no timezone is given "UTC" is assumed
uri | * | the URI of the CfP






