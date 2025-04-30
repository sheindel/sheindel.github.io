+++
date = '2025-04-15T00:08:00-05:00'
draft = true
title = 'AirTable Deep Dive, Part 2: APIs, Dynamic Schema, SDK Typings'
description = ""
slug = "at-deep-dive-2"
authors = ["Stephen Heindel"]
tags = ["airtable", "api", "sdk", "library", "metadata"]
categories = ["AirTable"]
externalLink = ""
series = ["AirTable Deep Dive"]
+++

# AirTable API

AirTable has a very nicely documented API for interacting with `Tables` and `Records`. You can write custom formulas in the API call to filter down to various records, you can paginate results, specify which fields you want returned (similar to (GraphQL)[https://graphql.org/]), and you can limit the total number of record results. While it does have some very serious performance issues (as it seems it's not *really* designed to be a primary backend API, especially given the [5 API calls per second rate limit](https://airtable.com/developers/web/api/rate-limits)), it is a very easy way to write custom "queries" from the calling SDK

# Dynamic Schema

One of the downsides to AirTable's power and flexibility is that it is very easy for a "power user" to add, delete, or rename existing fields. If all of AirTable's usage was restricted to its web UI, this wouldn't be a problem. But these changes can wreak havoc on a consuming application that is relying on that schema.

When I first took on managing the React JS application at my last role that leveraged AirTable, I quickly decided that the complexity of both the application and the data models warranted a migration to TypeScript. (While I know this can be a controversial decision in 2025 dev world where JS is king and JSDoc allegedly replaces everything we want from TypeScript, my retrospective on this move was that it has brought increased productivity and better error handling to our dev experience).

It was also around that time that I found out about AirTable's metatdata API (Accessed at https://api.airtable.com/v0/meta/*), primarily the (Base Schema Metadata endpoint)[https://airtable.com/developers/web/api/get-base-schema], which provides a list of tables in the base, and the fields in each table, along with its corresponding [Field Type](https://airtable.com/developers/web/api/field-model). This metadata API is incredibly powerful, and provides the foundation for much of the tooling discussed in this series. 

In order to combat the fragility mentioned above, we are largely concerned with two types of common changes: Renaming fields and deleting fields. Understandably, having a strong permission structure in place should be the first line of defense if reasonable: No one should be making these changes normally except for the software stakeholders whom it might affect. But when you're working at a small company, and you have quasi-technical management who are spreadsheet wizzes and for whom AirTable is more CRM than database, this can be unavoidable. Thankfully, AirTable's metadata API provides one of the keys to hardening your software against field renames, while still providing a positive user experience.

Every `Field` in AirTable has a friendly name and a corresponding `Field ID`. For instance, consider that we have a table called `Contacts` and a `Name` field. Then the metadata we get back will look something like this

```json
{
    "tables": [
        {
            "id": "tbl622YB7LCEUgXhy",
            "name": "Contacts",
            "primaryFieldId": "fldwHri9eQ64I37Qw",
            "fields": [
                {
                    "type": "singleLineText",
                    "id": "fldwHri9eQ64I37Qw",  <-- Unchanging Field ID
                    "name": "Name"              <-- Friendly Field Name
                },
                ...
        }
    ]
}
```

<!-- https://codesandbox.io/p/sandbox/react-typescript-forked-wzs2vs?file=%2Fsrc%2FApp.tsx%3A8%2C1 -->

So instead of calling 