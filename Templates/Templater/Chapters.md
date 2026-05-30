<%*

const parent = tp.config.active_file;

const fm = parent ? (app.metadataCache.getFileCache(parent)?.frontmatter ?? {}) : {};

const ch = await tp.system.prompt("Chapter number");

const padded = String(ch).padStart(2, "0");

let tags = fm.tags ?? [];

if (typeof tags === "string") tags = [tags];

const tagList = tags.join(", ");

const title = fm.title ?? "";

const author = fm.author ?? "";

const citekey_b = fm.citekey ?? parent?.basename;

const citekey = `${citekey_b}_${padded}`

const year = fm.year ?? "";
const alias = `${fm.title} - ${ch}`
const folder = parent?.parent?.path ?? "";
const newPath = folder ? `${folder}/${citekey}` : citekey;
await tp.file.move(newPath);
-%>
---
type: chapter
description:
title: "<% title %>"
author: "<% author %>"
chapter: "<% ch %>"
chapter title:
citekey: "<% citekey %>"
aliases: [<% alias %>]
tags: [<% tagList %>]
status: to-read
date created:
date modified:
---

Book: [[<% citekey_b %>|<% title %>]]

# Chapter <% ch %>
