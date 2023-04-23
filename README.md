# Muhammad Mufid Utomo - DevOps - Technical Test Jobhun Internship 2023

## Soal

a. Buatlah Script Github Actions untuk Deploy GitHub Repo ke SSH Instance!
b. Buatlah Kubernetes YAML File untuk Deploy App disertai penjelasannya!

## Solusi

Saya mengerjakan kedua soal secara sekaligus karena saya merasa kedua soal tersebut bisa dikerjakan secara bersamaan dan saya juga dapat mengaplikasikan pengetahuan saya dalam membuat Kubernetes cluster dan mengimplementasikan praktik continuous deployment dengan GitHub Actions.

Konfigurasi untuk Kubernetes cluster di kubernetes.yaml telah dites di [ValidKube](https://validkube.com/) dan berhasil tidak mengeluarkan error. Namun, karena saya tidak memiliki akses ke instance SSH, saya tidak dapat mengetes apakah aplikasi Wordpress yang saya deploy ke Kubernetes cluster berhasil berjalan.

### GitHub Actions

Saya membuat file deploy.yaml yang berada di .github/workflows sebagai konfigurasi untuk workflow Github Actions yang akan dijalankan ketika kita melakukan push ke branch `main`. Workflow ini akan menjalankan serangkaian perintah untuk mendeploy repo GitHub ini ke instance SSH, lalu mendeploy Kubernetes cluster yang berisi aplikasi Wordpress. Berikut 3 langkah yang dilakukan oleh workflow ini:

- Checkout code: Langkah ini akan mengambil kode dari repository ke runner Github Actions.

- Setup SSH: Langkah ini akan mengatur koneksi SSH ke instance target menggunakan action webfactory/ssh-agent. Secret SSH_PRIVATE_KEY digunakan untuk autentikasi koneksi SSH dan disimpan di GitHub menggunakan fitur [encrypted secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets).

- Deploy to Kubernetes: Langkah ini akan melakukan deploy aplikasi WordPress ke cluster Kubernetes menggunakan perintah kubectl apply dengan file konfigurasi kubernetes.yaml.

### Kubernetes

Saya menggunakan Wordpress sebagai contoh aplikasi yang akan dideploy ke Kubernetes. File kubernetes.yaml berisi konfigurasi untuk deployment dan service Wordpress. Berikut adalah penjelasan singkat mengenai konfigurasi Kubernetes yang saya gunakan:

1. Deployment Wordpress

    Deployment Wordpress akan menggunakan image `wordpress:latest` dan membuat 2 replika. Kemudian, di dalamnya terdapat beberapa environment variable yang digunakan untuk mengatur nama host, user, dan password database MySQL. Deployment ini juga akan membuat sebuah volume yang akan di-mount ke container MySQL sebagai persistent storage, dan menggunakan port 80 sebagai port yang akan di expose ke service Wordpress.

2. Service Wordpress

    Service Wordpress ini mengekspos deployment WordPress di dalam cluster Kubernetes lewat port 80.
