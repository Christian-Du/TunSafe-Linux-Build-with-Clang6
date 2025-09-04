## Why This Guide?

TunSafe provides an official Linux installation guide on their [website](https://tunsafe.com/user-guide/linux), but it no longer works out of the box. The issue is that TunSafe's build scripts require Clang 6.0, which is no longer available through official repositories in current Debian and Ubuntu distributions.

Rather than relying on unofficial third-party sources, this guide demonstrates how to build a working TunSafe installation using only trusted sources:
- **LLVM Project**: https://github.com/llvm/llvm-project/
- **TunSafe**: https://github.com/TunSafe/TunSafe

## About This Guide

The technical solution and compilation process described here is my own work - I figured out how to solve the Clang 6.0 dependency issue through research and testing. However, since my strength is problem-solving rather than writing, I used an LLM to help make this documentation more readable and well-structured.

## ⚠️ Disclaimer

**Use at your own risk.** As of September 4, 2025:
- Both Clang 6.0 and TunSafe are **no longer actively developed or maintained**
- I am not affiliated with the TunSafe or LLVM/Clang projects
- This guide is provided as-is, without warranty of any kind
- You are solely responsible for any consequences of following this guide

**TL;DR: Everything you do with this guide is your responsibility.**
