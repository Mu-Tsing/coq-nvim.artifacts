# Machine Generated

Used by [`coq.nvim`](https://github.com/ms-jpq/coq_nvim)

I revise the requirement in coq_nvim plugin, as I found maybe it's a bug about some snippets in LaTex under the VimTex environment.

I found the inline math and unlabeled math snippets can't has correct jump label. 

The original snippets of coq_nvim has some symbol like ``:#:'', which make it failure to jump and generated the content in my VimTex, macOS arm:
```json
    "Snippet_NAME": {
      "content": "$${1:#:expression}$",
      "doc": "",
      "filetype": "tex",
      "grammar": "snu",
      "label": "$$ expression $$",
      "matches": {
        "$": true,
        "mathexpression": true
      }
    },
```
actually, it generates something like ``$expression'' with real string content other than a jumpable label. So I fork this repository and revise it to:

```json
"96895ba9-a433-329c-8791-d721fb408265": {
      "content": "$ ${1} $ ${0}",
      "doc": "",
      "filetype": "tex",
      "grammar": "snu",
      "label": "$$ expression $$",
      "matches": {
        "$": true,
        "mathenva": true
      }
    },
```
however, it still can't work. I guess there are something I don't know about the snippets with the '$' symbol. So I use the '\\\(\\\)' to express inline math and '\\\[\\\]' for math block, it works with correct jumpable label:
```json
"...": {
      "content": "\\[\n${1}\n\\]\n${0}",
      "doc": "",
      "filetype": "tex",
      "grammar": "snu",
      "label": "$$ expression $$",
      "matches": {
        "dm": true,
        "mathenva": true
      }
    },
```

If I have more time, I will check which session the error occurs. But right now, this "fork-revise" method is acceptable for me; as I also has a easier way to write some snippet without other plugins.