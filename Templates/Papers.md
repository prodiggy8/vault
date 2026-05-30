---
type: paper
source: "{{url}}"
description:
title: "{{title}}" 
citekey: {{citekey}}
author: [{{authors}}]
{% if date %}year: {{ date | format("YYYY") }} {% endif %}
aliases:
- "{{title}}"
tags: [papers]
zotero: "{{desktopURI}}"
status: to-read
date created:
date modified:
---

> [!abstract]
> {{abstractNote}}