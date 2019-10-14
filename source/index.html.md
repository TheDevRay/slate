---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>-</a>

includes:
  - auth
  - users
  - errors
  - validation_rules

search: true
---

# Introduction

Welcome to the Spouser API!

Down here you will fond some endpoints, examples, etc. to get you going.

All the `POST`, `PUT` and `PATCH` endpoints, should be able to accept `json`.
But ofcourse the good ol' form parameters will always work.

> The default headers, which I bet you could guess would look something like this.

```json
headers: {
  // 'Authorization': 'Bearer <GENERATED_ACCESS_TOKEN>',
  'Content-Type': 'application/x-www-form-urlencoded',
  'Accept-Language': 'application/json',
  'X-Requested-With': 'XMLHttpRequest'
}
```
