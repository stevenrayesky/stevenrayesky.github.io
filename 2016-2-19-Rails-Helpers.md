---
layout: post
title: Rails Helpers
---

```
<%= link_to "", thing_path(thing.id), controller: :things, method: :delete, remote: true, data: {confirm: "Really delete this?"}, class: "thing-delete fa fa-times" %>
```