# Установка IVA Connect Desktop на Ubuntu (из .rpm-пакета)

Инструкция по установке приложения **IVA Connect Desktop** на Ubuntu на основе RPM-пакета (например, `ivcs_messenger_desktop-21.4.5348.altlinux.rpm`) с добавлением ярлыка в меню.

---

## 📦 1. Установка необходимых пакетов

```bash
sudo apt update
sudo apt install alien gdebi-core
````

---

## 🔄 2. Конвертация RPM в DEB

Перейдите в папку загрузки:

```bash
cd ~/Загрузки
```

Преобразуйте `.rpm` в `.deb`:

```bash
sudo alien --to-deb ivcs_messenger_desktop-21.4.5348.altlinux.rpm
```

В результате получится файл, например:

```
ivaconnect_21.4-5349_amd64.deb
```

---

## 💾 3. Установка .deb-файла

```bash
sudo dpkg -i ivaconnect_21.4-5349_amd64.deb
sudo apt --fix-broken install
```

---

## 🚀 4. Запуск вручную (если не создаётся ярлык)

Запуск приложения:

```bash
/opt/IVKS/ivaconnect/ivaconnect
```

Если при запуске появляется **"Аварийный останов"**, используйте переменные окружения:

```bash
QT_QPA_PLATFORM_PLUGIN_PATH=/opt/IVKS/ivaconnect/plugins/platforms \
LD_LIBRARY_PATH=/opt/IVKS/ivaconnect \
/opt/IVKS/ivaconnect/ivaconnect
```

---

## 📋 5. Добавление ярлыка в меню

Создайте файл ярлыка:

```bash
nano ~/.local/share/applications/ivaconnect.desktop
```

Вставьте следующее содержимое:

```ini
[Desktop Entry]
Name=IVA Connect
Exec=env QT_QPA_PLATFORM_PLUGIN_PATH=/opt/IVKS/ivaconnect/plugins/platforms LD_LIBRARY_PATH=/opt/IVKS/ivaconnect /opt/IVKS/ivaconnect/ivaconnect
Icon=/opt/IVKS/ivaconnect/usr/share/pixmaps/ivaconnect.png
Type=Application
Categories=Network;VideoConference;
StartupNotify=true
Terminal=false
```

Сохраните файл (`Ctrl+O`, затем `Ctrl+X`), затем сделайте его исполняемым:

```bash
chmod +x ~/.local/share/applications/ivaconnect.desktop
update-desktop-database ~/.local/share/applications/
```

---

## ✅ 6. Проверка

Откройте меню приложений — появится пункт **IVA Connect** с фирменной иконкой. При запуске всё должно работать корректно.
