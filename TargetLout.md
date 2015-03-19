# Lout target #

Please add here your own comments, links and ideas about the Lout target of txt2tags.


---


by Stefano Darchino

```
%------ txt2tagsrc for Lout -----------------

%%%% For locale italian
%!postproc(lout):  '@InitialLanguage { English }' '@InitialLanguage { Italian }'

%%%% For char utf-8 (Lout haven't utf-8)
%!postproc(lout):  ä  { @Char adieresis }
%!postproc(lout):  à  { @Char agrave }
%!postproc(lout):  è  { @Char egrave }
%!postproc(lout):  é  { @Char eacute }
%!postproc(lout):  È  { @Char Egrave }
%!postproc(lout):  ì  { @Char igrave }
%!postproc(lout):  ö  { @Char odieresis }
%!postproc(lout):  ò  { @Char ograve }
%!postproc(lout):  ü  { @Char udieresis }
%!postproc(lout):  ù  { @Char ugrave }
%!postproc(lout):  …  { @Char ellipsis }
%!postproc(lout):  “  { @Char quotedblleft }
%!postproc(lout):  ”  { @Char quotedblright }
%!postproc(lout):  ’  '
```