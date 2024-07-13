---
layout: default
title: Network
nav_order: 1
has_children: true
---
# Kubernete Ağ İletişimi
Kubernetes'teki ağ yapısının arkasındaki kavramlar ve kaynaklar. 

Aşağıdaki gereksinimlerle çalışır:

* Bir noddaki podlar, NAT olmadan tüm nodlarlardaki tüm bölmelerle iletişim kurabilir.
* bir noddaki kubernetes araçları (ör. sistem arka plan programları, kubelet) o noddaki tüm bölmelerle iletişim kurabilir.
* Bir düğümün ana bilgisayar ağındaki bölmeler, NAT olmadan tüm düğümlerdeki tüm bölmelerle iletişim kurabilir.


Kubernetes ağ iletişimi dört kritere göre gerçekleşir:

* Pod'daki konteynerler, loopback adresi üzerinden iletişim kurarlar.
* Küme ağı farklı Pod'lar arasında iletişim sağlamaya yarar.
* Service nesnesi, Podlarda çalışan uygulamaların kümenizin dışından erişilebilmesini sağlar.
* Service nesnesini, yalnızca kümenizdeki içinde yayımlamak amacıyla da kullanabilirsiniz.

Kubernetes pod'ların birbirleri ile iletişimini CNI (Container Network Interface) üzerinden çözümler. CNI, container'lar üzerindeki network interface'leri ayarlamak için gerekli olan spesifikasyonları ve kütüphaneleri sunan bir projedir. Buradaki amaç container networking gibi kompleks bir konuda çıkacak ürünler arasında standardı sağlamaktır.Implement edilecek CNI standartları dışında CNI plugin’ler Metod ve yaklaşım itibariyle farklılık gösterir. Popüler olarak kullanılan CNI plugin'ler aşağıda listelenmiştir.
Burada en önemli konu Kubernetes CNI plugin ile Pod’a tekil bir clusterIP atamasıdır. Her pod cluster içerisinden varsayılan olarak erişebilir şekilde ayağa kalkmaktadır. Bu konuya ek olarak kube-proxy sayesinde Service objesi kullanılarak servislerin dışarıdan veya içeriden erişilebilir durumda olması sağlanır. Nodlar arasındaki trafiğin yönlendirilmesini en altta iptables yönetir.


[IPtables](../../kaynaklar/cni-iptables)


Kubernetes Ağ Modeli:
**Her Pod'un Kendi IP Adresi vardır:**Kubernetes, her Pod'a benzersiz bir IP adresi atar.
**Pod'lar Arası İletişim:**Pod'lar, aynı küme içindeki diğer Pod'lara doğrudan IP adresleri ile erişebilir.
**Services:**Pod'ların bir grup olarak erişilmesini sağlar ve yük dengeleme (load balancing) gibi işlevleri sunar.
**ClusterIP:**Hizmetler varsayılan olarak bir ClusterIP türünde oluşturulur.ClusterIP,sadece küme içindeki diğer Pod'ların erişebileceği sanal bir IP adresi sağlar.
**NodePort ve LoadBalancer:**NodePort, bir hizmeti Node'un bir portu üzerinden erişilebilir hale getirir.LoadBalancer,  yük dengeleyicilerini kullanarak hizmeti dış dünyaya açar.

## Kubernetes Ağ Çözümleri (CNI Plugins)
Popüler CNI eklentileri şunlardır:
**Flannel:** Basit ve yaygın olarak kullanılan bir ağ çözümüdür.
**Calico:**Gelişmiş ağ politikaları ve güvenlik özellikleri sunar.Network Policies kullanarak trafiği kontrol edebilir.
**Weave:**Kullanımı kolay ve hızlı bir ağ çözümüdür.Otomatik keşif ve şifreleme gibi özellikler sunar.
**Cilium:**BPF (Berkeley Packet Filter) kullanarak gelişmiş ağ politikaları ve gözlemlenebilirlik sağlar.Mikro hizmet güvenliği ve ağ performansı için idealdir.