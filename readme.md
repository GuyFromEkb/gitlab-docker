# Gitlab + GitLab Runner + Docker


### Как потрогать:

### 1. Устанавливаем docker desktop. Запускаем
### 2. Извлекаем архив в корень

```
├── readme.md             
├── docker-compose.yml    
├── data-gitlab
    ├── ...      
```
### 3. Чуток печатаем
- изменяем в файле `.\docker-compose.yml` `hostname: __LOCAL IP__`
- изменяем в файле `.\data-gitlab\etc\gitlab-runner\config.toml` 
```
url = "http://__LOCAL_IP__:8000/"
clone_url = "http://__LOCAL_IP__:8000/"
```  
 
### 4. В корне запускаем команду `docker-compose up -d --force-recreate && docker-compose ps  `

web: http://LOCAL_IP:8000/  
login: root  
pw: mGDjtXZF


#### PS.
<details>
  <summary>Как узнать свой ip (Windows)  </summary>   
  
в cmd\powershell пишем `ipconfig`  
  ищем такое примерно такое:  
`IPv4-адрес. . . . . . . . . . . . : 192.168.1.38`
</details>   

#### PS #2.
<details>
  <summary>Источники которые использовал для настройки</summary>
  
#### [doc](http://snakeproject.ru/rubric/article.php?art=gitlab_docker_03_02_2022)  
#### [register gitlab runner in docker](https://docs.gitlab.com/runner/register/?tab=Docker)

</details>
