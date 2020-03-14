---
layout: post
title: Hello 6502!
parent: 6502
grand_parent: CPU
nav_order: 99
nav_exclude: true
---

# Hello 6502!
## HI MOS 6502!
## dummy document for template
```
start:
    LDA #0
    TAX
memClr:
    STX $00, X
    INX
    BNE memClr
```