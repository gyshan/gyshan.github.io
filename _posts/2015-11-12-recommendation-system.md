---
title: "Recommendation System"
excerpt: "Implement recommendation system by Python"
categories:
  - articles
tags:
  - Python
---

In this small article, I want to keep a record for my study experience in recommendation system. There are several parameters can evaluate a recommendation system, which are **precision**, **recall** and **F-measure**. Collaborative filtering (CF) is the most successful recommendation technique to date. There are three main categories of CF techniques: memory-based, model-based and hybrid CF algorithms (that combine CF with other recommendation techniques). 

<figure>
<img src="https://shangyblog-1256840873.cos.ap-beijing.myqcloud.com/Overview%20of%20CF.png?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKIDHKf4zkW7ZprNNZ3aLYKpm0icCbKCYNjX%26q-sign-time%3D1527753208%3B1527755008%26q-key-time%3D1527753208%3B1527755008%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3D6f6cda9d6cb61d30a06bd46dbe79ef1ecbda53c5&token=69d62916ab243b22e486b51a69d13e0482fc8d3810001&clientIP=124.254.9.174&clientUA=18df6d98-44d1-467a-9a74-b7b19dd04a0c
" alt="image">
<figcaption>Overview of collaborative filtering techniques.</figcaption>
</figure>

Today, I will mainly focus on Item-based and User-based CF techniques. The basic idea of item-based CF algorithms is to calculate the similarity between different items based on the user-item rating data and then to compute the prediction score for a given item based on the calculated similarity score, while the core of user-based CF algorithms is to provide item recommendation or prediction based on the common opinion of other like-minded users.

<figure>
<img src="https://shangyblog-1256840873.cos.ap-beijing.myqcloud.com/CF.gif?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKIDhooO9C46Q2rY1aWb1yW7xeA4hvWgywV1%26q-sign-time%3D1527753235%3B1527755035%26q-key-time%3D1527753235%3B1527755035%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3D98c90178a8c187c53e8597ef2a2a7fa48d663a55&token=6f353ab9ebab95ba6b14d79c26095ff834c819c510001&clientIP=124.254.9.174&clientUA=c28c7344-8566-47e9-809c-3481854fdf7a" alt="image">
</figure>

### Evaluation indicators for a recommendation system

| Notation | Meaning | 
|:--------|:-------:|
| P  | is the fraction of retrieved instances that are relevant. |
| R   | is the fraction of relevant instances that are retrieved.  | 
| F   | F = (2PR/(P+R)). in fact, F-measure is a measure of test's accuracy by coordinate Precision with Recall.  |
{: .table}


### Datasets

