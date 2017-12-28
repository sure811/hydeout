---
layout: post
title: LeetCode - Design Twitter
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
Design a simplified version of Twitter where users can post tweets, follow/unfollow another user and is able to see the 10 most recent tweets in the user's news feed. Your design should support the following methods:
<!--more-->

1. postTweet(userId, tweetId): Compose a new tweet.
2. getNewsFeed(userId): Retrieve the 10 most recent tweet ids in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user herself. Tweets must be ordered from most recent to least recent.
3. follow(followerId, followeeId): Follower follows a followee.
4. unfollow(followerId, followeeId): Follower unfollows a followee.
Example:
```
Twitter twitter = new Twitter();

// User 1 posts a new tweet (id = 5).
twitter.postTweet(1, 5);

// User 1's news feed should return a list with 1 tweet id -> [5].
twitter.getNewsFeed(1);

// User 1 follows user 2.
twitter.follow(1, 2);

// User 2 posts a new tweet (id = 6).
twitter.postTweet(2, 6);

// User 1's news feed should return a list with 2 tweet ids -> [6, 5].
// Tweet id 6 should precede tweet id 5 because it is posted after tweet id 5.
twitter.getNewsFeed(1);

// User 1 unfollows user 2.
twitter.unfollow(1, 2);

// User 1's news feed should return a list with 1 tweet id -> [5],
// since user 1 is no longer following user 2.
twitter.getNewsFeed(1);
```
### Java Solution
```java
Map<Integer, Set<Integer>> fans = new HashMap<>();
Map<Integer, LinkedList<Tweet>> tweets = new HashMap<>();
int cnt = 0;

public void postTweet(int userId, int tweetId) {
    if (!fans.containsKey(userId)) fans.put(userId, new HashSet<>());
    fans.get(userId).add(userId);
    if (!tweets.containsKey(userId)) tweets.put(userId, new LinkedList<>());
    tweets.get(userId).addFirst(new Tweet(cnt++, tweetId));
}

public List<Integer> getNewsFeed(int userId) {
    if (!fans.containsKey(userId)) return new LinkedList<>();
    PriorityQueue<Tweet> feed = new PriorityQueue<>((t1, t2) -> t2.time - t1.time);
    fans.get(userId).stream()
        .filter(f -> tweets.containsKey(f))
        .forEach(f -> tweets.get(f).forEach(feed::add));
    List<Integer> res = new LinkedList<>();
    while (feed.size() > 0 && res.size() < 10) res.add(feed.poll().id);
    return res;
}

public void follow(int followerId, int followeeId) {
    if (!fans.containsKey(followerId)) fans.put(followerId, new HashSet<>());
    fans.get(followerId).add(followeeId);
}

public void unfollow(int followerId, int followeeId) {
    if (fans.containsKey(followerId) && followeeId != followerId) fans.get(followerId).remove(followeeId);
}

class Tweet {
    int time;
    int id;

    Tweet(int time, int id) {
        this.time = time;
        this.id = id;
    }
}
```