# My notes for the AWS certified solutions architect associate course on A Cloud Guru

Unsorted, un-organized and only what I find interesting.

Hope they are helpful, do whatever you want with the notes.

Can be typeset into a pdf for example by using _pandoc_ and the commands below (with some custom settings to latex)

```shell
$ for f in *.md; do cat $f; echo; done > all.md
$ pandoc all.md -o all.pdf --from markdown --pdf-engine=lualatex -V geometry:margin=2cm -V documentclass:scrartcl -V fontfamily:libertine
```
