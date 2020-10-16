---
title: "Pagination"
---

All core API resources have support for bulk fetches via "list" API methods.
For example, you can list access points, access rights or users.

The SALTO Nebula API uses cursor-based pagination, i.e.: it returns a “cursor”, or opaque token, with the list of results.
This token is called the `next_page_token` and can be passed with the next API request to request the next page.

The field name should match the noun in the method name in the request.
For example, There will be a maximum number of items returned based on the `page_size` field in the request.

|Common parameters|Type|Description|
|---|---|---|
|`parent`|String|The parent resource name|
|`filter`|String|A filter that chooses which resource to return. The maximum length of the filter is 20000 characters|
|`order_by`|String|How the results should be sorted|
|`page_size`|Integer|The maximum number of items to return|
|`next_page_token`|String|A value returned from a previous `List` request, if any|

### Example request

Lists access points within an installation (using Go):

```go
resp, err := client.ListAccessPoints(context.Background(), &ListAccessPointsRequest{
    Parent:   "installations/{your-installation}",
    PageSize:  2,
})
```

### Example response

```json
{
  "access_points": [
    {
      "allowed_key_types": [
        "CARD",
        "MOBILE",
        "TAG"
      ],
      "name": "installations/{your-installation}/access-points/{your-door}",
      "parent_device_name": "installations/{your-installation}/repeaters/{your-repeater}",
      "display_name": "Your Door",
      "device_id": "01000000000002"
    },
    {
      "allowed_key_types": [
        "CARD",
        "MOBILE",
        "PIN"
      ],
      "name": "installations/{your-installation}/access-points/{your-door2}",
      "parent_device_name": "installations/{your-installation}/gateways/{your-gateway}",
      "display_name": "Your door2",
      "device_id": "01000000000003"
    }
  ],
  "next_page_token": "4VoaKt6Jv85cTe0X6xtS_oi2FMh65RqDaMwYs5kN0-nXk-QLBQiaihVDdHljzMSSSgLU0I-MfNOopm5WWo9XAm9b1GqBDIpPI0aiYw=="
}
```
