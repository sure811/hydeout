---
layout: post
title: LeetCode - Encode and Decode TinyURL
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition

TinyURL is a URL shortening service where you enter a URL such as https://leetcode.com/problems/design-tinyurl and it returns a short URL such as http://tinyurl.com/4e9iAk.

Design the encode and decode methods for the TinyURL service. There is no restriction on how your encode/decode algorithm should work. You just need to ensure that a URL can be encoded to a tiny URL and the tiny URL can be decoded to the original URL.
<!--more-->

### Java Solution
```java
public class Codec {
    HashMap<String, String> hashToUrl = new HashMap<String, String>();
    HashMap<String, String> urlToHash = new HashMap<String, String>();
    String tinyUrlBase = "http://tinyurl.com/";
    String characters = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    Random random = new Random();

    // Encodes a URL to a shortened URL.
    public String encode(String longUrl) {
        if (urlToHash.containsKey(longUrl))
            return tinyUrlBase + urlToHash.get(longUrl);

        StringBuilder hash = new StringBuilder();
        do {
            for (int i=0; i<6; i++) {
                hash.append(characters.charAt(random.nextInt(characters.length())));
            }
        } while (hashToUrl.containsKey(hash.toString()));

        hashToUrl.put(hash.toString(), longUrl);
        urlToHash.put(longUrl, hash.toString());
        return tinyUrlBase + hash.toString();
    }

    // Decodes a shortened URL to its original URL.
    public String decode(String shortUrl) {
        return hashToUrl.get(shortUrl.substring(tinyUrlBase.length()));
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(url));
```