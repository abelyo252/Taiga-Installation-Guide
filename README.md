# BriskDocu Taiga — Local Taiga Setup Ever

**One-command installation • Epic animated bench • Clean URLs**  
Built and perfected in November 2025 by the Brisk Backoffice team.

[![BriskDocu](https://img.shields.io/badge/BriskDocu-Powered-blue?style=for-the-badge)](https://briskdocu.example.com)
![Taiga](https://img.shields.io/badge/Taiga-Latest%20v6.9+-green)
![Docker](https://img.shields.io/badge/Docker-Ready-blue)

## Features

- Zero-config Docker Compose setup
- Full command suite (start, stop, backup, restore, sample-data, etc.)
- Switch between `http://localhost` and `http://localhost:9000` instantly
- Works perfectly on Ubuntu 22.04 / 24.04

---

## Quick Install (5 minutes)

```bash
# 1. Install Docker + Docker Compose
sudo apt update
sudo apt install -y docker.io docker-compose
sudo usermod -aG docker $USER
newgrp docker   # or logout/login

# Fix docker-compose command (works on all Ubuntu versions)
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version

# 2. Clone the official Taiga + BriskDocu magic
git clone https://github.com/taigaio/taiga-docker.git
cd taiga-docker

# 3. Create .env (open with gedit or nano)
gedit .env
```

Paste this into `.env` and save:

```env
# BriskDocu Taiga – Secure & Ready
SECRET_KEY=replace_this_with_output_below
POSTGRES_USER=taiga
POSTGRES_PASSWORD=[DBPASSWORD]

RABBITMQ_USER=taiga
RABBITMQ_PASS=replace_this_with_output_below
RABBITMQ_ERLANG_COOKIE=replace_this_with_output_below
RABBITMQ_VHOST=taiga

TAIGA_SCHEME=http
TAIGA_DOMAIN=localhost:9000
WEBSOCKETS_SCHEME=ws

SUBPATH=
EMAIL_BACKEND=console
ENABLE_TELEMETRY=False
PUBLIC_REGISTER_ENABLED=True
ATTACHMENTS_MAX_AGE=3600
```

Generate strong secrets:

```bash
echo "SECRET_KEY=$(openssl rand -hex 32)"
echo "RABBITMQ_PASS=$(openssl rand -hex 16)"
echo "RABBITMQ_ERLANG_COOKIE=$(openssl rand -hex 32)"
```

Copy the output and replace the placeholders in `.env`.

Start Taiga:

```bash
docker-compose up -d
```

Create your admin user:

```bash
docker-compose run --rm --entrypoint="" taiga-back python manage.py createsuperuser
```

Open Taiga: http://localhost:9000

---

## Install the Legendary BriskDocu Bench

```bash
gedit bench.sh
```

Paste the **full ultimate bench.sh** from below → save → make executable:

```bash
#!/bin/bash
# TAIGA BENCH ULTIMATE v5.0 – BriskDocu Edition
# November 2025 – The most beautiful Taiga bench ever created
set -e
cd "$(dirname "$0")"

RED='\033[0;31m'; GREEN='\033[0;32m'; YELLOW='\033[1;33m'; BLUE='\033[0;34m'; CYAN='\033[0;36m'; MAGENTA='\033[0;35m'; WHITE='\033[1;37m'; NC='\033[0m'

# Epic BriskDocu banner
# Epic BriskDocu banner
banner() {
    clear
    echo
    # --- BRISK --- (Using MAGENTA, BLUE, CYAN)
    echo -e "${MAGENTA}  ██████╗ ██████╗ ██╗███████╗██╗  ██╗██╗  ██╗ ${NC}" # The first block now spells BRISK across the columns
    echo -e "${MAGENTA}  ██╔══██╗██╔══██╗██║██╔════╝██║ ██╔╝██║ ██╔╝ ${NC}"
    echo -e "${BLUE}  ██████╔╝██████╔╝██║███████╗█████╔╝ █████╔╝   ${NC}"
    echo -e "${BLUE}  ██╔══██╗██╔══██╗██║╚════██║██╔═██╗ ██╔═██╗   ${NC}"
    echo -e "${CYAN}  ██████╔╝██║  ██║██║███████║██║  ██╗██║  ██╗ ${NC}"
    echo -e "${CYAN}  ╚═════╝ ╚═╝  ╚═╝╚═╝╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝ ╚═════╝${NC}"
    echo
    # --- DOCU --- (Using WHITE) - This block should now correctly spell DOCU
    echo -e "          ${WHITE}██████╗ ██████╗  ██████╗ ██╗   ██╗ ${NC}"
    echo -e "          ${WHITE}██╔══██╗██╔══██╗██╔═══   ██║   ██║ ${NC}"
    echo -e "          ${WHITE}██║  ██║██║  ██║██║      ██║   ██║ ${NC}"
    echo -e "          ${WHITE}██║  ██║██║  ██║██║      ██║   ██║ ${NC}"
    echo -e "          ${WHITE}██████╔╝██████╔╝╚██████╔ ╚██████╔╝ ${NC}"
    echo -e "          ${WHITE}╚═════╝ ╚═════╝  ╚═════╝  ╚═════╝  ${NC}"
    echo
    # --- BriskDocu Highlighted Section ---
    echo -e "          ${CYAN}╔══════════════════════════════════════════════════════════╗${NC}"
    echo -e "          ${CYAN}║${MAGENTA}                BriskDocu - The Future of Documentation         ${CYAN}║${NC}"
    echo -e "          ${CYAN}║        ${WHITE}TAIGA BENCH v1.0 - Powered by Brisk Backoffice team  ${CYAN}║${NC}"
    echo -e "          ${CYAN}╚══════════════════════════════════════════════════════════╝${NC}"
    echo
}


# Animated loading with your name
loading() {
    echo -e "${CYAN}BriskDocu Loading ...${NC}"
    sleep 1.5
    echo -e "${CYAN}Your Operation is ongoing ......${NC}"
    sleep 1.2
    echo -e "${CYAN}BriskDocu Loading .........${NC}"
    sleep 0.5
}

# Always show banner + animation first
banner
loading

# Quick background commands (silent)
(
    case "$1" in
        start|stop|restart|rebuild|update|switch-port-80|switch-port-9000) exit 0 ;;
        *) exit 0 ;;
    esac
) > /dev/null 2>&1 &
wait $! 2>/dev/null

clear
banner

# Main command execution
case "$1" in

    start)              docker-compose up -d && echo -e "${GREEN}Taiga STARTED → http://localhost:9000${NC}" ;;
    stop)               docker-compose down && echo -e "${RED}Taiga STOPPED${NC}" ;;
    restart)            docker-compose restart && echo -e "${GREEN}Restarted${NC}" ;;
    rebuild)            docker-compose up -d --force-recreate && echo -e "${GREEN}Rebuilt & started${NC}" ;;
    logs)               docker-compose logs -f ;;
    status)             docker-compose ps ;;

    update)
        echo -e "${YELLOW}Updating Taiga (BriskDocu Edition)...${NC}"
        git pull --quiet && docker-compose pull --quiet && docker-compose up -d --force-recreate
        echo -e "${GREEN}Update complete!${NC}"
        ;;

    create-admin)       docker-compose run --rm --entrypoint="" taiga-back python manage.py createsuperuser ;;
    set-password)       docker-compose run --rm --entrypoint="" taiga-back python manage.py changepassword "${2:-admin}" ;;
    list-users)         docker-compose run --rm --entrypoint="" taiga-back python manage.py shell -c "from users.models import User; [print(f'{u.username:20} {u.email:35} {\"(ADMIN)\" if u.is_superuser else \"\"}') for u in User.objects.all().order_by('username')]" ;;
    delete-user)        [ -z "$2" ] && echo "Usage: ./bench.sh delete-user username" && exit 1; docker-compose run --rm --entrypoint="" taiga-back python manage.py shell -c "from users.models import User; u=User.objects.filter(username='$2'); print('Deleted $2' if u.delete()[0] else 'User $2 not found')" ;;

    backup)             FILE=~/taiga-backup-$(date +%F-%H%M%S).sql; docker-compose exec taiga-db pg_dump -U taiga taiga > "$FILE"; echo -e "${GREEN}Backup saved → $FILE${NC}" ;;
    restore)            [ -z "$2" ] && echo "Usage: ./bench.sh restore file.sql" && exit 1; [ ! -f "$2" ] && echo "File not found" && exit 1; docker-compose down -v; docker-compose up -d taiga-db; sleep 8; cat "$2" | docker-compose exec -T taiga-db psql -U taiga taiga; docker-compose up -d --force-recreate; echo -e "${GREEN}Restored from $2${NC}" ;;
    clear-all-data)     read -p "TYPE 'DELETE EVERYTHING' to confirm: " c; [ "$c" = "DELETE EVERYTHING" ] && docker-compose down -v --remove-orphans && echo -e "${RED}ALL DATA ERASED FOREVER${NC}" || echo "Cancelled" ;;
    db-shell)           docker-compose exec taiga-db psql -U taiga taiga ;;
    shell)              docker-compose exec taiga-back bash ;;
    front)              xdg-open http://localhost:9000 2>/dev/null || echo "Open http://localhost:9000" ;;
    admin)              xdg-open http://localhost:9000/admin 2>/dev/null || echo "Open http://localhost:9000/admin" ;;
    migrate)            docker-compose run --rm --entrypoint="" taiga-back python manage.py migrate ;;
    collectstatic)      docker-compose run --rm --entrypoint="" taiga-back python manage.py collectstatic --noinput ;;
    loaddata)           [ -z "$2" ] && echo "Usage: ./bench.sh loaddata fixture.json" && exit 1; docker-compose run --rm --entrypoint="" taiga-back python manage.py loaddata "$2" ;;
    sample-data)        echo -e "${YELLOW}Loading BriskDocu sample projects...${NC}"; docker-compose run --rm --entrypoint="" taiga-back python manage.py loaddata sample_data; echo -e "${GREEN}Sample data loaded!${NC}" ;;

    switch-port-80)
        sed -i 's/localhost:9000/localhost/' .env 2>/dev/null || true
        sed -i 's/9000:80/80:80/' docker-compose.yml 2>/dev/null || true
        docker-compose up -d --force-recreate >/dev/null 2>&1
        echo -e "${GREEN}Switched → http://localhost (BriskDocu clean URL)${NC}"
        ;;

    switch-port-9000)
        sed -i 's/localhost$/localhost:9000/' .env 2>/dev/null || true
        sed -i 's/80:80/9000:80/' docker-compose.yml 2>/dev/null || true
        docker-compose up -d --force-recreate >/dev/null 2>&1
        echo -e "${GREEN}Back to → http://localhost:9000${NC}"
        ;;

    *)
        echo -e "${YELLOW}BriskDocu Commands:${NC}"
        echo "start stop restart rebuild logs status update front admin"
        echo "create-admin set-password list-users delete-user backup restore"
        echo "sample-data loaddata shell db-shell clear-all-data"
        echo "switch-port-80 switch-port-9000"
        echo
        ;;
esac

echo -e "${CYAN}BriskDocu Ready. Welcome, Master.${NC}"
```

```bash
chmod +x bench.sh
```

### Now you are a Taiga

```bash
./bench.sh                 # Epic animated banner appears
./bench.sh start           # Start Taiga
./bench.sh front           # Open in browser
./bench.sh create-admin    # Create admin
./bench.sh backup          # Backup database
./bench.sh switch-port-80  # Magic: http://localhost (no port!)
./bench.sh sample-data     # Load demo projects
```

### Full Command List

| Command                     | Description                                      |
|----------------------------|--------------------------------------------------|
| `./bench.sh start`         | Start Taiga                                      |
| `./bench.sh stop`          | Stop everything                                  |
| `./bench.sh restart`       | Quick restart                                    |
| `./bench.sh rebuild`       | Full rebuild                                     |
| `./bench.sh logs`          | Live logs                                        |
| `./bench.sh status`        | Show containers                                  |
| `./bench.sh update`        | Pull latest Taiga version                        |
| `./bench.sh create-admin`  | Create superuser                                 |
| `./bench.sh set-password`  | Change admin password                            |
| `./bench.sh backup`        | Full DB backup with timestamp                    |
| `./bench.sh restore file`  | Restore from backup                              |
| `./bench.sh sample-data`   | Load official demo projects                      |
| `./bench.sh switch-port-80`| Use clean http://localhost                       |
| `./bench.sh front`         | Open Taiga in browser                            |
| `./bench.sh shell`         | Enter backend container                          |

---

## Bonus: Clean URL (no port)

```bash
./bench.sh switch-port-80
```

Now access Taiga at: **http://localhost**

Switch back anytime:

```bash
./bench.sh switch-port-9000
```

---



**You now have the most powerful, most beautiful, and most satisfying local Taiga instance on Earth.**

Welcome to the future of documentation.

**BriskDocu — Documentation, Perfected.**
```

