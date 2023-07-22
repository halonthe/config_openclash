**Table of Contents**

- [Persiapan](#persiapan)
- [Cara Mengisi Akun](#cara-mengisi-akun)
  - [1 Modem](#single-modem)
  - [2 Modem](#multi-modem)
- [Kumpulan Format Akun OpenClash](#kumpulan-format-akun-openclash)
  - [Shadowsocks](#shadowsocks)
  - [Vmess](#vmess)
  - [Snell](#snell)
  - [Trojan](#trojan)

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

# Kumpulan Format Akun OpenClash
#### Shadowsocks

* Shadowsocks Original / tanpa plugin
```yaml
- name: "shadowsocks"
  type: ss
  server: aaa.bbb.ccc.ddd
  port: 34963
  cipher: chacha20-ietf-poly1305
  password: passwordss
  udp: true
  interface-name: eth1
```
* Shadowsocks dengan plugin obfs
```yaml
- name: "shadowsocks obfs"
  type: ss
  server: aaa.bbb.ccc.ddd
  port: 32033
  cipher: chacha20-ietf-poly1305
  password: passwordss
  plugin: obfs
  plugin-opts:
    mode: tls
    host: BUG.COM
  interface-name: eth1
```

#### Vmess

* Vmess websocket dengan BUG SNI
```yaml
- name: "Vmess ws bug SNI"
  type: vmess
  server: domainserver.com
  port: 443
  uuid: UUIDMU
  alterId: 0
  cipher: auto
  udp: true
  tls: true
  skip-cert-verify: true
  servername: BUGSNI.COM
  network: ws
  ws-opts:
    path: /iptunnelscom
    headers:
      Host: BUGSNI.COM
    max-early-data: 2048
    early-data-header-name: Sec-WebSocket-Protocol
  interface-name: eth1
```
* Vmess websocket dengan BUG CDN (bolak-balik)
```yaml
- name: "vmess ws bug CDN"
  type: vmess
  server: IP/HOST_CDN_CLOUDFLARE
  port: 443
  uuid: UUIDMU
  alterId: 0
  cipher: auto
  udp: true
  tls: true
  skip-cert-verify: false
  servername: domainservermu.com
  network: ws
  ws-opts:
    path: /iptunnelscom
    headers:
      Host: domainservermu.com
    max-early-data: 2048
    early-data-header-name: Sec-WebSocket-Protocol
  interface-name: eth1
```
* Vmess gRPC bug SNI
```yaml
- name: vmess grpc SNI
  server: domainservermu.com
  port: 443
  type: vmess
  uuid: UUIDMU
  alterId: 0
  cipher: auto
  network: grpc
  tls: true
  servername: BUGSNI.COM
  skip-cert-verify: true
  grpc-opts:
    grpc-service-name: iptunnelsvgrpc
  interface-name: eth1
```
* Vmess gRPC bug CDN
```yaml
- name: vmess grpc CDN
  server: IP/HOST_CDN_CLOUDFLARE
  port: 443
  type: vmess
  uuid: UUIDMU
  alterId: 0
  cipher: auto
  network: grpc
  tls: true
  servername: domainservermu.com
  skip-cert-verify: false
  grpc-opts:
    grpc-service-name: iptunnelsvgrpc
  interface-name: eth1
```

#### Snell

* Snell Server v3 (support udp).
```yaml
- name: "snell server"
  type: snell
  server: aaa.bbb.ccc.ddd
  port: 33223
  psk: password
  version: 3
  udp: true
  obfs-opts:
    mode: tls
    host: BUGSNI.COM
  interface-name: eth1
```

#### Trojan

* Trojan-gfw bug SNI
```yaml
- name: "trojan-gfw SNI"
  type: trojan
  server: domainservermu.com
  port: 443
  password: PASSWORD
  udp: true
  sni: BUGSNI.COM
  alpn:
    - h2
    - http/1.1
  skip-cert-verify: true
  interface-name: eth1
```
* Trojan-go websocket bug CDN
```yaml
- name: trojan ws cdn
  server: IP/HOST_CDN_CLOUDFLARE
  port: 443
  type: trojan
  password: PASSWORD
  network: ws
  sni: domainservermu.com
  skip-cert-verify: false
  udp: true
  ws-opts:
    path: /iptunnelstrgo
    headers:
        Host: domainservermu.com
  interface-name: eth1
```
* Trojan gRPC bug SNI
```yaml
- name: "trojan gRPC SNI"
  type: trojan
  server: domainservermu.com
  port: 443
  password: PASSWORD
  udp: true
  sni: BUGSNI.COM
  alpn:
  - h2
  skip-cert-verify: true
  network: grpc
  grpc-opts:
    grpc-service-name: iptunnelstrojangrpc
  interface-name: eth1
```
* Trojan gRPC bug CDN
```yaml
- name: "trojan gRPC CDN"
  type: trojan
  server: IP/HOST_CDN_CLOUDFLARE
  port: 443
  password: PASSWORD
  udp: true
  sni: domainservermu.com
  alpn:
  - h2
  skip-cert-verify: false
  network: grpc
  grpc-opts:
    grpc-service-name: iptunnelstrojangrpc
  interface-name: eth1
```
