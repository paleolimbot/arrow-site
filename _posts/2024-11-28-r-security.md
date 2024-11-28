---
layout: post
title: "CVE-2024-52338: Deserialization of Untrusted Data in the arrow R package (4.0.0-16.1.0)"
date: "2024-11-28 00:00:00"
author: pmc
categories: [release]
---
<!--
{% comment %}
Licensed to the Apache Software Foundation (ASF) under one or more
contributor license agreements.  See the NOTICE file distributed with
this work for additional information regarding copyright ownership.
The ASF licenses this file to you under the Apache License, Version 2.0
(the "License"); you may not use this file except in compliance with
the License.  You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
{% endcomment %}
-->

## Vulnerability description

Deserialization of untrusted data in IPC and Parquet readers in the
Apache Arrow R package versions 4.0.0 through 16.1.0 allows arbitrary
code execution. An application is vulnerable if it reads Arrow IPC,
Feather or Parquet data from untrusted sources (for example, user-supplied
input files). This vulnerability only affects the arrow R package, not other
Apache Arrow  implementations or bindings unless those bindings are
specifically used via the R package (for example, an R application that embeds
a Python interpreter and uses PyArrow to read files from untrusted sources
is still vulnerable if the arrow R package is an affected version).

It is recommended that users of the arrow R package upgrade to 17.0.0 or later.
Similarly, it is recommended that downstream libraries upgrade their dependency
requirements to arrow 17.0.0 or later. If using an affected version of the package,
untrusted data can read into a `Table` and its internal `to_data_frame()` method
can be used as a workaround (e.g.,
`read_parquet(..., as_data_frame = FALSE)$to_data_frame()`).This issue affects the
Apache Arrow R package versions 4.0.0 through 16.1.0. Users are recommended to
upgrade to version 17.0.0 or later (e.g., `install.packages("arrow")`), which
fixes the issue.

For more information, see [CVE-2024-52338](https://www.cve.org/CVERecord?id=CVE-2024-52338).
