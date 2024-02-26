# Gitlab + GitLab Runner + Docker

### Как потрогать:

### 1. Устанавливаем docker desktop. Запускаем

### 2. В файле `docker-compose.yml` меняем hostname на свой ip

### 3. В корне запускаем команду `docker-compose up -d --force-recreate && docker-compose ps  `

### 4. Gitlab запустится на ip:80

### 5. Что бы получить текущий пароль:

- Заходим в контейнер gitlab: `docker exec -it gitlab_gitlab_1 bash` _gitlab_gitlab_1 = имя контейнера_
- После подключения пишем `grep 'Password:' /etc/gitlab/initial_root_password`
- забираем пароль, заходим **root** : **password**

### 6. Подключение раннера:

- подключаемся в контейнер ранера
- вводим `gitlab-runner register`
- следуем по шагам в cli. Подробнее [тут](https://docs.gitlab.com/runner/register/?tab=Docker)

#### PS.

<details>
  <summary>Как узнать свой ip (Windows)  </summary>

#### в cmd\powershell пишем `ipconfig`

ищем примерно такое:  
`IPv4-адрес. . . . . . . . . . . . : 192.168.1.38`

</details>


#### PS #1.

Что бы работал кэш среди локальных ранеров, нужно в настройках ранера (`config.toml`) [явно указать мапинг для volume](https://gitlab.com/gitlab-org/gitlab-runner/-/issues/36877#note_1572421182)  
пример файла:
```yml
concurrent = 5
check_interval = 0
connection_max_age = "15m0s"
shutdown_timeout = 0

[session_server]
  session_timeout = 1800

[[runners]]
  name = "docker-runner"
  url = "http://192.168.1.38/"
  id = 1
  token = "zKHfrn8UPiT1yM_5VgXV"
  token_obtained_at = 2024-02-25T15:35:13Z
  token_expires_at = 0001-01-01T00:00:00Z
  executor = "docker"
  [runners.docker]
    tls_verify = false
    image = "docker:stable"
    privileged = false
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["/mnt/gitlab-runner/cache:/cache"]
    shm_size = 0
    network_mtu = 0

[[runners]]
  name = "docker-runner2"
  url = "http://192.168.1.38/"
  id = 2
  token = "uoBV8rNjLx_N-2wVJ7hT"
  token_obtained_at = 2024-02-26T15:31:15Z
  token_expires_at = 0001-01-01T00:00:00Z
  executor = "docker"
  [runners.cache]
    MaxUploadedArchiveSize = 0
  [runners.docker]
    tls_verify = false
    image = "docker:stable"
    privileged = false
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["/mnt/gitlab-runner/cache:/cache"]
    shm_size = 0
    network_mtu = 0

```

  
#### PS #2.

<details>
  <summary>Источники которые использовал для настройки</summary>
  
#### [doc](http://snakeproject.ru/rubric/article.php?art=gitlab_docker_03_02_2022)

</details>

#### PS #3.

- Есть возможность хранить данные в файлах (т.е. docker volume не внутри докера) данный пример лежит в ветке `windows-file-volume` текущего репозитория. **_НО!! там не работают артефакты. как раз по причине маппинга данных для docker-volume._**  
  **Решение:** либо использовать linux (туториал в доках) либо хранить данные в volumes от докера (если windows)