Here I want to evaluate running time of two algorithms using [MovieLens](http://grouplens.org/datasets/movielens/) datasets.

[u1.base](https://shangyblog-1256840873.cos.ap-beijing.myqcloud.com/u1.base?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKIDwUsDy5hXefH20BnGDq40zf5Zdat6sH6n%26q-sign-time%3D1527753278%3B1527755078%26q-key-time%3D1527753278%3B1527755078%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3D6d12f657e4105291129165568961e03e0e59ae6d&token=fb0507c323f2c2cda50e0055f187bc650a1c228e10001&clientIP=124.254.9.174&clientUA=e368c04e-97ba-4c5f-8367-b791c4cc47f0)
「Total 943 person, Total 1650 movies」

[u1.test](https://shangyblog-1256840873.cos.ap-beijing.myqcloud.com/u1.test?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKIDCfB5T2O7EfAhrKDOFWyhMg5KlmIVT5Vt%26q-sign-time%3D1527753299%3B1527755099%26q-key-time%3D1527753299%3B1527755099%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3D1812b190bcceb4c3b2a893cbf501e94b2b3f6768&token=e1a2f557581c98d3f2ab737c6713be46f41f764310001&clientIP=124.254.9.174&clientUA=eedf2e5f-93d1-4c8e-b46e-ef61ac6ebc3a)
「Total 459 person, Total 1410 movies」


### User-based CF & Item-based CF



{% highlight python %}
#! /usr/bin/env python
# -*- coding:utf-8 -*-
# Author: <work#shanguangyu.com>

from __future__ import division
from math import sqrt
import time


class UserBasedCF:

    def __init__(self, train_file, test_file):
        self.train_file = train_file
        self.test_file = test_file
        self.readData()
        self.userSimilarity()

    def readData(self):
        self.train, self.test = {}, {}
        for line in open(self.train_file):
            user, item, score, _ = line.strip().split("\t")
            self.train.setdefault(user, {})
            self.train[user][item] = int(score)
        for line in open(self.test_file):
            user, item, score, _ = line.strip().split("\t")
            self.test.setdefault(user, {})
            self.test[user][item] = int(score)

    def userSimilarity(self):
        # Build invese table for item_users
        self.item_users = {}
        for u, items in self.train.iteritems():
            for i in items.keys():
                if i not in self.item_users:
                    self.item_users[i] = set()
                self.item_users[i].add(u)

        C, N = {}, {}
        for i, users in self.item_users.iteritems():
            for u in users:
                N.setdefault(u, 0)
                N[u] += 1
                C.setdefault(u, {})
                for v in users:
                    if u == v:
                        continue
                    C[u].setdefault(v, 0)
                    C[u][v] += 1

        self.W = {}
        # Calculate finial similarity matrix W
        for u, related_users in C.iteritems():
            self.W.setdefault(u, {})
            for v, cuv in related_users.iteritems():
                self.W[u][v] = cuv / sqrt(N[u] * N[v])

    def recommend(self, user, K=3, N=10):
        rank = {}
        interacted_items = self.train[user]
        for v, wuv in sorted(self.W[user].items(),
                             key=lambda x: x[1], reverse=True)[0:K]:
            for i, rvi in self.train[v].items():
                if i in interacted_items:
                    # filter items user interacted before
                    continue
                rank.setdefault(i, 0)
                rank[i] += wuv * rvi

        return dict(sorted(rank.items(),
                           key=lambda x: x[1], reverse=True)[0:N])

    def evaluate(self, train=None, test=None, K=3, N=10):
        train = self.train
        test = self.test
        hit, recall, precision = 0, 0, 0
        for user in train.keys():
            tu = test.get(user, {})
            rank = self.recommend(user, K=K, N=N)
            for i, _ in rank.items():
                if i in tu:
                    hit += 1
            recall += len(tu)
            precision += N
        recall = hit / recall
        precision = hit / precision
        f = 2 * recall * precision / (precision + recall)
        return (recall, precision, f)


class ItemBasedCF:

    def __init__(self, train_file, test_file):
        self.train_file = train_file
        self.test_file = test_file
        self.readData()
        self.itemSimilarity()

    def readData(self):
        self.train, self.test = {}, {}
        for line in open(self.train_file):
            user, item, score, _ = line.strip().split("\t")
            self.train.setdefault(user, {})
            self.train[user][item] = int(score)
        for line in open(self.test_file):
            user, item, score, _ = line.strip().split("\t")
            self.test.setdefault(user, {})
            self.test[user][item] = int(score)

    def itemSimilarity(self):
        C = dict()  
        N = dict()
        for user, items in self.train.items():
            for i in items.keys():
                N.setdefault(i, 0)
                N[i] += 1
                C.setdefault(i, {})
                for j in items.keys():
                    if i == j:
                        continue
                    C[i].setdefault(j, 0)
                    C[i][j] += 1
        self.W = {}
        for i, related_items in C.items():
            self.W.setdefault(i, {})
            for j, cij in related_items.items():
                self.W[i][j] = cij / (sqrt(N[i] * N[j]))
        return self.W

    def recommend(self, user, K=3, N=10):
        rank = dict()
        interacted_items = self.train[user]
        for item, score in interacted_items.iteritems():
            for j, wj in sorted(self.W[item].iteritems(),
                                key=lambda x: x[1], reverse=True)[0:K]:
                if j in interacted_items.keys():
                    continue
                rank.setdefault(j, 0)
                rank[j] += score * wj
        return dict(sorted(rank.items(),
                           key=lambda x: x[1], reverse=True)[0:N])

    def evaluate(self, train=None, test=None, K=3, N=10):
        train = self.train
        test = self.test
        hit, recall, precision = 0, 0, 0
        for user in train.keys():
            tu = test.get(user, {})
            rank = self.recommend(user, K=K, N=N)
            for i, _ in rank.items():
                if i in tu:
                    hit += 1
            recall += len(tu)
            precision += N
        recall = hit / recall
        precision = hit / precision
        f = 2 * recall * precision / (precision + recall)
        return (recall, precision, f)

if __name__ == '__main__':
    start_time = time.time()

    # choose which method to use
    # model = UserBasedCF('u1.base', 'u1.test')
    model = ItemBasedCF('u1.base', 'u1.test')

    # The performance of model under various K
    klst = [5, 10, 15, 20, 25]
    print("recall", "precision", "f1")
    for k in klst:
        print model.evaluate(train='u1.base', test='u1.test', K=k)
    print("--- %s seconds ---" % (time.time() - start_time))

{% endhighlight %}

### Results
{% highlight text %}
User-based CF:
('recall', 'precision', 'f1')
(0.09855, 0.20901378579003183, 0.13394495412844035)
(0.1054, 0.22354188759278898, 0.14325518178729188)
(0.10725, 0.22746553552492046, 0.14576962283384304)
(0.10875, 0.23064687168610817, 0.14780835881753313)
(0.1087, 0.2305408271474019, 0.14774040095141014)
--- 13.2764439583 seconds ---

Item-based CF:
('recall', 'precision', 'f1')
(0.0974, 0.20657476139978792, 0.13238192320761127)
(0.09955, 0.21113467656415694, 0.13530411145090046)
(0.0997, 0.2114528101802757, 0.13550798504926945)
(0.09905, 0.21007423117709437, 0.1346245327896704)
(0.0981, 0.2080593849416755, 0.13333333333333336)
--- 387.862884045 seconds ---
{% endhighlight %}

### Conclusion

In short, user-based CF is appropriate for a situation that items increase fast with real-time demand, such as news recommendation. While in e-commerce, movie recommendation, items usually don't change very much, so this often can be computed off line by item-based CF.

### References

1. [A Programmer's Guide to Data Mining](https://raw.githubusercontent.com/zacharski/pg2dm-python/master/ch2/recommender.py)
2. [Item-based Collaborative Filtering Recommendation Algorithms](glaros.dtc.umn.edu/gkhome/fetch/papers/www10_sarwar.pdf)
3. [推荐系统实践 (Practice in Recommendation system)](https://book.douban.com/subject/10769749/)
4. [协同过滤实现 (Implementation of Collaborative Filtering)](http://wuchong.me/blog/2014/04/19/recsys-cf-study/)


