---
layout: post
title: Hello 6502!
parent: 6502
grand_parent: CPU
nav_order: 1
---

# Hello 6502!
## HI MOS 6502!
```
start:
    LDA #0
    TAX
memClr:
    STX $00, X
    INX
    BNE memClr
```