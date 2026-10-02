# Automated Workspace Deploy: Nextcloud + ONLYOFFICE

This Ansible playbook automates the full deployment cycle of a monolithic workspace environment (Nextcloud, ONLYOFFICE, Nginx, PostgreSQL, Redis) using Docker Compose.

The script dynamically requests all necessary parameters (passwords, domains, JWT secrets) at runtime, creates an in-memory inventory host, and executes the deployment.

## Key Features:
1. Installs Docker and Docker Compose on the target server.
2. Generates `docker-compose.yml` and Nginx configurations from templates.
3. Deploys containers and waits for their initialization.
4. Integrates ONLYOFFICE with Nextcloud (configures URLs, JWT tokens, and trusted domains via Tailscale).
5. Loads custom corporate fonts and rebuilds the ONLYOFFICE font cache.
6. Mass-generates users based on a specified index and assigns them to the appropriate document access group.

## Project Structure:
* `deploy.yml` — The main Ansible playbook.
* `templates/nginx.conf.j2` — Nginx reverse proxy configuration template.
* `templates/docker-compose.yml.j2` — Docker Compose template.
* `files/fonts/` — Directory for custom fonts (place your `.ttf` files here).

## Usage
To run the playbook from your local machine, execute the following command:

```bash
ansible-playbook -i "localhost," deploy.yml

# Automated Workspace Deploy: Nextcloud + ONLYOFFICE

Цей Ansible-плейбук автоматизує повний цикл розгортання монолітного робочого простору (Nextcloud, ONLYOFFICE, Nginx, PostgreSQL, Redis) за допомогою Docker Compose. 

Скрипт динамічно запитує всі необхідні параметри (паролі, домени, JWT) при запуску, створює хост у пам'яті та виконує деплой.

## Що робить цей скрипт:
1. Встановлює Docker та Docker Compose на цільовий сервер.
2. Створює структуру директорій (`/opt/workspace`) з правильними дозволами.
3. Генерує `docker-compose.yml` та конфіги `nginx` із шаблонів.
4. Запускає контейнери та чекає на їх ініціалізацію.
5. Інтегрує ONLYOFFICE в Nextcloud (прописує URL-адреси, JWT-токени, налаштовує довірені домени через Tailscale).
6. Завантажує кастомні корпоративні шрифти та ребілдить кеш ONLYOFFICE.
7. Масово генерує користувачів за заданим індексом та додає їх у групу доступу до документів.

## Структура проекту:
- `deploy.yml` — головний плейбук.
- `templates/nginx.conf.j2` — шаблон конфігурації Nginx.
- `templates/docker-compose.yml.j2` — шаблон Docker Compose.
- `files/fonts/` — директорія для кастомних шрифтів. Додавайте шрифти у форматі '.ttf'.

## Запуск

Для запуску скрипта на локальній машині виконайте команду:

bash
ansible-playbook -i "localhost," deploy.yml

Під час запуску скрипт попросить вас ввести:
- IP-адресу або домен цільового сервера
- Ім'я SSH-користувача та sudo-пароль
- Ваш Tailscale домен
- Паролі для БД, Redis та JWT-секрет для OnlyOffice
- Кількість користувачів для автоматичної генерації

