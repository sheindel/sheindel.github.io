+++
date = '2025-04-15T00:08:00-05:00'
draft = false
title = 'AirTable Deep Dive, Part 1: Introduction'
description = ""
slug = "at-deep-dive-1"
authors = ["Stephen Heindel"]
tags = ["airtable", "api"]
categories = ["AirTable"]
externalLink = ""
series = ["AirTable Deep Dive"]
+++

# What is AirTable?

Over the past 3 years, I have been regularly using and developing tooling around [AirTable](https://airtable.com/), a no-code/low code platform that provides a powerful Excel/Spreadsheet style experience, including very Excel-like [formulas](https://support.airtable.com/docs/formula-field-reference), a user friendly [lookup](https://support.airtable.com/v1/docs/lookup-field-overview) in place of SQL foreign keys, and [rollup](https://support.airtable.com/docs/rollup-field-overview) which has a hint of SQL join.

Despite some well known pains, including a very aggressive [API limit](https://support.airtable.com/docs/managing-api-call-limits-in-airtable), a [pricing](https://community.airtable.com/product-operations-69/airtable-pricing-updates-for-2023-are-a-slap-in-the-face-for-pro-users-40253) [change](https://www.reddit.com/r/Airtable/comments/15ziz1n/new_airtable_pricing_updates/) that took their large user base by surprise, and some very public bugs which have caused production downtimes for my own services, their product is truly unique and powerful with a wide variety of convenience features that appeal haevily to business interests. It integrates a [Forms](https://support.airtable.com/building-and-sharing-forms-in-airtable) feature that provides powerful and configurable data ingestion, nicely built customized auto-generated API documentation (located at https://airtable.com/{your_base_id}/api/docs), a surprisingly robust [permissions system](https://support.airtable.com/docs/airtable-permissions-overview), and a wide set of [batteries included integrations](https://www.airtable.com/integrations), to name a few of its more impressive features.

# Series Goals

In this series, my goal is to dig into some specifics of using AirTable, both its primary data API as well as its metadata API, and to demonstrate some tooling I've developed overtime to improve the usability of AirTable as a both a data backend and a user-friendly CRM. I won't bother to repease descriptions and definitions that AirTable has already nicely defined in its [AirTable Basics](https://support.airtable.com/docs/introduction-to-airtable-basics) documentation, so if you're new to AirTable, I would recommend you read through that first. I will be using the terms `Base`, `Table`,  `Record`, `Field`, and `View` with the assumption that you know what they mean. 

Over the course of this series, I hope to address some common pain points with AirTable, including
- Dynamic schema/SDK typing (TypeScript focus)
- SDK formulas (Python focus)
- Formula Dependency Decoupling
- Automatic Dependency Graph Generation

If you have other input or questions about any of my work, or need AirTable consulting specifically or AirTable consulting in general, feel free to [reach out](/contact)