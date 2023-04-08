---
layout: default
title:  Decompose By Strangler
parent: Mikroservis Ayrışması
nav_order: 2
---

# Monolitik uygulamadan geçiş (Decompose By Strangler)

Eski bir uygulamanızın geçişini sağlamak için bu pattern kullanılmaktadır. Büyük bir Monolith uygulamasını sıfırdan yeniden yazmak büyük bir çaba gerektirir ve bununla ilişkili oldukça fazla risk içerir. Bizim için en büyük zorluklardan biri eski sistem hakkında iyi bir anlayışa sahip olmaktı. Eski sistemle ilgili teknik borcu yeni modern sistemimize taşımak istemedik. Ayrıca monolitiği sıfırdan yeniden yazmaya devam ederseniz, tamamlanana kadar yeni sistemi kullanmaya başlayamazsınız. Yeni sistem geliştirilip beklendiği gibi işleyene kadar bir belirsizlik koridorundasınız .Bunun için öncelikle miniservis geçisi sonrasında mikroservis geçişini yapıyorsunuz.

Strangler Kalıbını uygulamak için 3 adım:

 1. Dönüştür
 2. Birlikte Var Ol
 3. Ortadan Kaldır

![StrangerPatter1](./../kaynaklar/stranger-pattern1.png)

Ayrıştırdıktan sonra bunun canlıda testini sağlamak için gelen trafiğin belli bölümünü buraya geçiriyorsunuz.

![StrangerPatter2](./../kaynaklar/stranger-pattern2.jpeg)

