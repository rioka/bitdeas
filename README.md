# Bitdeas Tech Notes

My repo to collect notes, ideas, and so on...

## Tech details

Built using [MkDocs](https://mkdocs.org).

Other options were considered or evaluated, namely
- [Bookdown](https://github.com/yihui/bookdown-minimal) 
  (via R.Project/R.Studio)
- [Gitbook](https://www.gitbook.com/) 
  Nice, but does not longer generate a static site (or I've not been able to figure out how it could be done using recent versions)
- [Joplin](https://joplinapp.org/)
  Multiplatform (via electron) application
- [mdBook](https://rust-lang.github.io/mdBook/index.html)
  Similar to MkDocs, apparently less popular (but may be badly wrong)
- [Orchid](https://orchid.run/)
  Seems interesting, but too lazy to take a look now.

## MkDocs Quick Start

- Create a repo in github
  - In `Settings -> Github pages -> Source`, select `gh-pages` as 

- Install mkdocs (e.g. using [chocolatey](https://chocolatey.org/))
- Create a site (`mkdocs new <folder>`)
- Publish to github pages (`mkdocs gh-deploy`)
 
### MkDocs Plugins 

Quite a few interesting [plugins](https://github.com/mkdocs/mkdocs/wiki/MkDocs-Plugins).

Another quite large list available [here](https://www.wheelodex.org/entry-points/mkdocs.plugins/).

Interesting, there are plugins for both [PlantUML](https://plantuml.com/) and [mermaid](https://mermaid-js.github.io/mermaid/).
