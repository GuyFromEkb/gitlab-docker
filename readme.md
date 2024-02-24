# Gitlab + GitLab Runner + Docker


### Как потрогать:

1. Устанавливаем docker desktop. Запускаем
2. извлекаем архив в корень

```
├── readme.md             
├── docker-compose.yml    
├── data-gitlab
    ├── ...      
```
3. в корне запускаем команду `docker-compose up -d --force-recreate && docker-compose ps  `

web: http://192.168.1.38:8000/  
login: root  
pw: mGDjtXZF



<details>
  <summary>Источники которые использовал для настройки</summary>
  
#### [doc](http://snakeproject.ru/rubric/article.php?art=gitlab_docker_03_02_2022)  
#### [register gitlab runner in docker](https://docs.gitlab.com/runner/register/?tab=Docker)

</details>