# WEB SCRAPING DATA ENGINEERING PROJECT

Sometime this year, I had an idea to build a data warehouse that serves as a database for Nigerian movies and holds information such as:

+ title of a movie,
+ runtime or duration of a movie,
+ release year of a movie,
+ names of main cast and crew that worked on a movie,
+ movie description, and so on.

This could be used by curious data enthusiasts to build charts, dashboards or even web apps; to uncover insights surrounding the trend of movies in Nigeria over a certain period, best-performing actors and actresses, language diversity of Nigerian movies; and much more.

This project in particular focuses on scraping data from each of the [Nigerian movies hosted on imdb](https://www.imdb.com/search/title/?country_of_origin=NG&sort=alpha,asc&start=1&ref_=adv_nxt) using the following skills:

+ Scrapy framework,
+ Regex,
+ nltk,
+ Postgres,
+ Docker.

## How to Run Scrapy Project with Docker

This entire project was containerized using Docker and here is a quick tutorial on spinning up the containers required to start this project.

+ `git clone` this repository to get a local copy of all files;

+ Spin up your Docker Terminal or CLI;

+ `cd` into the directory that holds the **docker-compose.yml** and run `docker-compose up --build`

> This attempts to start the containers within the **docker-compose.yml** file. The `imdb.pg.cntr` first; once that is successfully started then the `imdb.py.cntr` commences. The **--build** option allows docker to build the python image as specified in the **Dockerfile** and gives it a fixed name: `imdb.image`

+ `docker exec -it imdb.pg.cntr bash` opens an interactive shell to the postgres container to run psql queries.

+ `psql -d imdb -U admin` connects to database as the user **admin**

+ From here SQL queries can be run and the data can be explored.

> Alternatively, this Postgres container can be connected to a PgAdmin GUI as preferred by user; or to a local Postgres instance

+ `docker-compose down` is used to stop all running containers.

+ `docker-compose down -v` is used as an extra option to remove existing volumes for a fresh run of the project, otherwise previous or database would be used.

+ The `imdb.pg.cntr` container is built with a volume to persist the database. This means when both containers run successfully and Scrapy sends data to the imdb database, this is saved to your host computer in a hidden location; to enable reuse of data without docker-compose up every single time.