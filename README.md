# Decode Ways

This repository contains a solution to the "Decode Ways" problem, a common question asked in coding interviews at companies like Facebook.

## Problem Statement

You are given a string containing digits, representing an encoded message. Your task is to determine the total number of ways to decode it.

The encoding works as follows:

- `'1' -> "A"`
- `'2' -> "B"`
- ...
- `'26' -> "Z"`

### Example

Given the input string `s = "226"`, the possible decodings are:

1. `"BZ"` (`"2"` -> `"B"`, `"26"` -> `"Z"`)
2. `"VF"` (`"22"` -> `"V"`, `"6"` -> `"F"`)
3. `"BBF"` (`"2"` -> `"B"`, `"2"` -> `"B"`, `"6"` -> `"F"`)

Thus, the total number of ways to decode `"226"` is `3`.

### Constraints

- The input string `s` contains only digits (`'0'` - `'9'`).
- The input string is non-empty and contains at least one character.

## Approach

The problem can be solved using **Dynamic Programming (DP)**. The idea is to use a DP array where each entry `dp[i]` represents the number of ways to decode the substring `s[0:i]`.

### Steps

1. **Initialization**:
   - If the first character `s[0]` is `'0'`, it cannot be decoded, so the number of ways is `0`. Otherwise, it is `1` because there is only one way to decode a single non-zero digit.
   - Initialize `dp[0] = 1` to represent an empty string (which can be "decoded" in exactly one way).

2. **State Transition**:
   - For each subsequent character `s[i]`:
     - **Single Digit Check**: If `s[i]` is between `'1'` and `'9'`, it can be decoded as a single character. Therefore, `dp[i] += dp[i - 1]`.
     - **Two Digits Check**: If the two-digit number `s[i-1:i+1]` (formed by `s[i-1]` and `s[i]`) is between `10` and `26`, it can be decoded as a double character (like "J" to "Z"). Therefore, `dp[i] += dp[i - 2]`.

3. **Final Result**:
   - The final result will be stored in `dp[n]`, where `n` is the length of the input string `s`.

## Code Implementation

Here's the Python implementation of the solution:

