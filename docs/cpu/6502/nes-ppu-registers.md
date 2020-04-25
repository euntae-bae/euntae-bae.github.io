---
layout: post
title: "패미컴: PPU 레지스터(WIP)"
parent: 6502
grand_parent: CPU
nav_order: 22
---

|이름      |주소 |방향|비트 구성  |설명                                                                |
|:--------:|:---:|:--:|:---------:|:------------------------------------------------------------------:|
|PPUCTRL   |$2000|RW  |`VPHB SINN`|PPU 제어 레지스터 1                                                 |
|PPUMASK   |$2001|RW  |`BGRs bMmg`|PPU 제어 레지스터 2                                                 |
|PPUSTATUS |$2002|R   |`VS0- ----`|PPU 상태 레지스터                                                   |
|OAMADDR   |$2003|W   |`aaaa aaaa`|OAM(Object Attribute Memory 또는 스프라이트 메모리)의 주소 지정     |
|OAMDATA   |$2004|RW  |`dddd dddd`|OAM(스프라이트 메모리) 데이터                                       |
|PPUSCROLL |$2005|W   |`xxxx xxxx`| |
|PPUADDR   |$2006|W   |`aaaa aaaa`|PPU 메모리(CPU 메모리와는 다르다) 주소를 지정하기 위한 주소 레지스터|
|PPUDATA   |$2007|RW  |`dddd dddd`|PPU 메모리의 데이터를 읽거나 쓰기 위한 데이터 레지스터              |
|OAMDATA   |$4014|W   |`aaaa aaaa`| DAM Access to the Sprite Memory |

### 참고 자료
* <http://fms.komkon.org/EMUL8/NES.html>
* <http://wiki.nesdev.com/w/index.php/PPU_registers>