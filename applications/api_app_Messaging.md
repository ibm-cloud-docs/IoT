---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# HTTP Messaging API for applications
{: #rest_messaging_api}

## Publishing events and commands
{: #event_command_publication}

In addition to using the MQTT messaging protocol, you can also configure your applications to publish events and commands to the {{site.data.keyword.iot_short_notm}} over HTTP by using one of the following HTTP REST API commands:

### Non-secure event POST request
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>
{: codeblock}

### Secure event POST request
<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>
{: codeblock}

### Non-secure command POST request
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></code></pre>
{: codeblock}

### Secure command POST request
<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></code></pre>
{: codeblock}

If you are connecting a device or application to the Quickstart service, replace **orgId** with the string 'quickstart'.

NOTE: While applications can reuse an HTTP connection to post events or commands to different devices, the authorization HTTP header cannot be changed.

## Authentication

All requests must include an authorization header. Basic authentication is the only method that is supported. Applications are authenticated by using API keys. When an application makes any request through the  {{site.data.keyword.iot_short_notm}} HTTP REST API, the following credentials are required:

```
username = API key (for example, a-orgId-a84ps90Ajs)
password = Authentication token
```

## Content-Type request headers

A `Content-Type` request header must be provided with the request. The following table shows how the supported types are mapped to the {{site.data.keyword.iot_short_notm}} internal formats.

|Content-Type header|Format in {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

## Quality of service

Similar to the MQTT quality of service "at most once" delivery service level 0, HTTP REST messaging provides non-persistent message delivery but it validates that the request is correct and that it can be delivered to the server before it sends the HTTP response. A reply that contains a HTTP status code of 200 confirms that the message was delivered to the server. When you use either the "at most once" MQTT quality of service level or the HTTP equivalent to deliver event messages, the device or application must implement retry logic to guarantee delivery.


For more information about the MQTT protocol and the quality of service levels for {{site.data.keyword.iot_short_notm}}, see [MQTT messaging](../reference/mqtt/index.html).

## Accessing the HTTP Messaging API documentation
{: #rest_messaging_api}

To access the {{site.data.keyword.iot_short_notm}} HTTP Messaging API documentation and find more information about sending events, see [{{site.data.keyword.iot_short_notm}} HTTP Messaging API ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}.