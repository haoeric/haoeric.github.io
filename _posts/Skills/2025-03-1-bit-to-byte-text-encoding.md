---
layout: post
title: Bytes, Text Encoding, and Precision in LLMs
comments: true
author: Chen Hao
categories: [Skills]
tags: [bit, byte, ASCII, UTF, FP8, FP16, encode]
---


## 1. Why 1 Byte = 8 Bits?
- A **bit** is a 0 or 1. Computers group 8 bits into a **byte**.
- Why 8? IBM’s 1960s System/360 made it standard for 256 characters (ASCII). It’s a power of 2 (2^3), good for binary math.
- **Use**: Basis for all data storage (kilobytes, megabytes).

## 2. Bytes in Text Encoding
- **ASCII**: 1 byte (8 bits) per character. 256 options (e.g., "A", "1"). English-only.
- **UTF-8**: Variable. 1 byte for ASCII (English), 3 bytes for Chinese, up to 4 for rare symbols. Supports all languages.
- **UTF-16**: 2 bytes usually, 4 for extras. Used in old Windows systems.
- **UTF-32**: 4 bytes always. Bulky, rare.
- **Example**: "Hello 世界" (Hello World) = 11 bytes in UTF-8 (5 + 2 spaces + 6).

## 3. Chinese vs. English in UTF-8
- **English**: 1 byte per letter. "Life is good" = 11 bytes.
- **Chinese**: 3 bytes per character, but concise. "生活好" = 9 bytes.
- **Trend**: Chinese often uses fewer bytes for same meaning (e.g., "I enjoy reading books in the library" = 31 bytes vs. "我喜欢图书馆读书" = 15 bytes).
- **Exception**: Short phrases like "Go now" (6 bytes) beat "现在走" (9 bytes).
- **Result**: Chinese wins for complex content.

## 4. FP8 and FP16 in Large Language Models
- **FP16 (16-bit)**: 2 bytes per number. Half the memory of FP32 (32-bit). Fast on GPUs, used in training/inference (e.g., GPT-3 = 350 GB).
- **FP8 (8-bit)**: 1 byte. Two types: E4M3 (precision) and E5M2 (range). Cuts memory further (e.g., GPT-3 = 175 GB), 2x+ faster on H100 GPUs.
- **Trade-off**: FP16 is safer, FP8 needs tuning to avoid accuracy loss.
- **Use**: Both shrink LLMs, speed up training/inference. FP8 is newer, cutting-edge.

## Summary
- **Byte**: 8 bits, set by history.
- **Encoding**: UTF-8 rules, 1-4 bytes per character.
- **Chinese**: More efficient for meaning-heavy text.
- **FP16/FP8**: 2 or 1 bytes, make AI lean and fast.
