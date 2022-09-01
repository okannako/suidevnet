![1_IRwa2GrRrF3HaCsR-h3yIQ](https://user-images.githubusercontent.com/73176377/179422942-beb8be43-66c0-4412-af3e-07a3aa0ddea7.png)

## Sistem Gereksinimleri
 - Memory: 8 GB RAM
 - CPU: 2
 - Disk: 50 GB 
 - OS: Ubuntu 20.04
 
## Açıklamalar
 - Eğer yükleme işlemini Digital Oceon, Linode gibi sağlayıcılar üzerinde değil Google Cloud, Azure, Aws gibi sağlayıcılar üzerinde yapıyorsanız aşağıdaki port açma bölümünü yapmanız gerekiyor. Eğer kodlarla olmazsa kendi yönetim sayfalarından elle açmanız gerekli.
## Port Açmak
```
sudo ufw allow 8080
sudo ufw allow 9000
sudo ufw allow 9184
```
## Node Yükleme
```
apt install tmux
tmux
wget -O sui.sh https://api.nodes.guru/sui.sh && chmod +x sui.sh && ./sui.sh
```
- Tmux ekranını arka plana atmak için `ctrl+b d` basıyoruz. Tekrar girmek için önce `tmux ls` yazıyoruz ve ekranın ismini görüyoruz. Daha sonra `tmux attach -t isim` yazıp ilgili tmux ekranına girmiş oluyoruz. 

## Node İle İlgili Kodlar
### Kontrol
```
curl -s -X POST http://127.0.0.1:9000 -H 'Content-Type: application/json' -d '{ "jsonrpc":"2.0", "method":"rpc.discover","id":1}' | jq .result.info
```

### Versiyon Kontrolü (27 Temmuz güncellemesinden sonra)
- Şu kodu `grep 'version =' /root/sui/crates/sui/Cargo.toml` girdiğinizde aşağıdaki gibi bir sonuç vermeli.
```
version = "0.8.0"
```
### Log Kontrolü
```
journalctl -u suid -f -o cat
```
### Node Restart
```
sudo systemctl restart suid
```
### Node Durdurmak
```
sudo systemctl stop suid
```
### Node Silmek
```
sudo systemctl stop suid
sudo systemctl disable suid
rm -rf ~/sui /var/sui/
rm /etc/systemd/system/suid.service
```
### Site Üzerinden Node Durumu
 - https://node.sui.zvalid.com/
## Kurulum Rehber Videosu ve Discord Linki
 - https://youtu.be/7aLtCeD78kg
 - https://discord.gg/TRVphefMdh
