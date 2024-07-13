---
layout: default
title:  Event -Driven Architecture
parent:  Mikroservislerde haberleşme
nav_order: 1
---

# Event -Driven Architecture

![Senkron ve Asenkron iletişim](./../kaynaklar/sync-async.png)

**Senkron**: Synchronous communication (senkron iletişim), bir veri alışverişi işleminin iki taraf arasında gerçek zamanlı olarak gerçekleştirildiği bir iletişim yöntemidir. İki taraf arasında belirli bir sırayla ve zamanlama ile bilgi alışverişi yapılır.Bu iletişim yönteminde, veri gönderen taraf, veriyi göndermeden önce veri alıcı tarafın hazır olduğunu doğrulamak için bekler. Veri alıcı taraf, veri gönderen tarafın işlemi tamamlamasını bekler ve ardından yanıt verir. Senkron iletişimde, veri gönderme işlemi tamamlanmadan önce veri alışverişi tamamlanmaz.

Senkron iletişimde, veri alışverişi işleminin bir tarafından kaynaklanan bir gecikme, diğer taraftaki işlemi geciktirebilir. Bu nedenle, yüksek trafikli uygulamalarda senkron iletişim yerine, asenkron iletişim tercih edilmelidir.

**Asenkron**: Veri alışverişinde gerçek zamanlı olmayan bir iletişim yöntemidir.Asenkron mesaj bize scability,reciliency ve High availability sağlar.

**Event-driven architecture (EDA)**: Etkinlik temelli mimari anlamına gelir. Bu mimari, bir sistemdeki bileşenlerin birbirleriyle iletişim kurmasını ve işlemlerini olaylara (event) yanıt olarak gerçekleştirmesini sağlar.EDA, birçok farklı bileşenin etkileşim içinde olduğu karmaşık sistemlerde kullanılır. Bu bileşenler, birbirleriyle doğrudan iletişim kurmak yerine, bir aracı olarak hareket eden bir olay akışı (event stream) üzerinden iletişim kurarlar. Bu sayede, bir bileşenin diğer bir bileşenin durumunu sürekli olarak takip etmesi yerine, olayların oluşması durumunda olay akışından gelen bilgiyi kullanarak ilgili işlemi gerçekleştirir.

- Publish/Subscribe Pattern: Bu pattern, bir veya daha fazla kaynaktan gelen olayları dinleyen ve olayların işlenmesi için bir veya daha fazla tüketicinin kaydolduğu bir yayın kanalı kullanır. Bu sayede kaynaklar ve tüketiciler arasındaki bağımlılık azaltılarak uygulamanın ölçeklenebilirliği artırılır.
- Event Sourcing Pattern: Bu pattern, uygulamanın durumunu ve önceki işlemlerini takip etmek için olayların kaydedilmesini kullanır. Bu şekilde uygulamanın mevcut durumu, geçmiş olayların birleştirilmesiyle elde edilir. Bu pattern, uygulamaların ölçeklenebilirliğini artırır ve aynı zamanda kaynakların anlık durumunu kaydetme konusunda daha esnek olmalarına olanak tanır.
- CQRS (Command Query Responsibility Segregation) Pattern: Bu pattern, okuma işlemlerinin yazma işlemlerinden ayrılmasını ve bunların farklı uygulama katmanlarında ele alınmasını sağlar. Bu, uygulamaların ölçeklenebilirliğini artırır ve aynı zamanda farklı işlemlere farklı hizmet düzeyleri sunmalarına olanak tanır.
- Sagas Pattern: Bu pattern, uzun ömürlü ve karmaşık iş akışlarına sahip uygulamalar için kullanılır. Bu pattern, iş akışındaki her adımda bir olayın tetiklenmesi ve bir sonraki adımda hangi işlemin gerçekleştirileceğine karar verilmesiyle çalışır. Bu, uygulamaların daha karmaşık senaryolarda çalışmasına olanak tanır.

## Publish/Subscribe Pattern

Servisler arası haberleşmenin event mesajlar üzerinden asenkron şekilde yapılmasını sağlamaktadır. FIFO(first in first out) ilk giren ilk çıkacak şekildedir
Publisher mesajları üretip gönderirken Subscribers ise mesajı tüketmek ile sorumludur.
