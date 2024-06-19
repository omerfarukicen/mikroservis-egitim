---
layout: default
title : Components
parent: Genel Mimari
nav_order: 2
has_children: true
---

  

# Control Plane

  

## API Server

Kubernetes cluster mekanizmasının ortasında yer almaktadır. Master sunucumuza gelen tüm REST request'lerin yönetilmesi bu araç üzerinden gerçekleştirilir. Tüm istekler bu servis tarafından kabul edilir ve doğrulanır, ayrıca etcd veritabanına yapılan tek bağlantı bu ajanla yapılır. Sonuç olarak cluster içerisindeki ana işlem yeridir diyebiliriz. API hizmeti verir. Gelen istekler doğrular. Kimlik doğrulama, yetkilendirme ve erişim denetimi yapar.

  

## ETCD

  

Kubernetes üzerinde gerçekleştirilen bütün konfigürasyon ve durumların tutulduğu yüksek hızlı (10000 istek/sn) high-available mod'da çalışabilen, dağıtık, tutarlı bir key-value store’dur.Raft algoritmasıyla lider seçimi yapar.Veriler bellekte durur, istenildiği zamanlar diske kalıcı olarak yazılabilir.HTTP protokolü kullanır.

Tuttuğu değerler için zaman aşımları tanımlanabilmesine izin verir.Kendi ayarlarına /config şeklinde HTTP protokolüyle erişilebilir.Değerler değişmez (immutable) olarak tutulur. Varolan bir değerin değiştirilmesi istenirse eski değeri sürümleyerek korur ve yeni değer oluşturur. Eski verileri silmek, sıkıştırma (compact) işlemiyle yapılır yoksa verilerin tüm sürümleri hep kalır.

  
  
  

>  **Dikkat edilmedi Gerekenler:**
>  Etcd tek sayı üyelerden oluşan bir küme olarak çalıştırılır.Etcd'ye yeterli kaynak verilmesi gerekir. Çok fazla cpu'ya ihtiyaç duymaz, canlı sistemlerde 8GB bellek ve ortalama bir disk genel ihtiyaçlarını karşılar.
Etcd kümelerini kararlı tutmak, Kubernetes kümelerinin kararlılığı için kritik öneme sahiptir. Bu nedenle, garantili kaynak gereksinimleri için özel makinelerde veya yalıtılmış ortamlarda etcd kümelerini çalıştırın.

  
  

## Controller Manager

Controller uygulamalarını çalıştıran parçadır. Controller kavramı ilgili bölümde ayrıca açıklanacaktır.


Bazı controller tipleri:

 -  **Node controller:** Node'ların hata yaşama durumlarını fark etmekten ve karşılık vermekten sorumludur.
 -  **Job controller:** Job objelerinin çalıştırılmasından ve tamamlanmasından sorumludur.
 -  **Endpoints controller:** Endpoint objelerinin Service & Pod objeleri ile ilişkilendirilmesinden sorumludur.
 -  **Service Account & Token controllers:** Yeni oluşturulan namespace'ler için varsayılan service account ve API erişim token'larını oluşturur.

## Scheduler
Scheduler, deploy ettiğimiz uygulamaların hangi node(lar) üzerinde çalıştırılması gerektiğini hesaplayıp karar veren parçadır. Bu hesaplamayı, uygulamamızın ram ve cpu gibi kaynak gereksinimlerini ve cluster'ımızda bulunan worker node makinelerinin kullanılabilir ram/cpu değerlerini göz önüne alarak yapar.

Aynı zamanda uygulamalarımızı çeşitli kurallara göre (nodeSelector, affinity/anti-affinity, taint/toleration) farklı node'lar üzerinde çalışmasını isteyebiliriz. Scheduler bu kurallara uyan node'ların seçilmesini sağlar.

# Worker Node Plane
## Kubelet
Kubernetes kümesinin her düğümünde (node) çalışan bir ajan olarak görev yapar. Kubelet, her düğümde çalışan Pod'ları yönetir. API sunucusundan aldığı Pod tanımlarını (manifest) okuyarak bu Pod'ların belirtilen şekilde çalışmasını sağlar. Kubelet, her düğümdeki Pod'ların ve düğümün kendisinin durumunu sürekli olarak Kubernetes API sunucusuna rapor eder. Kubelet, düğümdeki kaynakların (CPU, bellek, disk vs.) izlenmesini ve yönetilmesini sağlar.

## Kube-Proxy
Service ve Endpoint objelerinin erişebilirliğini sağlamak için node üzerindeki network kurallarını ayarlar ve connection forwarding işlemini gerçekleştirir. Görevlerinden biride Kubernetes Service’lere ve Pod'lara virtual IP atamasıdır. Kube-proxy aynı zamanda bir servisin altındaki tüm pod’lara load-balance özelliği kazandırır.
Kube-proxy, iptables veya IPVS (IP Virtual Server) gibi sistem araçlarını kullanarak ağ trafiğini yönlendirmek için kurallar oluşturur ve yönetir. Bu kurallar, ağ paketlerinin doğru hedeflere ulaşmasını sağlar.

Kube-proxy kabul görmüş şekilde 2 modda çalışır:

**iptables:**
 Linux işletim sistemlerinde kullanılan bir paket filtreleme ve NAT (Ağ Adresi Çevirme) yönetim aracıdır. Linux çekirdeği içindeki Netfilter modülü ile birlikte çalışır ve ağ trafiğini kontrol etmek, filtrelemek ve yönlendirmek için kullanılır.Küme büyüdükçe yükü artar.

**IPVS:**
 Ağ trafiğini yönlendirme ve yük dengeleme işlevlerini gerçekleştirmek için Linux kernel seviyesinde çalışan güçlü bir araçtır.Yük dengeleme için bazı algoritmalar kullanır.

* Round-Robin: Gelen trafiği sırayla backend sunucularına yönlendirir.
* Least Connections: En az bağlantısı olan backend sunucuya trafiği yönlendirir.
* Least Load: En az yük altında olan backend sunucuya trafiği yönlendirir.
* Shortest Expected Delay: Beklenen en kısa gecikmeye sahip backend sunucuya trafiği yönlendirir.

```
kube-proxy --proxy-mode=ipvs

```


