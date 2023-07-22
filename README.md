**Table of Contents**

- [Persiapan](#persiapan)
- [Cara Mengisi Akun](#cara-mengisi-akun)
  - [1 Modem](#single-modem)
  - [2 Modem](#multi-modem)

# Persiapan
1. Aktifkan meta core
<img src="Screenshot 2023-05-12 203415.png"/></br>
2. Upload semua file di folder `proxy_provider` ke `Openclash >> config_editor >> proxy_provider`
3. Upload semua file di folder `rule_provider` ke `Openclash >> config_editor >> rule_provider`
4. Masuk ke `Config Manage`. upload config file `configAkrab.yaml` kemudian aktifkan
5. Pada menu `Config Manage` scroll kebawah cari `proxy group`, sesuaikan `interface name` dengan interface modem kalian
<img src="Screenshot 2023-05-12 203416.png"/></br>
6. Commit & Apply

# Cara Mengisi Akun
### Single Modem
1. Edit file `config editor >>> proxy-provider >>> AKUN.yaml`
2. Anda bisa menambahkan beberapa akun sekaligus, contoh format ada di `contoh format.yaml`
```yaml
proxies:
- name: VPN-1
  type: trojan
  server: SERVER.COM
  port: 443
  password: PASSWORD
  udp: true
  sni: BUGSNI.COM
  alpn:
  - http/1.1
  skip-cert-verify: true
  network: ws
  ws-opts:
    path: /trojan-ws
    headers:
      Host: BUGSNI.COM

- name: VPN-2
  server: SERVER.COM
  port: 443
  type: trojan
  password: PASSWORD
  network: ws
  sni: BUGSNI.COM
  skip-cert-verify: true
  udp: true
  ws-opts:
    path: /path
  headers:
    Host: BUGSNI.COM
```
### Multi Modem
1. Edit file `config editor >>> proxy-provider >>> VPN1.yaml & VPN2.yaml`, VPN1 untuk interface modem1 VPN2 untuk interface modem2
2. Untuk format akun sama seperti 1 modem tapi perlu ditambah `interface name`, sesuaikan dengan interface modem
3. Contoh pengisian akun
```yaml
#File VPN1.yaml
proxies:
- name: biznet
  type: trojan
  server: SERVER.COM
  port: 443
  password: PASSWORD
  udp: true
  sni: BUGSNI.COM
  alpn:
  - http/1.1
  skip-cert-verify: true
  network: ws
  ws-opts:
    path: /trojan-ws
    headers:
      Host: BUGSNI.COM
  interface-name: eth1 (sesuaikan dengan modem)
```
```yaml
#File VPN2.yaml
proxies:
- name: biznet
  type: trojan
  server: SERVER.COM
  port: 443
  password: PASSWORD
  udp: true
  sni: BUGSNI.COM
  alpn:
  - http/1.1
  skip-cert-verify: true
  network: ws
  ws-opts:
    path: /trojan-ws
    headers:
      Host: BUGSNI.COM
  interface-name: eth2 (sesuaikan dengan modem)
```
