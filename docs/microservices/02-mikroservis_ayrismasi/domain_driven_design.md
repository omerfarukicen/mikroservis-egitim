---
layout: default
title:  Domain Driven Design
parent: Mikroservis Ayrışması
nav_order: 1
---

# Domain Driven Design(İş alanı alt alanlara göre ayrıştırma (Decompose by subdomain):

 Domain Driven Design (DDD), bir yazılım projesinin karmaşık iş kurallarının ve problem alanlarının analizi ve modellemesi için bir yaklaşımdır. Bu yaklaşım, karmaşık iş süreçlerini ve bağlamlarını daha kolay anlamak için iş alanlarını (domain) öne çıkarır.Sonuç olarak, DDD, yazılım sistemlerinin karmaşık iş süreçlerine daha iyi uyum sağlamasına, müşteri ihtiyaçlarını karşılamasına ve daha modüler ve esnek hale gelmesine yardımcı olan bir yazılım tasarım yaklaşımıdır.

DDD, temelde iki çeşide ayrılır:

1. Strategic DDD: İş alanı tasarımının genel stratejisini belirleyen ve bir organizasyondaki tüm sınırlı bağlamlar arasındaki ilişkileri ele alan bir yaklaşımdır. Bu yaklaşım, sınırlı bağlamların belirlenmesi, iş alanı modellerinin ve kurallarının tanımlanması, bağlamsal arayüzlerin tasarlanması ve iş alanı servislerinin oluşturulması gibi konuları ele alır.

2. Tactical DDD: Belirli bir sınırlı bağlam içindeki nesne modellerinin ve sınıfların nasıl organize edileceğini ve bu modellerin birbiriyle nasıl etkileşeceğini tasarlamak için kullanılan bir yaklaşımdır. Taktik tasarım, bir iş alanındaki öğelerin (entity, value object, aggregate, repository vb.) nasıl düzenleneceğini, birbirleriyle nasıl etkileşimde bulunacaklarını ve hangi kurallara uyacaklarını belirlemekle ilgilidir.

## 1. Strategic DDD

**Domain Expert :**  İşin uzmanı ve yazılımın geliştirilmesi için gerekli tüm teorik bilgilere sahiptir.

**Ubiquitous Language :** Domain expert arasındaki ortak iletişimi sağlamakta, sağlanması gerektiğini ifade etmektedir. Domain expert’ler, alanlarına dair her ne kadar derin ve yeterli bilgiye sahip olsalar da yazılım geliştirme hakkında hiçbir şey bilmiyor olabilirler. Aynı şey yukarıda gördüğümüz gibi bir yazılım geliştirici için de geçerli olabilir ve çalışılacak alana dair herhangi bir bilgi söz konusu olmayabilir. İşte böyle bir durumda DDD yazılım geliştiricisi ile domain expert’ler arasında her iki tarafında rahat anlaşabilmesi için ortak dil bulunmasını önermektedir. Ubiquitous language’in önerdiği ortak dilin geliştirilmesi ister istemez domain model’e yansıyacaktır. Çünkü domain model, yapılacak işin omurgasıdır. Haliyle otomatik olarak bu ortak dil koda yansımış olacaktır. Zaten ortak dil kullanmanın en büyük avantajı bu dilin tekrarlı kullanımında dilin zayıf yönlerini belirlememizi sağlamasıdır. Bu durumda domain model hızlı bir şekilde düzeltme yapabilmemizi sağlayacak ve böylece ortak dilde bir şey değişirse bu domain model aracılığıyla doğrudan kod üzerinde de değişikliğe sebebiyet vermiş olacaktır.

**Bounded Context :** Bounded Context, birbirlerinden ayrılmış ve sınırları belirlenmiş yapılanmalardır. Esasında bu içeriğimizin başlangıç paragrafında belirtilen alt kırılımlardaki her bir ana kırılım bir Bounded Context’e karşılık gelmektedir. Bounded Context’leri mikro servis mimarilerdeki her bir servise karşılık gelen projeler/microservis olarak da düşenebilirsiniz.

**Context Mapping**:
Bounded context’lerin kendi aralarındaki iletişim mimarisine dayalı birbirleriyle olan kesişim noktalarını izah edebilmeye context mapping denmektedir. Yani bir başka deyişle context mapping, bounded context’ler ile bunlardan sorumlu ekipler arasındaki ilişkiyi belirlemenize olanak sağlayan araçtır. Buna bir örnek vermemiz gerekirse eğer; siparişler tablosunda(bounded context) müşteri numarasının olması amma velakin müşteri tablosunda(bounded context) siparişe dair herhangi birşeyin olmaması yani bu sınırların ayarlanması bir Context Mapping’dir.

## 2. Tactical DDD

**Entity:** Bir varlığı temsil eden bir nesne, örneğin bir müşteri veya bir sipariş.

**Value Object:** Değer nesneleri, bir kimlik veya özellik kümesi ile tanımlanabilen, ancak kendilerinin bir benzersiz kimliği olmayan nesnelerdir. Örneğin, bir tarih aralığı veya bir para birimi değeri.

**Aggregate:** Bir dizi ilişkili varlığı birleştiren bir grup. Aggregate, bir işlem sırasında birbirleriyle bütünleşik olarak değiştirilebilir.

**Repository:** Varlıkların ve agregatların kalıcı saklama yerlerini temsil eden bir arayüz.

**Service:** Bir işlevi gerçekleştiren bir iş mantığı parçasıdır. Örneğin, bir ödeme işlemi gerçekleştirmek veya bir envanter güncellemesi yapmak için bir hizmet kullanılabilir.

**Factory:** Nesneleri yaratmak için kullanılan bir yöntemdir. Örneğin, bir müşteri nesnesi oluşturmak için bir müşteri fabrikası kullanılabilir.

**Domain Event:** Bir uygulamada gerçekleşen bir olayı temsil eden bir nesnedir. Örneğin, bir siparişin tamamlandığı bir olaya sahip olmak mümkündür.

![Monolitik Uygulama](../kaynaklar/tacticaldesign.png)

 **Eric Evans’a göre domain model:**
Domain Model, belirli bir diyagram değildir! Diyagramın iletmeyi amaçladığı fikirdir. Ve bu sadece alan uzmanının kafasındaki bilgi değil, bu bilginin titiz bir şekilde organize edilmiş bir soyutlamasıdır.
