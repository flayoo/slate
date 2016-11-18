---
title: API Reference

language_tabs:
  - shell
  - ruby

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Notism API! You can use our API to access Notism API endpoints, which can get information on projects and users of your account.

We have language bindings in Shell and Ruby. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.


# Authentication

> To authorize, use this code:

```ruby
def api_call(action, bodyJson)
  url = "https://www.notism.io/api/v1/"+action
  uri = URI.parse(url)
  http = Net::HTTP.new(uri.host, uri.port)
  http.use_ssl = true
  
  request = Net::HTTP::Post.new(
    uri.request_uri, 
    initheader = {'Content-Type' =>'application/json', "X-Api-Key" => "abc"}
  )
  request.body = bodyJson

  response = http.request(request)
  if response.code == 200 || response.code == "200"
    return JSON.parse(response.body)
  else
    return {:error => response.code}
  end

end
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H 'NT-Api-Key: abc'  -H 'Content-Type: application/json'
```

> Make sure to replace `abc` with your API key.

Notism uses API keys to allow access to the API. You get your API Key in your [account area](https://www.notism.io/account).

Notism expects for the API key to be included in all API requests to the server in a header that looks like the following:

`X-Api-Key: abc`

<aside class="notice">
You must replace <code>abc</code> with your personal API key.
</aside>

# Projects

## Create Project

```ruby
 api_call("projects/add", '{ “type” : “design”, “name” : “My first project” }')
```


```shell
curl https://www.notism.io/api/v1/projects/add -X POST 
-H 'NT-Api-Key: abc' -H 'Content-Type: application/json' 
-d '{ “type” : “design”, “name” : “My first project” }'

```

> The above command returns JSON structured like this:

```json

  {
    "code": 200,
    "project": "1"
  }

```

This endpoint creates a new project

### HTTP Request

`POST https://www.notism.io/api/v1/projects/add`

### Query Parameters

Parameter | Description
--------- | -----------
type | The type of the workspace: <code>design</code> or <code>video</code>
name | The name of the project



