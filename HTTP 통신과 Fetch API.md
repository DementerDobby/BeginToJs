
## HTTP 요청 / 응답의 기본 구조
### HTTP란?
- **Hypertext Transfer Protocol**의 약자로, 클라이언트와 서버 간 데이터를 교환하는 프로토콜.
- 브라우저, 모바일 앱, API 호출 등에서 사용.

### 요청(Request) 구조
- 주요 구성 요소:
	- **URL**: 요청을 보낼 서버 주소.
	- **HTTP 메서드**: 요청의 동작을 정의 (`GET`, `POST` 등).
	- **헤더(Header)**: 추가 정보를 포함 (예: 인증 토큰, 데이터 타입).
	- **본문(Body)**: POST, PUT 요청에서 데이터를 포함.

### 응답(Response) 구조
- 주요 구성 요소 : 
	- **상태 코드(Status Code)**: 요청 결과를 나타내는 숫자.
	- **헤더(Header)**: 응답 정보 (예: 데이터 타입).
	- **본문(Body)**: 서버가 반환한 데이터.



## HTTP 메서드와 상태 코드
### HTTP 메서드
| 메서드      | 설명             |
| -------- | -------------- |
| `GET`    | 데이터를 서버에서 가져옴. |
| `POST`   | 데이터를 서버에 전송.   |
| `PUT`    | 서버의 데이터를 업데이트. |
| `DELETE` | 데이터를 서버에서 삭제.  |

### HTTP 상태 코드
| 상태 코드 | 설명                             |
| ----- | ------------------------------ |
| `200` | 성공 (OK).                       |
| `201` | 리소스 생성 성공 (Created).           |
| `400` | 잘못된 요청 (Bad Request).          |
| `401` | 인증 실패 (Unauthorized).          |
| `404` | 리소스 없음 (Not Found).            |
| `500` | 서버 오류 (Internal Server Error). |



## Fetch API
### Fetch API란?
- 브라우저 내장 API로 HTTP 요청을 비동기적으로 처리.
-  프로미스를 반환.

### 기본 사용법
```JavaScript
fetch("https://jsonplaceholder.typicode.com/posts") 
.then((response) => response.json()) 
.then((data) => console.log(data)) 
.catch((error) => console.error("Error:", error));
```

### HTTP 메서드 사용
#### ```GET``` 요청
- 서버에서 데이터를  가져오기 
```JavaScript
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

#### ```POST```요청
- 데이터를 서버에 전송
```JavaScript
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    title: "foo",
    body: "bar",
    userId: 1,
  }),
})
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

#### ```PUT```요청
- 데이터를 업데이트 
```JavaScript
fetch("https://jsonplaceholder.typicode.com/posts/1", {
  method: "PUT",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    id: 1,
    title: "updated title",
    body: "updated body",
    userId: 1,
  }),
})
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

#### ```DELETE```요청
- 데이터를 삭제 
```JavaScript
fetch("https://jsonplaceholder.typicode.com/posts/1", {
  method: "DELETE",
})
  .then((response) => {
    if (response.ok) {
      console.log("Deleted successfully");
    } else {
      console.error("Failed to delete");
    }
  })
  .catch((error) => console.error("Error:", error));
```



## 에러 처리와 요청 옵션
####  에러 처리 
-  네트워크 요청이 실패했을 때 대처법 
``` JavaScript
fetch("https://invalid-url.com")
  .then((response) => {
    if (!response.ok) {
      throw new Error("HTTP error: " + response.status);
    }
    return response.json();
  })
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

#### 요청 옵션
- ```headers``` : 요청 헤더 설정
- ```body``` : 데이터를 포함하는 요청에 설정
``` JavaScript
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer YOUR_TOKEN",
  },
  body: JSON.stringify({
    title: "New Post",
    body: "Content of the new post",
    userId: 1,
  }),
});
```
