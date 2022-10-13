<div align="center">
    <h1>
        Accounts API
    </h1>
</div>

## ResponseBlock
```Rust
pub struct ResponseBlock<T> {
    pub status: bool,
    pub body: T,
}
```

항상 모든 응답들은 `ReponseBlock<T>`를 `json`으로 serialization한 결과로 주어진다.

이때, `T`는 trait `Serialize + Deserialize`를 만족하는 구조체이고, 이 문서의 모든 섹션마다 Request(요청) 또는 Response(응답)이 명시되어있는 경우 각각 그 이후에 따르는 구조체는 `T`의 역할을 한다.

## Enums

### AccountError

Account API를 이용할때, 에러를 표시하기 위한 Enum이다.

```Rust
pub enum AccountError {
    None,
    NotLoggedIn,
    AlreadyLoggedIn,
    DatabaseError,
    PassNotMatched,
    UserNotExists,
}
```

### AccountPerm

Account에 지정된 권한을 나타내는 Enum이다.

```Rust
pub enum AccountPerm {
    User,
    Admin,
}
```

## General

### `GET` /api/accounts/self

Token 만료기간 연장

#### **Request**
`()` (단, 요청 헤더의 `Cookie`가 이용됨)

#### **Response**
````Rust
{
    uuid: Uuid,
    id: String,
    permission: AccountPerm,
    timezone: chrono_tz::Tz,
    first_name: String,
    last_name: String,
    email: String,
    preferred_language: String,
}
````

### `DELTE` /api/accounts/self

로그아웃

#### **Request**
`()` (단, 요청 헤더의 `Cookie`가 이용됨)

#### **Response**
`AccountError`

### `POST` /api/accounts/login

로그인

#### **Request**
```Rust
{
    id: String,
    password: String,
}
```

#### **Response**
`AcccountError`

### `POST` /api/accounts/register

회원가입

## ADMIN ONLY

### `POST` /api/accounts/admin/register

관리자 권한으로 강제 회원가입 (Permission 등을 조정할 수 있음)