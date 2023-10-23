---
title: "LACES Documentation"
linkTitle: "Documentation"
type: "docs"
tags: []
weight: 20

cascade:
- _target:
    path: "/blog/**"
  type: "blog"
  # set to false to include a blog section in the section nav along with docs
  toc_root: true
- _target:
    path: "/about/**"
  type: "about"
- _target:
    path: "/community/**"
  type: "community"
  # set to false to include a blog section in the section nav along with docs
- _target:
    path: "/**"
    kind: "page"
  type: "docs"
- _target:
    path: "/**"
    kind: "section"
  type: "docs"
- _target:
    path: "/**"
    kind: "section"
  type: "home"
---

Please explore the LACES Documetation site. This site provides background material, terminology, and tutorials for getting started in the lab.
