# GO DDD API

Kumparan Backend Technical Assessment, create REST API with domain driven approach (DDD) using Golang, GORM (Object Relational Mapping), and MySQL

## Installation & Run

First, Make sure you have set up \$GOPATH.

```bash
# Download this project
go get github.com/jojoarianto/go-ddd-api

# It's take several minute to download project
```

Set project environment and run

```bash
# move to project directory
cd $GOPATH/src/github.com/jojoarianto/go-ddd-api
# set env
export DB_USER="db_user";
export DB_PASSWORD="db_pass";
export DB_HOST="db_host";
export DB_PORT="db_port";
export DB_NAME="db_name";
# run golang project
go run main.go
# API Endpoint : http://localhost:8000/api/v1/
```

## Required Features

- `Manajement news` user can manage data news (CRUD)
- `Manajement topic` user can manage data topic (CRUD)
- `Relational model betwean news & topic` many to many (one news can contains multiple topic, one topic has multiple news)
- `filter by news status` filter news by it's status ['draft', 'deleted', 'publish']
- `filter by news topic` filter news by a topic (forinstance: politik)

## Design

- Application
  - Write business logic
    - news.go (GetNews, GetAllNews, &...)
    - topic.go (GetTopic, GetAllTopic, &...)
- Domain
  - Define interface
    - repository interface for infrastructure
  - Define struct
    - Entity struct that represent mapping to data model
      - news.go
      - topic.go
- Infrastructure
  - Implements repository interface
    - news_repository.go
    - topic_repository.go
- Interfaces
  - HTTP handler

## URL ENDPOINT

#### /api/v1/news

- `GET` : Get all news
- `POST` : Create a news

#### /api/v1/news/:news_id

- `GET` : Get a news by id
- `PUT` : Update a news by id
- `DELETE` : Delete a news by id

#### /api/v1/topic

- `GET` : Get all topic
- `POST` : Create a topic

#### /api/v1/topic/:news_id

- `GET` : Get a topic by id
- `PUT` : Update a topic by id
- `DELETE` : Delete a topic by id

### Usage Examples

Get all news, URL GET `/api/v1/news`

```json
[
    ...
    {
		"ID": 2,
		"CreatedAt": "0001-01-01T00:00:00Z",
		"UpdatedAt": "0001-01-01T00:00:00Z",
		"DeletedAt": null,
		"title": "Sebuah Mobil Terperosok ke Sungai di Kalimalang",
		"slug": "sebuah-mobil-terperosok-ke-sungai-di-kalimalang",
		"content": "Sebuah mobil jenis mini bus terperosok ke sungai di Kalimalang, Bekasi, ... Erna mengungkapkan, mobil ditemukan terperosok sekitar pukul ...",
		"status": "draft",
		"Topic": [
            {
            "ID": 5,
            "CreatedAt": "0001-01-01T00:00:00Z",
            "UpdatedAt": "2019-01-15T22:57:05Z",
            "DeletedAt": null,
            "name": "Berita",
            "slug": "berita"
            }
        ]
	},
    ...
]
```

Create a news example, URL POST `/api/v1/news` with json

```json
{
  "title": "Sebuah Mobil Terperosok ke Sungai di Kalimalang",
  "slug": "sebuah-mobil-terperosok-ke-sungai-di-kalimalang",
  "status": "draft",
  "content": "Sebuah mobil jenis mini bus terperosok ke sungai di Kalimalang, Bekasi, ... Erna mengungkapkan, mobil ditemukan terperosok sekitar pukul ...",
  "Topic": [
    {
      "ID": 5,
      "CreatedAt": "0001-01-01T00:00:00Z",
      "UpdatedAt": "2019-01-15T22:57:05Z",
      "DeletedAt": null,
      "name": "Berita",
      "slug": "berita"
    }
  ]
}
```

## Product Items Backlog

- [ ] **Mandatory:** create REST API News & Topic CRUD
  - [ ] News
    - [x] Get all
    - [x] Get by id
    - [x] Create
    - [ ] Update
    - [ ] Delete
  - [x] Topic
    - [x] Get all topic
    - [x] Get by id
    - [x] Create
    - [x] Update
    - [x] Delete
- [x] **Mandatory:** create Filter
  - [ ] Filter by status news
  - [ ] Filter by topic
- [ ] **Mandatory:** API Functional Test
- [ ] **opsional:** Deploy to (heroku/aws/azure/digital ocean)
- [ ] **opsional:** Database setup
  - [x] Migration schema DB
  - [ ] Seeding DB

## Reference

DDD Skeleton : https://github.com/takashabe/go-ddd-sample
GORM Documentation : http://doc.gorm.io
