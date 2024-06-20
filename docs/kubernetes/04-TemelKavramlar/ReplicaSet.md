---
layout: default
title : ReplicaSet
parent: Temel Kavramlar
nav_order: 2
---


# Tanım

Yatay olarak ölçeklendireceğimiz pod'ların çalışması gereken replica sayılarını vererek replicaSet olarak çalıştırabiliriz. Örnek vermek gerekirse, replica:3 olarak verilmiş bir ReplicaSet belirtilen pod'dan kesinlikle 3 tane çalışacağını garanti eder. Pod'lar zaman zaman hata verse bile tekrar ayağa kaldırmaya çalışır. Deployment olmadığı zaman ölçeği söylemek için kullanılır. deployment varsa replicasets deployment içerisinden yönetilir.
