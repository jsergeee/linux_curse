# Механизмы пространства имен 

## Контейнеризация Урок 1



| Пространство имен    | Что изолируется |
| ---- | ---- |
|PID |Изоляция идентификатора процессов|
|Network|Сетевая изоляция (сеть, порты, стеки итак далее|
|User |Изоляция пользователей и групп|
|Mount|Переопределение точек монтирования|
|IPC (Inter Process Communication)|Изоляция меж процессного взаимодействия (в т.ч. очереди POSIX)|
|UTS (UNIX Time-Sharing)|Изоляция имени хоста и доменного и имени|

PID для запущенных процессов в системе можно найти с помощью, например, команды `ps` либо команды `top`: 

- ps – сообщает моментальный снимок текущих процессов. 

- top выводит список запущенных процессов в реальном времени.







Основные команды ДК:

- `docker-compose build` - команда позволяет собрать сервисы, описанные в конфигурационных файлах 
- `ocker-compose up -d` - запускает наш проект. В данном случае проект запустится в фоновом режиме, так как в команде присутствует флаг -d 
-  `docker-compose start` - запускает любые остановленные ранее сервисы в соответствии с указанными параметрами 
- `docker-compose down` - останавливает наш проект и, что немаловажно, удаляет все сервисы, которые были запущены ранее 
- `docker-compose stop` - эта команда просто останавливает все сервисы, описанные в конфигурации. Она не удаляет контейнеры, тома, сети и прочие сущности, описанные в конфигурационном файле 
- `docker-compose logs -f [service name]` - с помощью этой команды можно посмотреть логи нашего сервиса 
- `docker-compose ps` - выводит на экран список всех доступных контейнеров 
- `docker-compose exec [service name] [command]` - с ее помощью можно выполнить команду в сервисе, не заходя при этом в контейнер. Ранее мы рассматривали подобное на уроке “Введение в Docker” 
- `docker-compose images` - позволяет вывести список образов.







Docker Compose и Docker Swarm — это два инструмента, которые помогают управлять контейнерами Docker, но они предназначены для разных целей и имеют разные функции.

### Docker Compose

**Docker Compose** — это инструмент для определения и запуска многоконтейнерных приложений. Он позволяет вам описать всю архитектуру вашего приложения в одном YAML-файле (`docker-compose.yml`), где вы можете указать, какие контейнеры вам нужны, их конфигурацию, зависимости, сети и тома.

**Основные характеристики:**
- **Локальная разработка:** Compose идеально подходит для разработки и тестирования приложений на локальной машине.
- **Простота использования:** С помощью одной команды (`docker-compose up`) вы можете запустить все сервисы, указанные в вашем `docker-compose.yml`.
- **Поддержка многоконтейнерных приложений:** Вы можете легко управлять несколькими контейнерами и их зависимостями.

**Пример `docker-compose.yml`:**
```yaml
version: '3'
services:
  web:
    image: nginx ports:
      - "80:80"
  db:
    image: mysql environment:
      MYSQL_ROOT_PASSWORD: example
```

### Docker Swarm

**Docker Swarm** — это встроенное средство оркестрации Docker, которое позволяет управлять кластером Docker-демонов (узлов) как единым виртуальным хостом. Swarm обеспечивает высокую доступность и масштабируемость приложений.

**Основные характеристики:**
- **Оркестрация:** Swarm позволяет автоматически распределять контейнеры по узлам кластера, управлять их состоянием и обеспечивать отказоустойчивость.
- **Масштабируемость:** Вы можете легко масштабировать сервисы, добавляя или удаляя контейнеры.
- **Службы и задачи:** В Swarm вы определяете службы, которые могут автоматически масштабироваться и обновляться.

**Пример создания сервиса в Swarm:**
```bash
docker service create --name web --replicas 3 -p 80:80 nginx
```

### Сравнение

| Характеристика   | Docker Compose                                    | Docker Swarm                                                 |
| ---------------- | ------------------------------------------------- | ------------------------------------------------------------ |
| Цель             | Локальная разработка многоконтейнерных приложений | Оркестрация контейнеров в кластере                           |
| Масштабируемость | Ограниченная (локальная машина)                   | Высокая (распределенные узлы)                                |
| Команды          | `docker-compose up`, `docker-compose down`        | `docker service create`, `docker stack deploy`               |
| Конфигурация     | YAML файл для описания сервисов                   | YAML файл для описания стеков (может быть использован с Compose) |

### Заключение

Docker Compose и Docker Swarm могут использоваться вместе. Например, вы можете разработать приложение с помощью Docker Compose, а затем развернуть его в Docker Swarm для масштабирования и управления на уровне кластера.
