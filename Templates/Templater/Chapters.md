
<%*

const parent = tp.config.active_file;

const fm = parent ? (app.metadataCache.getFileCache(parent)?.frontmatter ?? {}) : {};

let tags = fm.tags ?? [];

if (typeof tags === "string") tags = [tags];

const tagList = tags.join(", ");

const bookTitle = fm.title ?? parent?.basename ?? "";

const ch    = await tp.system.prompt("Chapter number");

const chTtl = await tp.system.prompt("Chapter title");

const padded = String(ch).padStart(2, "0");
const folder = parent?.parent?.path ?? "";
const newPath = folder ? `${folder}/${padded} - ${chTtl}` : `${padded} - ${chTtl}`;
await tp.file.move(newPath);
-%>
---
book: "<% bookTitle %>"
chapter: <% ch %>
title: "<% chTtl %>"
status: unread
tags: [<% tagList %>]
---