---
question: |-
  command language interpreterはおそらくterminologyだけど、Bash is implemented to be a conformant implementation… はどっちかと判別つきません。
---

# Bash is intended to be a conformant implementation of …

## 構造
Bash is intended to be [a conformant implementation
  [of the Shell and Utilities portion
    [of the IEEE POSIX specification (IEEE Standard 1003.1)]]].

- **is intended to be** … ：普通の英語。「〜であることを意図している／目指している」
- **conformant implementation** ：規格用語。「(規格に) 準拠した実装」
- **the Shell and Utilities portion** ：POSIX の中の「シェルとユーティリティ」編という固有の区分

## 訳
Bash は、IEEE POSIX 仕様 (IEEE Standard 1003.1) のうち「シェルとユーティリティ」の部分に準拠した実装となることを目指している。

## 読み解きのポイント
- 術語かどうかの見分け方：「規格名・仕様名と結びついているか」。*implementation of 〈仕様〉* の形なら「仕様に対する実装」という技術用語。*conformant/conforming implementation* は POSIX 自身が定義している用語。
- 一方 *is intended to be* は一般英語で、「保証はしないが、そう設計している」という控えめな言い方。man page では断言を避けるときによく出る。
- 原文は *implemented* ではなく *intended*。*is implemented to be a … implementation* だと同じ語の重複になるので、英語としては不自然。

## 出典

> Bash is intended to be a conformant implementation of the Shell and Utilities portion of the IEEE POSIX specification (IEEE Standard 1003.1). (DESCRIPTION ¶2)

bash(1) — https://man7.org/linux/man-pages/man1/bash.1.html, DESCRIPTION ¶2
