# [저스틴 블로그](https://justindglee.com) 를 위한 Strapi CMS 서버

## 실행

- 개발환경에서는 `npm run dev` 을 입력하면 됩니다.
- 개발중, 실제 이용중인 데이터를 이용하기 위해 배포된 production 데이터베이스를 불러와 사용하고 싶을 경우 `.env.development`에 `DATABASE_URL` 환경변수를 설정한 후 `npm run prod` 을 입력하면 됩니다.

### 환경변수

각 환경변수에 대한 설명.

---

사용중인 PostgreSQL의 정보를 입력합니다.

`DATABASE_NAME`: 데이터베이스 이름  
`DATABASE_USERNAME`: 데이터베이스 유저명  
`DATABASE_PASSWORD`: 데이터베이스 비밀번호
`DATABASE_URL`: 위의 세가지 정보가 모두 포함된 데이터베이스 접속용 URL로, `npm run prod` 등의 명령어를 사용해 프로덕션 모드로 연결할 경우 위의 세가지 정보 대신 이것을 사용하여 연결합니다.

Strapi 에서 사용되는 정보들입니다.

`APP_KEYS` : 스트라피는 koa 기반으로, 이 값은 koa session에서 사용됩니다.

> In a Koa application, the app.keys property (often referred to as the "app key") is crucial when setting up sessions. This key is used for signing cookies, ensuring that the data stored in the session is secure and cannot be tampered with by the client.

`API_TOKEN_SALT` : API 토큰을 생성할 때 사용되는 salt이며, 스트라피가 자동으로 .env 파일에 생성해주는 정보입니다. 이 salt를 변경하면 기존의 API 토큰을 모두 사용할 수 없게 되므로 유의하세요. [참고](https://docs.strapi.io/dev-docs/configurations/api-tokens)

아래의 두가지는 새로운 토큰이 만들어질 때 사용되는 비밀 키 입니다. [참고](https://docs.strapi.io/dev-docs/plugins/users-permissions)

`ADMIN_JWT_SECRET`  
`JWT_SECRET`

admin jwt secret이 따로 존재하는 이유는 퍼블릭 API에 사용되는 secret이 탈환되더라도 admin app은 보안을 지키기 위함입니다.

---

1. development

`.env.development` 에서 설정하며,
`config/..` 에서 사용됩니다.

```
  DATABASE_NAME
  DATABASE_USERNAME
  DATABASE_PASSWORD
  DATABASE_URL (optional)
  APP_KEYS
  API_TOKEN_SALT
  ADMIN_JWT_SECRET
  JWT_SECRET
```

2. production

헤로쿠 등 배포환경에서 주어지는 설정환경 또는 `.env.production` 에서 설정하며,
`config/env/production/..` 에서 사용됩니다.

```
  DATABASE_URL
  APP_KEYS
  API_TOKEN_SALT
  ADMIN_JWT_SECRET
  JWT_SECRET
  MY_HEROKU_URL
```

기본적으로는 개발환경과 동일하지만 다음과 같은 차이점이 있습니다.

- 프로덕션 환경에서는 데이터베이스와 관련된 변수들을 `DATABASE_URL` 로 통합하였습니다.
- 그리고 배포된 주소에 해당하는 `MY_HEROKU_URL` (헤로쿠로 배포하였습니다)이 추가됩니다.
