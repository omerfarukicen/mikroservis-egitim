---
layout: default
title:  Service
parent: Network
nav_order: 1
---

## Tanım
Service, pod’ların ön tarafında konumlanan ve gelen istekleri karşılayıp arka tarafta pod'ları mantıksal olarak gruplayıp servis olarak dışarıya sunmamızı sağlayan objedir. Buradaki mantıksal gruplama ise Kubernetes’in sunduğu Labels & Selectors ile sağlanmaktadır. Default olarak loadbalancing yapar.Bir servis birden çok deploymenta hizmet verebilir.  kube-proxy yeni servis ve end-pointleri izler ve servis oluşturulunca yönlendirilmeye başlar.  Her servis kendini kubernetes dns servisine bildirir. Bir service NodePort, LoadBalancer, ClusterIP veya externalName yöntemleri ile hizmet verebilir.