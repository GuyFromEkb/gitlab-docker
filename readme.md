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

#### PS #2.

<details>
  <summary>Источники которые использовал для настройки</summary>
  
#### [doc](http://snakeproject.ru/rubric/article.php?art=gitlab_docker_03_02_2022)

</details>

#### PS #3.

- Есть возможность хранить данные в файлах (т.е. docker volume не внутри докера) данный пример лежит в ветке `windows-file-volume` текущего репозитория. **_НО!! там не работают артефакты. как раз по причине маппинга данных для docker-volume._**  
  **Решение:** либо использовать linux (туториал в доках) либо хранить данные в volumes от докера (если windows)
