# how to deploy application
helm upgrade --install svc-user . --values values-testing.yaml --debug

# Taints:
## Fungsi: 
Mencegah pod dari dijadwalkan pada node tertentu, kecuali jika pod tersebut memiliki toleration yang sesuai. Ini digunakan untuk mengontrol penempatan pod dan mencegah pod yang tidak diinginkan dari ditempatkan pada node tertentu.
## Cara Kerja: 
Taints diterapkan pada node. Ketika sebuah node memiliki taint, hanya pod yang memiliki toleration yang cocok yang dapat dijadwalkan pada node tersebut.

# Tolerations:
## Fungsi: 
Memungkinkan pod untuk dijadwalkan pada node yang memiliki taint. Tolerations "menoleransi" taint pada node sehingga pod tersebut tidak akan terhindar dari node yang ditaint.
## Cara Kerja: 
Tolerations diterapkan pada pod. Pod dengan toleration yang sesuai dapat dijadwalkan pada node yang memiliki taint tertentu.

# how to deploy ingress nginx controller
## add repo
1. helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
## install nginx (by default service type loadbalancer layer 4 )
2. helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx
## optional use nodeport / clusterip
2. helm show values ingress-nginx/ingress-nginx > values-nginx.yml
## change service type to nodeport / clusterip
3. helm upgrade --install ingress-nginx ingress-nginx/ingress-nginx -f values-nginx.yml -n ingress-nginx --debug

# how to use gcp ingress
## create a rule format similar to nginx but the classname used is gce or gce-internal

# nginx ingress vs gcp ingress
## performance
- gunakan Nginx Ingress jika Anda memprioritaskan latency yang lebih kecil, throughput yang lebih tinggi, dan penanganan traffic bervolume tinggi dengan pemrosesan minimal.
- gunakan GCP ingress jika memerlukan routing path yang lebih advanced, SSL termination, global load balancing, and application-layer features. tetapi akan mengorbankan latency & throughput.
## Doc and community
### nginx ingress
nginx ingress memiliki komunitas yang sangat besar. Dokumentasi dan tutorial Nginx Ingress sangat lengkap dan tersebar luas di berbagai blog dan situs web.
### gcp ingress
gcp ingress memiliki komunitas yang banyak, tetapi tidak sebanyak Nginx. Dokumentasi GCP Ingress terstruktur dengan baik namun lebih terpusat pada platform GCP. Jumlah tutorial di blog-web tentang GCP Ingress lebih sedikit dibandingkan Nginx.
## Penggunaan
- nginx ingress dapat digunakan di mana saja, seperti di cloud, on-premises, atau laptop. Fitur-fitur di Nginx Ingress sangat banyak, jadi kita perlu menyesuaikan penggunaan fitur atau anotasi sesuai kebutuhan.
- gcp ingress hanya bisa digunakan di Google Cloud. Di luar itu, GCP Ingress tidak bisa digunakan. Fitur dan anotasi yang tersedia cukup banyak dan dapat dimanfaatkan sesuai kebutuhan di lingkungan Google Cloud.