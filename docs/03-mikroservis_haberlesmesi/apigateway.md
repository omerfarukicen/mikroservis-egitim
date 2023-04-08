---
layout: default
title:  ApiGateway Pattern
parent: Mikroservislerde haberleşme
nav_order: 3
---

# ApiGateway Pattern

Büyük mikroservis yapılarında tavsiye edilen bir tasarım desenidir.

Faydaları:

## 1.Reverse Proxy

 Bir sunucu mimarisi öğesidir ve gelen istekleri ön uç sunucudan (client) alarak, arka uç sunucularına (server) yönlendiren bir tür ara sunucudur. Bu sayede, istemcilerin doğrudan arka uç sunucularına erişmelerine gerek kalmadan, önyüzdeki (frontend) sunucular üzerinden iletişim kurabilmeleri sağlanır

## 2.  Response cache

 Client yapılan istekler gateway üzerinde cachelenir ve bu sayede latency düşürülür.

## 3. Rate limiting

Bir servisin veya API'nin, kullanıcıların belirli bir zaman aralığında yaptıkları istek sayısını sınırlandırması anlamına gelir.

- Güvenlik sağlama: Rate limiting, aynı kaynaktan gelen istek sayısını sınırlandırarak, DDoS saldırılarına karşı koruma sağlar.

- İş yükünü dengeleme: Rate limiting, farklı kullanıcılara eşit davranarak, sunucu kaynaklarının dengeli kullanımını sağlayarak, aşırı yüklenmeden kaçınır.

## 4. Load balancing

Bir ağdaki yükü birden fazla sunucu arasında eşit şekilde dağıtarak, ağın performansını artırmak ve hizmet kesintilerini önlemek için kullanılan bir yöntemdir.

- Yüksek performans ve Yüksek erişebilirlik sağlar

## 5. Authentication-Authorization

İlgili backend servislerine erişmeden güvenlik katmanını gateway üzerinde konumlandırabiliyoruz.

## 6. Retry Policy

Dağıtık sistemlerde kullanılan bir politika türüdür. Servis kesintilerinin önlenmesi amacıyla yapılmaktadır.

## 7.Circuit Breaker

 Circuit breaker, hataları algılar ve uygulamanın başarısız işlem sayısı belirli bir eşiği geçmesi durumunda ise yeniden kullanılabilir hale gelene kadar işlemleri engeller.

## 8. IP checklist

   Belirli ip erişimleri sağlanarak  yada erişimleri engellenerek güvenlik arttırılabilir.

## 9.Request Transformation

Client gelen isteklerin header veya bir alan eklenmesi gibi işlemleri yaptıktan sonra ilgili servise yönlendirme işlemi yapabilir.

## 10. Api Composition

Birden fazla API'yi birleştirerek, daha kompleks ve işlevsel bir hizmet oluşturmak için kullanılan bir yaklaşımdır.

![API Gateway Pattern](./../kaynaklar/apigateway-pattern.png)
