данная роль устанавливает zabbix-agent2 , прописывает сервер и запускет демона
роль имеет встроенные тесты на движке docker
чтобы прогнать тесты сперва выполните python пакет molecule:

pip install "molecule[docker]" ansible

так же убедитесть что установлен docker и что сследующая команда выполняется без ошибок 
```
docker run --rm hello-world
```

Начать выполнять тест роли:

```
molecule create     # создать docker контейнеры
molecule prepare    # выполнить подготовку (установка python и все что указано в ./molecule/default/prepare.yml  )
molecule converge   # применить роль
```

все это можно выполнить одной командой:
```molecule test```    , который выполнит по пути еще кучу всего, а именно:
```
- molecule destroy — 🧹 Удаляет старое тестовое окружение (контейнеры, инстансы и т.д.)
- molecule dependency — 📦 Устанавливает зависимости роли (например, через requirements.yml)
- molecule syntax — ✅ Проверяет синтаксис playbook'ов Ansible
- molecule create — 🏗️ Создаёт тестовое окружение (обычно контейнер с образом из platforms)
- molecule prepare — ⚙️ Запускает подготовительный playbook (prepare.yml), например, установка Python в контейнере
- molecule converge — 🚀 Применяет роль (выполняет converge.yml, как обычный playbook)
- molecule idempotence — 🔁 Повторно запускает роль и проверяет, что изменений не происходит (идемпотентность)
- molecule verify — 🔍 Выполняет проверки (verify.yml или тесты в testinfra/goss)
- molecule cleanup — 🧼 Удаляет временные файлы или артефакты после теста (опционально)
- molecule destroy — 💥 Удаляет тестовое окружение (например, контейнеры), чтобы оставить систему чистой
```
