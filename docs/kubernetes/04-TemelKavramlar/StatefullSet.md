---
layout: default
title : StatefullSet
parent: Temel Kavramlar
nav_order: 3
---

# Tanım
State tutma ihtiyacı duyan uygulamalar için Kubernetes’de StatefulSet kullanılması önerilir. Biliyoruz ki Kubernetes’de kalıcı hale getirmek istediğimiz veriyi PersistentVolume içerisinde tutuyoruz. Bu veri ile onu kullanan pod ayrı node’a giderlerse veri pod tarafından erişilemez duruma gelir. Kendi içinde küme olarak çalışan bir uygulama göz önüne alındığında ise bu çok olası bir durumdur. Bu durumun engellenmesi için de StatefulSet kullanırız.

StatefulSet
scaling-up ve scaling-down işlemlerinde pod'ları sıralı olarak ayağa kaldırır ve sıralı olarak siler.
Oluşturulan pod'ların tekilliğini garanti eder.
Data integrity’sini sağlamak içinde yaratılan StatefulSet’ler silindiği zaman kullandıkları PersistentVolume'lar silinmez.


Örnek: 3 replicalı (deployment düğümleri gibi düşüneşim) bir StatefulSet yarattığımızı düşünelim.

Deployment’ın aksine StatefulSet'te pod'lar X-1, X-2, X-3 gibi belirli bir identity ile isimlendirilir.
Pod'lar ayağa kalkarken ilk X-1, sonra X-2, sonra X-3 ayağa kalkacağını biliriz.
Aynı şekilde StatefulSet'i silerken de ilk olarak X-3 kill edilir, sonra X-2 en son da X-1 kill edilir.
Bu isimlendirmeyi yapabilmek için de StatefulSet bir Headless Serviceden faydalanılır.
Storage tarafında daha detaylı bu konuyu inceleyeceğiz.