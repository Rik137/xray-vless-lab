# xray-vless-lab  

Этот проект предназначен для людей которым нужна помощь в преодалении цензурного зановеса. 
Здесь представлена подробная инструкция как пользоваться эко-системой xray которая помжет быть 
всегда на связи даже в условиях обсолютного железног зановися.
---
что нужно?
1. снять в оренду самый дешевй VPS сервер в стране где нет проблем с блокироваками
2. поднчть на нем движок xray

```bash
sudo apt update
sudo apt install xray
```
3. запустить xray и добавть его в автозагрузку
   
 ```bash
sudo systemctl start xray
sudo systemctl enable xray
```
4. проверить запуск xray
```bash
sudo systemctl status xray
```
5. положить уже готовай config file c именем config_client.json по пути

```bash
/usr/local/etc/xray/config.json
```
6. сгенрировать ключи доступа при помощи команды

```bash
xray 
