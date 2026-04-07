---
share: true
uuid: dedecb5f-c142-402e-84d4-126b3e6cda9f
---
[Home : Hypothesis](https://web.hypothes.is/)

#### [[Social Media Message Format]]


We are going to request some JSON from their API in my [[Hypothes.is API Tutorial]]

``` JSON

{
  "id": "P0NTJrK7Ee6mOqM8a5CFPQ",
  "created": "2024-01-14T08:59:38.479713+00:00",
  "updated": "2024-01-14T08:59:38.479713+00:00",
  "user": "acct:dentropy@hypothes.is",
  "uri": "https://gutenberg.net.au/ebooks13/1303661h.html",
  "text": "So religions are frameworks for makeing decisions!!!!!!",
  "tags": [],
  "group": "__world__",
  "permissions": {
	"read": [
	  "group:__world__"
	],
	"admin": [
	  "acct:dentropy@hypothes.is"
	],
	"update": [
	  "acct:dentropy@hypothes.is"
	],
	"delete": [
	  "acct:dentropy@hypothes.is"
	]
  },
  "target": [
	{
	  "source": "https://gutenberg.net.au/ebooks13/1303661h.html",
	  "selector": [
		{
		  "type": "RangeSelector",
		  "endOffset": 96,
		  "startOffset": 0,
		  "endContainer": "/p[56]",
		  "startContainer": "/p[56]"
		},
		{
		  "end": 46032,
		  "type": "TextPositionSelector",
		  "start": 45936
		},
		{
		  "type": "TextQuoteSelector",
		  "exact": "\"YES,\" objects a reader, \"but does not our religion tell us\n  what we are to do with our lives?\"",
		  "prefix": " — RELIGION IN THE NEW WORLD\n\n  ",
		  "suffix": "\n\n  We have to bring religion, a"
		}
	  ]
	}
  ],
  "document": {
	"title": [
	  "The Open Conspiracy"
	]
  },
  "links": {
	"html": "https://hypothes.is/a/P0NTJrK7Ee6mOqM8a5CFPQ",
	"incontext": "https://hyp.is/P0NTJrK7Ee6mOqM8a5CFPQ/gutenberg.net.au/ebooks13/1303661h.html",
	"json": "https://hypothes.is/api/annotations/P0NTJrK7Ee6mOqM8a5CFPQ"
  },
  "user_info": {
	"display_name": "dentropy"
  },
  "flagged": false,
  "hidden": false
},
```