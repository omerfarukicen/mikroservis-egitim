---
layout: default
title: Mikroservis çözümü
parent: Mikroservis Giriş
nav_order: 2
---

# Mikroservis Nedir?

 Tek başına, tek sorumluluğu olan ve tek iş yapan sadece o işe ait işleri yürüten modüler projelerdir.Monolitik mimariler başlığında belirtilen sorunlardan kurtulmanın bir yolu mikroservis mimarisine geçmektir. Mikroservis, tanımı gereği küçük,geliştirilmesi ortalama iki üç hafta süren, bağımsız (otonom), diğer mikroservislerle sıkı sıkıya bağımlılığı bulunmayan, tek başına çalışan, kendine ait veritabanı olan, geliştirme sürecinden kuruluma kadar bağımsız olan,yatayda ve dikeyde kendi başına ölçeklenebilen uygulamalardır.

## Ölçeklenebilirlik

![Monolitik Uygulama](kaynaklar/olceklenebilirlik.jpg)

Mikroservisler, her biri belirli bir işlevselliği yerine getiren küçük, bağımsız hizmetlerdir. Bu, her bir mikroservisin farklı bir kaynağı işlemesi ve ayrı bir ölçeklendirme seviyesine sahip olması anlamına gelir. Böylece, bir mikroservisin artan talebi karşılamak için ölçeklendirilmesi, tüm uygulamanın ölçeklendirilmesine gerek kalmadan gerçekleştirilebilir.

## Bağımsız geliştirme ve Yayınlama

Monolitik mimarilerde modülerlik, programlama dili yapıları ile (örneğin Java'da package) ya da derleme varlıkları ile ifade edilir. Monolitik uygulamalarda modülerliği koruyan bir yapı yoktur. Zaman geçtikce modüller arasındaki bağımlılık artar ve yönetilemez duruma gelir. Mikroservislerde ise modülerlik birimi servislerdir.Contract uygun şekilde bağımsız deploy işlemleri yapabilir

## Hata izolasyonu

Mikroservislerden birinde oluşan hata herhangi bir domino etkisi oluşturmadan sadece ilgili mikroservis etkilenir.Diğer mikroservisler hizmet etmeye devam eder.

## Teknoloji Bağımsızlığı

  Her mikroservisin ihtiyaç duyulan teknoloji ile yazılabilir. Gelişen teknoloji dünyasında uygulamanızın yeni teknolojilere adaptasyonu ve geçişi kolaylaştıracaktır.

## Dezavantajları

* Karmaşıklık artmasına 
* İşletim Maliyetlerinin artmasına 
* Test etkinlik sürelerinin artması 

neden olmaktadır.