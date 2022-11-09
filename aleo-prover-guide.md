## 1. Клонуємо проект:
```
git clone https://github.com/AleoHQ/snarkOS.git --depth 1
```

## 2. Збираємо бінарники:
```
cd snarkOS
./build_ubuntu.sh
cargo install --path .
```

## 3. Створюємо гаманець, ЗБЕРІГАЄМО ОБОВЯЗКОВО.
```
snarkos account new
```

## 4. Створюємо сервіс для запуску прувера:
```
nano /etc/systemd/system/aleod-prover.service
```

В файл прописуємо свій APrivateKey
```
[Unit]
Description=Aleo Prover1 Testnet3
After=network-online.target
[Service]
User=root
ExecStart=/root/.cargo/bin/snarkos start --nodisplay --prover APrivateKey1000000000000000000000000000000000000000000000000
Restart=always
RestartSec=10
LimitNOFILE=10000
[Install]
WantedBy=multi-user.target
```

## 5. Запускаємо сервіс
```
systemctl enable aleod-prover
systemctl start aleod-prover
```
### Додаткові команди:
 - перевірка логів
```
journalctl -u aleod-prover -а
```
- зупинка сервіса
```
systemctl stop aleod-prover
```
 - перезапустити
 ```
 systemctl restart aleod-prover
 ```
 ## Видалення:
 ```
 systemctl disable --now aleod-prover
 rm -rf ~/snarkOS
 ```
