# Gensyn-Node-Partipication-Rewards-Alamama-Sorununa-Bakış
# RG-Swarm Bağlantı Testi Rehberi

Bu rehber, `rg-swarm.yaml` dosyanızda listelenen **bootnode IP ve portlarının** çalışırlığını test etmenize yardımcı olur.  
Amaç, bulunduğunuz bölgenin çevrimiçi olduğunu ve swarm ağına katılmaya hazır olduğunu doğrulamaktır.

## 1. Bootnode Bilgilerini Görüntüleme

`rg-swarm.yaml` dosyanızı açmak için terminalde şu komutu kullanın:

```bash
nano rgym_exp/config/rg-swarm.yaml
```

Eğer `nano` yüklü değilse önce kurun:

```bash
apt install nano -y
```

Dosyada aşağıdaki gibi bir bölüm göreceksiniz.  
**Sadece IP adresleri ve portları alınmalıdır** — Peer ID’leri düzenlemeyin veya değiştirmeyin.

```
communications:
  initial_peers:
    - /ip4/38.101.215.12/tcp/30011/p2p/QmQ2gEXoPJg6iMBSUFWGzAabS2VhnzuS782Y637hGjfsRJ
    - /ip4/38.101.215.13/tcp/30012/p2p/QmWhiaLrx3HRZfgXc2i7KW5nMUNK7P9tRc71yFJdGEZKkC
    - /ip4/38.101.215.14/tcp/30013/p2p/QmQa1SCfYTxx7RvU7qJJRo79Zm1RAwPpkeLueDVJuBBmFp
```

Yani test edeceğiniz adresler:  
```
38.101.215.12:30011  
38.101.215.13:30012  
38.101.215.14:30013
```

## 2. Gerekli Araçları Kurma

Eğer sisteminizde `ping` veya `nc` (netcat) yüklü değilse şu komutları çalıştırın:

```bash
apt update
apt install -y iputils-ping netcat
```

## 3. Bağlantı Testleri

IP’leri test etmek için:

```bash
ping -c 4 38.101.215.12
ping -c 4 38.101.215.13
ping -c 4 38.101.215.14
```

Portları test etmek için:

```bash
nc -vz 38.101.215.12 30011
nc -vz 38.101.215.13 30012
nc -vz 38.101.215.14 30013
```

**Başarılı sonuç:**
```
Connection to <IP> <PORT> port [tcp/*] succeeded!
```

## 4. Örnek Sonuçlar

```
38.101.215.12:30011 → erişilebilir  
38.101.215.13:30012 → erişilebilir  
38.101.215.14:30013 → erişilebilir  
Tüm düğümler başarıyla yanıt verdi.
```

## 5. Sorun Giderme

- `ping` başarısızsa → bağlantınızı, VPN veya güvenlik duvarınızı kontrol edin.  
- `nc` zaman aşımına uğrarsa → bootnode bakımda olabilir.  
- Sadece bazı IP’ler başarısızsa → sorun bölgesel olabilir.
