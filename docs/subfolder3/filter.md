---
title: Filter
description: Guide on how to use the SALTO Nebula filter
---

## SALTO Nebula filter expressions

In order to simplify your API usage and enrich API consumption you can make a decision about how many and what results you want to show.

You can do this by using filter expressions which are an advanced way to filter queries in Nebula without the need for custom implementations for each use case.

## Example expressions

1. Equals, filter by field:

    Example: `display_name == 'Baker Street elevator'`  

2. Using logical operators (&&, ||, ...):

    Example: `display_name == 'Baker Street elevator' || name == 'installations/surelock-homes-hq/gateways/conan-doyle-gateway'`

3. Using parentheses:

    Example: `(display_name == 'Baker Street elevator' && name == 'installations/surelock-homes-hq/gateways/conan-doyle-gateway') || display_name == 'Maintenance door'`

## Supported expressions

You can use filters to limit your terms so they only apply to specific fields within applicable objects.
Preface a term with one of the filters in the table below.
The more terms you provide in your query, the more specific the results you'll get.

|  Operator        |  Description |  Type        |
|------------------|--------------|--------------|
| `!`           | `not`. Is not equal to “FOO” (is any value except “FOO”), matches “pizza”, “trash”, “fun” but not “foo” | `bool` |
| `&&`          | `and`. Is equal to “FOO” and “BAR” | `bool` |
| `\|\|`          | `or`. Is equal to either “FOO” or “BAR” | `bool` |
| `==`          | `equals`. Is equal to “FOO”, exactly  | `string`, `int` |
| `!=`          | `not equals`. Is not equal to “FOO”, exactly  | `string`, `int` |
| `in`          | Is in a list containing "FOO" | `string`, `int` |
| `contains`    | Contains “FOO”, matches “buffoon” and “fast food”  | `string` |
| `endsWith`    | Ends with “FOO”, matches “buffoo” and “fast foo” but not “buffoon” or “fast food”  | `string` |
| `startsWith`  | Starts with “FOO”, matches “foolish” and “food” but not “buffoon” or “fast food” | `string` |

### Notes

1. Matches in string filters are **case insensitive**, eg. the expressions `SHERLOCK` and `sherlock` will match the word “Sherlock”
2. Some filters can only be applied to strings eg. `contains`, `startsWith`, `endsWith` whereas others, for example, `equals` support both strings and ints
3. Filter terms are in `camelCase`
4. The maximum length of the filter is 20000 characters
5. Filters can be combined using `or`, `and` and `not` boolean logic

## Example request

Below you can find an example request for a user search.
Examples are in JSON format.

```json
{
  "parent": "installations/surelock-homes-hq",
  "page_size": 10,
  "filter": "display_name.startsWith('Sherlock')"
}
```

## Example response

```json
{
  "users": [
    {
      "name": "installations/surelock-homes-hq/users/01DMDAFG5GGW8XNJYTTFA4XCJ6",
      "first_name": "Sherlock",
      "last_name": "Holmes",
      "display_name": "Sherlock Holmes",
      "email": "sherlock@surelockhomes.com",
      "activate_time": {
        "seconds": "1568110176",
        "nanos": 0
      },
      "expire_time": null
    }
  ],
  "next_page_token": ""
}
```

## Example request with Boolean operator

Each Boolean operator can be wrapped in parentheses to group and / or change the precedence when executing the query. For example:

```json
{
  "parent": "installations/surelock-homes-hq",
  "page_size": 10,
  "filter": "(display_name.startsWith('sherlock') || display_name.startsWith('john’)) && display_name.endsWith('watson')"
}
```

## Error handling

* Filtering on a service that doesn't contain filter functionality will result in an error which currently looks something like this:  
`2 UNKNOWN: ERROR: <input>:1:1: undeclared reference to 'field'`

* Filtering using a combination of more than 3 expressions will result in an error, eg.  
`2 UNKNOWN: expr: limit of 3 depth level exceed`

## Best practices

Filtering is provided on `List` methods (or similar methods to query a collection, such as `Search`).
Many searches can be performed with a single term.
Use something that would be fairly atypical, such as a name or email address.
If you are seeing too few results, make the term less specific.
If there are too many results, include additional terms, one at a time.

## Filter by date

You can also filter over `google.protobuf.Timestamp` types.
This is useful if you want to filter for events such as access point openings that take place within an installation over a specific time period.

The following is an example of a `ListEvents` using the parameter `occur_time`:

```json
{
  "parent": "installations/acme",
  "page_size": 10,
  "filter": "occur_time <= timestamp('2020-05-27T13:35:36.697714Z')"
}
```

You can use the following operators in the date filter:

```operators
>
<
>=
<=
```

You can combine these with `&&` and `||`.
