---
title: "GitHub - salsa-rs/salsa: A generic framework for on-demand, incrementalized computation. Inspired by adapton, glimmer, and rustc's query system."
source: "https://github.com/salsa-rs/salsa?tab=readme-ov-file"
author:
published:
created: 2025-01-30
description:
tags:
  - "clippings"
---
## salsa[![Test](https://github.com/salsa-rs/salsa/workflows/Test/badge.svg)](https://github.com/salsa-rs/salsa/actions?query=workflow%3ATest) [![Book](https://github.com/salsa-rs/salsa/workflows/Book/badge.svg)](https://github.com/salsa-rs/salsa/actions?query=workflow%3ABook) [![Released API docs](https://camo.githubusercontent.com/eb68a1cac496947bfe83548fbdfbeea4bdec46925b76fccb6833d5e1c3f6b589/68747470733a2f2f646f63732e72732f73616c73612f62616467652e737667)](https://docs.rs/salsa) [![Crates.io](https://camo.githubusercontent.com/940a3c33fd4598d74a8d86f7dd752cd71978541b056b00e771d8646563040641/68747470733a2f2f696d672e736869656c64732e696f2f6372617465732f762f73616c73612e737667)](https://crates.io/crates/salsa)

*A generic framework for on-demand, incrementalized computation.*

[![Salsa Logo](https://raw.githubusercontent.com/salsa-rs/logo/main/FerrisSalsa4-01.svg)](https://raw.githubusercontent.com/salsa-rs/logo/main/FerrisSalsa4-01.svg)

## Obligatory warningVery much a WORK IN PROGRESS at this point. Ready for experimental use but expect frequent breaking changes.

## CreditsThis system is heavily inspired by [adapton](http://adapton.org/), [glimmer](https://github.com/glimmerjs/glimmer-vm), and rustc's query system. So credit goes to Eduard-Mihai Burtescu, Matthew Hammer, Yehuda Katz, and Michael Woerister.

## Key ideaThe key idea of `salsa` is that you define your program as a set of **queries**. Every query is used like function `K -> V` that maps from some key of type `K` to a value of type `V`. Queries come in two basic varieties:

- **Inputs**: the base inputs to your system. You can change these whenever you like.
- **Functions**: pure functions (no side effects) that transform your inputs into other values. The results of queries are memoized to avoid recomputing them a lot. When you make changes to the inputs, we'll figure out (fairly intelligently) when we can re-use these memoized values and when we have to recompute them.

## Want to learn more?To learn more about Salsa, try one of the following:

- read the [heavily commented examples](https://github.com/salsa-rs/salsa/tree/master/examples);
- check out the [Salsa book](https://salsa-rs.github.io/salsa);
- [中文版](https://rust-chinese-translation.github.io/salsa-book)
- watch one of our [videos](https://salsa-rs.github.io/salsa/videos.html).

## Getting in touchThe bulk of the discussion happens in the [issues](https://github.com/salsa-rs/salsa/issues) and [pull requests](https://github.com/salsa-rs/salsa/pulls), but we have a [zulip chat](https://salsa.zulipchat.com/) as well.