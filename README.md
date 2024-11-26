# 안익수 202030318

## 새로운 내용은 위에

## 14주차 정리(11.27)

## css와 내장 스타일링 메서드

### 1. Styled JSX

"Next.js"는 React 기반의 웹 프레임워크로, 클라이언트 및 서버 사이드 렌더링, 라우팅, 코드 분할 등을 지원하는데, "styled-jsx"는 Next.js에서 제공하는 CSS-in-JS 라이브러리 중 하나입니다. "styled-jsx"를 사용하면 JavaScript 파일 안에서 CSS 스타일을 정의할 수 있습니다.

"Next.js"와 "styled-jsx"를 함께 사용할 때, "styled-jsx"는 기본적으로 각 컴포넌트에 대한 스타일을 지정하는 데 사용됩니다. "styled-jsx"를 통해 정의된 스타일은 해당 컴포넌트의 스코프에만 적용되므로 전역 스타일 충돌을 방지할 수 있습니다.

아래는 "styled-jsx"를 사용한 예시입니다:

- 기본 사용법

```jsx
const MyComponent = () => (
  <div>
    <p>Some text</p>
    <style jsx>{`
      p {
        color: red;
      }
    `}</style>
  </div>
);
```

위의 예시에서 **`<style jsx>`** 태그 내부에 작성된 CSS는 **`MyComponent`** 컴포넌트에만 적용됩니다.

- 동적 스타일링

```jsx
const dynamicColor = "blue";

const DynamicStyleComponent = () => (
  <div>
    <p>Dynamic styling</p>
    <style jsx>{`
      p {
        color: ${dynamicColor};
      }
    `}</style>
  </div>
);
```

위의 예시에서 **`${dynamicColor}`**를 통해 JavaScript 변수를 사용하여 동적으로 스타일을 정의할 수 있습니다.

- **글로벌 스타일링**

```jsx
export default () => (
  <div>
    <p>Global styling</p>
    <style jsx global>{`
      body {
        background: #f0f0f0;
      }
    `}</style>
  </div>
);
```

의 예시에서 **`<style jsx global>`**을 사용하여 글로벌 스타일을 정의하고 있습니다.

"styled-jsx"를 사용하면 컴포넌트 기반의 스타일링을 할 수 있어 유지보수성이 높아지며, 동시에 스타일 관리가 간편해집니다.

### CSS Module

CSS Modules는 CSS를 모듈화하여 컴포넌트 범위에서 스타일을 관리하는 방법 중 하나입니다. 이를 통해 전역 스코프를 방지하고, 스타일을 모듈로 구성하여 재사용성을 높일 수 있습니다. 주로 React와 함께 사용되며, Next.js와 Create React App 등의 프로젝트에서 기본적으로 지원됩니다.

여기에는 CSS Modules의 기본적인 사용법이 포함되어 있습니다:

- **CSS 모듈 생성:**

CSS 모듈은 파일 이름에 **`.module.css`** 확장자를 사용하여 생성됩니다.

```css
cssCopy code
/* styles.module.css */

.myComponent {
  color: blue;
}

.button {
  background-color: green;
}
```

- **React 컴포넌트에서 사용:**
  React 컴포넌트에서 해당 CSS 모듈을 불러와 사용합니다.

  ```jsx
  jsxCopy code
  // MyComponent.jsx

  import React from 'react';
  import styles from './styles.module.css';

  const MyComponent = () => (
    <div className={styles.myComponent}>
      <p>This is styled using CSS Modules</p>
      <button className={styles.button}>Click me</button>
    </div>
  );

  export default MyComponent;

  ```

  위의 예시에서 **`styles.myComponent`** 및 **`styles.button`**은 CSS 클래스 선택자로 사용되며, 이들은 실제로 컴파일된 클래스 이름과 매핑됩니다.

- **동적 클래스 이름 사용:**
  동적으로 클래스 이름을 생성할 수도 있습니다.

  ```jsx
  jsxCopy code
  import React from 'react';
  import styles from './styles.module.css';

  const isDisabled = true;

  const MyComponent = () => (
    <button className={`${styles.button} ${isDisabled ? styles.disabled : ''}`}>
      Click me
    </button>
  );

  ```

  위의 예시에서 **`styles.disabled`**는 조건에 따라 동적으로 적용되는 클래스입니다.

CSS Modules를 사용하면 클래스 이름이 전역 스코프로 노출되지 않으므로 클래스 이름 충돌이 방지됩니다. 또한, 코드 내에서 클래스 이름을 하드코딩하는 것이 아니라 모듈에서 가져와 사용하므로 코드 유지보수성이 향상됩니다.

Sass는 Syntactically Awesome Stylesheets의 약자로, CSS의 확장된 문법을 제공하는 CSS 전처리기입니다. Sass를 사용하면 반복 코드를 줄이고, 변수, 중첩 규칙, 함수 등을 활용하여 스타일시트를 더 효과적으로 관리할 수 있습니다. Sass는 두 가지 구문을 제공하는데, 하나는 SCSS(Sassy CSS)이고 다른 하나는 들여쓰기 기반의 문법입니다.

### **SCSS 구문:**

1. **변수 사용:**

   ```scss
   scssCopy code
   $primary-color: #3498db;

   .myComponent {
     color: $primary-color;
   }

   ```

2. **중첩 규칙:**

   ```scss
   scssCopy code nav {
     ul {
       margin: 0;
       padding: 0;
       list-style: none;
     }

     li {
       display: inline-block;
     }

     a {
       text-decoration: none;

       &:hover {
         border-bottom: 1px solid #ccc;
       }
     }
   }
   ```

3. **파일 분할:**

   Sass를 여러 파일로 나누고 **`@import`**를 사용하여 합칠 수 있습니다.

   ```scss
   scssCopy code
   // _variables.scss
   $primary-color: #3498db;

   // styles.scss
   @import '_variables';

   .myComponent {
     color: $primary-color;
   }

   ```

### **들여쓰기 기반의 문법:**

1. **변수 사용:**

   ```sass
   sassCopy code
   $primary-color: #3498db

   .myComponent
     color: $primary-color

   ```

2. **중첩 규칙:**

   ```sass
   sassCopy code
   nav
     ul
       margin: 0
       padding: 0
       list-style: none

     li
       display: inline-block

     a
       text-decoration: none

       &:hover
         border-bottom: 1px solid #ccc

   ```

Sass는 CSS로 컴파일되어 웹 브라우저에서 해석됩니다. 다양한 기능과 유용한 도구를 제공하여 스타일 시트의 가독성과 유지보수성을 향상시킬 수 있습니다. Sass는 주로 프로젝트에서 스타일링 작업을 수행하는데 사용되며, 많은 웹 개발자들에게 사랑받고 있습니다.

## 13주차 정리(11.20)

## 지역 및 전역 상태 관리

- 리액트 앱에서는 상태 관리는 아주 중요한 부분입니다.
- 상태는 동적 정보의 일종입니다.
  1. 높은 수준의 상호 작용이 가능한 내 구현하거나.
  2. 더 뛰어난 UX 개발 위한 필수 요소입니다.
- 최신 웹앱에서는 비가 상태를 사용하고, 관리하는 경우가 많이 있습니다.
  1. 밝은 테마에서 어두운 테마로 변경하거나,
  2. 배송 주소를 바꿈으로써 폼의 상태를 변경합니다.

1. 버튼 클릭 만으로 앱의 상태를 변하게 할 수도 있다.

- 상태 관리 때문에 앱에 더 뛰어난 상호 작용 등의 기능을 구현할 수 잊지만, 앱의 복잡도는 증가 합 니다.
- 리액트는 클래스 컴포넌트 시절부터 setState 메소드를 사용해서 상태를 관리했습니다.
- 리액트 16.8 이후부터는 usestate 혹을 포함한 리액트 흑을 제공합니다.
- 리액트 앱의 상태 관리가 어려운 것은 데이터의 흐름이 단방향이라는 것입니다.
- 부모 컴포넌트는 자식에게 속성의 형태로 상태를 전달할 수 있지만, 반대로 자식이 부모에게 태를 전달 할 수 없습니다.
- 지역 상태는 클래스 컴포넌트나 훅을 사용해서 별다른 어려움 없이 관리할 수 있지만, 전역 상태는 단방향 데이터 흐름 때문에 관리하기가 힘듭니다.

### 지역 상태 관리

```jsx
import React, ( useState } from "react";
function Counter { initialCount = 0 )) {
const [count, setCount] = useState(initialCount);

return (
‹div›
<b>Count is: {count)</b><br />
‹button onClick=(() = setCount (count + 1)}›
Increment +
</button>
<button onClick={() = setCount (count - 1)}>
Decrement - </button>
</div>

export default Counter;
```

- 지역 상태 관리에 있어서 앱의 상태는 컴포넌트 스코프 상태를 의미합니다.
- Increment버튼을 클릭하면 현재 click하면 count값에 1을 더하고, Decrement버튼을 클릭하면 현재 값에서 1을 뺍니다.
- 부모 컴포넌트는 자식에게 initialCount라는 속성값을 통해서 초기 counter값을 쉽게 전달할 수 있습니다
- 이 때는 useState 흑만으로 필요한 모든 것을 구현할 수 입니다

### 전역 상태 관리

- 전역 상태는 여러 컴포넌트가 공유하는 상태를 의미합니다.
- 즉, 어떤 컴포넌트라도 접근 및 수정이 가능한 상태인 것입니다.
- Vue.js4 Angular와는 다르게 React는 데이터 흐름이 단방향 입니다.
- 단방향의 데이터 흐름은 1) 오류 발생 가능성을 줄여 주고, 2) 디버깅하기 쉬우며 효율적이라는 장점이 있습니다.
- 반면 앱 개발이 더 복잡해 진다는 단점도 있습니다.
- 예를 들어 상품목록 카드에서 원하는 물건을 고르면, 장바구니에 담긴 항목의 숫자를 표시하는 기 능을 구현 한다고 생각해 보면 어려움을 잘 알 수 있습니다.
- 내비게이션 바와 상품 목록 카드 간에 어떠한 연결점도 없기 때문입니다.
- 카드 컴포넌트가 가지고 있는 데이터 들은 언마운트 되는 즉시 지역 상태를 잃게 됩니다
- 최근 앱에서는 다양한 라이브러리를 사용해서 이런 상태 관리를 구현합니다.

## 12주차 정리(11.13)

## GraphQL API

2012년에 메타(페이스북)에서 개발했습니다

- API에서 사용할 수 있는 질의어로 RESTLI SOAP 같은 방식과는 다른 새로운 관점으로 API
  데이터를 다릅니다.
- 꼭 필요한 데이터만 불러오도록 지정할 수 있습니다
- 한 번의 요청으로 여러 곳의 데이터를 불러올 수 있습니다 시용형 네이티에 대해 정적이면서도 강력한 타입 시스템을 제공합니다.
  이 밖에도 많은 장점을 가지고 있습니다.
- 아래와 같이 사용할 수 있습니다

```jsx
import { ApolloServer, gql } from "apollo-server-micro";
import GraphQLJSON from "graphql-type-json";
import "crypto";

const sign_db = [];

function uuidv4() {
  return "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx".replace(/[xy]/g, function (c) {
    var r = (Math.random() * 16) | 0,
      v = c == "x" ? r : (r & 0x3) | 0x8;
    return v.toString(16);
  });
}

const typeDefs = gql`
  scalar JSON
  input InsertSign {
    nickname: String!
    content: String!
    country: String
  }
  type Query {
    sign(offset: Int!, limit: Int!, order_by: JSON): [Sign]!
  }
  type Mutation {
    insert_sign(objects: InsertSign): NewSign
  }
  type NewSign {
    returning: Sign
  }
  type Sign {
    uuid: ID
    created_at: String
    content: String
    nickname: String
    country: String
  }
`;

const resolvers = {
  Query: {
    sign(_, args) {
      const variable = JSON.parse(JSON.stringify(args));
      const offset = variable.offset;
      const limit = variable.limit;
      const order_by = variable.order_by.created_at;
      const sort_func =
        order_by.created_at === "desc"
          ? (a, b) => Number(a.created_at) - Number(b.created_at)
          : (a, b) => Number(b.created_at) - Number(a.created_at);
      const signlist = sign_db.sort(sort_func).slice(offset, offset + limit);
      return signlist;
    },
  },
  Mutation: {
    insert_sign(_, objects) {
      const uuid = uuidv4();
      const contents = JSON.parse(JSON.stringify(objects));
      const created_at = Date.now();
      const newSign = {
        ...contents.objects,
        created_at,
        uuid,
      };
      sign_db.push(newSign);
      return { returning: newSign };
    },
  },
};

const apolloServer = new ApolloServer({ typeDefs, resolvers });
const startServer = apolloServer.start();

export default async function handler(req, res) {
  await startServer;
  await apolloServer.createHandler({
    path: "/api/graphql",
  })(req, res);
}

export const config = {
  api: {
    bodyParser: false,
  },
};
```

```jsx
import Link from "next/link";
import { useQuery } from "@apollo/client";
import GET_LATEST_SIGNS from "../lib/apollo/queris/getLatestSigns";
import Sign from "../components/Sign";
import Loading from "../components/Loding";

function HomePage() {
  const { loading, data } = useQuery(GET_LATEST_SIGNS, {
    fetchPolicy: "no-cache",
  });

  if (loading) {
    return <Loading />;
  }

  return (
    <div className="flex justify-center items-center flex-col mt-20">
      <h1 className="text-3xl mb-5">Real-World Next.js signbook</h1>
      <Link href="/new-sign">
        <button className="mb-8 border-2 border-purple-800 text-purple-900 p-2 rounded-lg text-gray-50 m-auto mt-4">
          Add new sign
        </button>
      </Link>
      <div>
        {data.sign.map((sign) => (
          <Sign key={sign.uuid} {...sign} />
        ))}
      </div>
    </div>
  );
}

export default HomePage;
```

- Apollo 트라이어트를 초기화하기 위한 함수를 추가합니다. 113페이지 하단의 코드
- 이 함수를 사용하면 페이지마다 새로운 Apollo 클라이언트를 만들지 않아도 됩니다
- 대신 글라이언트 인스턴스를 apolloClient 변수에 저장하여, 인스턴스를 함수 인자에 초기 상태값으로 전달합니다.
- 해당 함수는 지역 캐시값과 전달받은 조기 상태값을 합쳐서 전체 상태값을 만들어 사용합니다

## 11주차 정리 (11.06)

## SSR 과 CSR REST API 사용

### 서버에서 REST API 사용하기

- REST API를 호출할 때는 public AP를 호출할 것인지, private API를 호출할 것인지를 먼저 확인해야 합니다.
- Publie API는 어떤 인증이나 권한도 필요 없으며 누구나 호출할 수 있습니다.
- Private API는 호출 전 반드시 인증과 권한 검사 과정을 거쳐야 입니다
- 예를 들어 구글의 AP를 사용하고 싶다면 OAuth 20을 사용해야 합니다. 거의 산업 표준이라고 할 수 있습니다.
- 이 밖에 API들도 어떻게 인증과 권한 검사 과정을 거치는지 반드시 확인해야 합니다.

위 실습은 Axios를 사용해서 진행되는데

Axios 란? Axios는 **브라우저, Node.js를 위한 Promise API를 활용하는 HTTP 비동기 통신 라이브러리**이다.

프로젝트에 Axios 라이브러리를 설치하기 위해서는 아래와 같은 명령어를 터미널에 입력해 주면 된다.

```bash
$ npm install axios
```

그럼 아래와 같은 코드를 실행할 수 있게 된다.

```jsx
import Link from "next/link";
import axios from "axios";

export async function getServerSideProps(ctx) {
  const { username } = ctx.query;
  const { status, data } = await axios.get(
    `${process.env.API_ENDPOINT}/api/04/users/${username}`,
    {
      headers: {
        authorization: process.env.API_TOKEN,
      },
    }
  );

  if (status === 404) {
    return {
      notFound: true,
    };
  }

  return {
    props: {
      user: data,
    },
  };
}

function UserPage({ user }) {
  return (
    <div>
      <div>
        <Link href="/" passHref>
          Back to home
        </Link>
      </div>
      <hr />
      <div style={{ display: "flex" }}>
        <img
          src={user.profile_picture}
          alt={user.username}
          width={150}
          height={150}
        />
        <div>
          <div>
            <b>Username:</b> {user.username}
          </div>
          <div>
            <b>Full name:</b> {user.first_name} {user.last_name}
          </div>
          <div>
            <b>Email:</b> {user.email}
          </div>
          <div>
            <b>Company:</b> {user.company}
          </div>
          <div>
            <b>Job title:</b> {user.job_title}
          </div>
        </div>
      </div>
    </div>
  );
}

export default UserPage;
```

위에 코드를 보면 process.env.API_TOKEN가 나와있는데 이걸 왜 사용했느냐

직접 써도 되지만 다음과 같은 이유로 권장하지 않습니다.

1. 인증 토큰은 비밀번호와 같이 반드시 지켜야 할 비밀 정보로 간주해야 합니다
2. 앱을 로컬에서 실행하면 테스트 토큰을 사용해서 API에 접근하며, 배포한 후에는 다른 토큰을 사용합니다.

- 환경 변수를 사용하면 서로 다른 배포 및 실행 환경에서 다른 토큰을 더 쉽게 사용할 수 있습니다.

습니다.

3. API 토큰 값이 바뀌면 환경 변수나 설정 파일의 값을 바꾸는 것으로 쉽게 적용할 수 있습니다

- Root 디렉토리에 .env라는 파일을 만들고 다음 코드를 작성합니다.
- .env 파일은 중요한 정보가 들어 있기 때문에 절대 커밋하면 안 됩니다.
- .gitignore파일에 등록해 주세요.
- Next는 .env나 .envlocal 파일을 지원하기 때문에 별도의 설정은 필요하지 않습니다.

### SSR로 데이터를 불러오는 이유

- 서버가 데이터를 불어오는 것이 좀 더 안전함
- API 엔드포인트 주소, 매개변수 값, HTTP 헤더, 인증 토큰 값 등 중요한 정보가 외부에 노출되지 않기 때문임

### 클라이언트가 데이터 불러오기

- 브라우저에서 HTTP 요청을 보낼 때는 반드시 다음 사항을 지켜야 합니다.

1. 믿을 수 있는 곳에만 HTTP 요청을 보내야 합니다
2. SSL 인증서를 통해 안전하게 접근할 수 있는 곳의 HTTP API만 사용해야 합니다.
3. 브라우저에서 원격 데이터베이스에 직접 연결해서는 안 됩니다.

### 클라이언트에서 REST API 사용하기

- getServersideProps나 getStaticProps함수 내에서 REST API를 호출하면 서버가 데이터를 가져오지만,
- 그 외의 컴포넌트 내에서 데이터를 불러오는 작업은 클라이언트가 실행합니다.
- 클라이언트는 주로 주로 두 가지 시점에 데이터를 불러옵니다.

1. 컴포넌트가 마운트된 후
2. 특정 이벤트가 발행한 후

- Next라고 해서 React와 다른 특별한 방법을 사용해야 할 필요는 없습니다.
- 브라우저의 내장 fetch API 혹은 Axios와 같은 외부 라이브러리를 사용해서 HTTP 요청을 보냅니다.

<br>

## 10주차 정리 (10.31)

## 디렉토리 구조 구성

- 애플리케이션의 코드를 쉽게 유지 보수하고 확장하려면 프로젝트의 디렉토리 구조는 간결해야 함

- Next.js에서는 특정 파일과 디렉토리가 지정된 위치에 있어야 함

- create-next-app을 명령으로 Next.js 애플리케이션을 처음 만들었을 때 디렉토리를 살펴보자

- next-js-app

  - node_modules/ : Next.js 프로젝트의 의존성 패키지를 설치하는 디렉토리

  - pakage.json

  - pages/ : 웹 애플리케이션의 페이지의 파일을 저장하고 라우팅 시스템을 만드는 디렉토리

  - public/ : 컴파일된 CSS 및 자바스크립트 파일, 이미지, 아이콘 등의 정적 자원을 저장하고 제공하는 디렉토리

  - styles/ : 스타일링 포맷(CSS, SASS, LESS 등)과 관계없이 스타일링 모듈을 저장하는 디렉토리

### 컴포넌트 구성

- 컴포넌트를 세 가지로 분류하고 각 컴포넌트와 관련된 스타일링 및 테스트 파일은 같은 곳에 두어야 함

- componets/ 디렉토리를 만들고 그 안에 추가 디렉토리를 만듬

- 코드를 더 효율 적으로 구성하기위해 사용함 아토믹 디자인 원칙에 따라 각 컴포넌트를 서로 다른 수준의 디렉토리를 둠

- 여기서는 컴포넌트를 다음과 같이 네 가지 종류로 나눔

#### atoms

- 코드에서 사용되는 가장 기본적인 컴포넌트임

- button, input, p와 같은 표준 HTML 요소를 감싸는 용도로 사용되거나 애니메이션 또는 컬러 팔레트 등과 같은 용도로 사용되는 컴포넌트를 이곳에 저정함

#### molecules

- atoms에 속한 컴포넌트 여러 개를 조합하여 좀 더 복잡한 구조를 만드는 컴포넌트들임

- 유틸리티 기능들은 많이 사용되지 않음

#### organisms

- molecules와 aoms를 섞어서 구조의 컴포넌트를 만듬

- 예를 들면 회원가입 양식이나 putter, carousel 등이 이에 속함

#### templates

- 일종의 페이지 스켈레톤으로 어디에 organims, atoms, molecules를 배치할지 결정해서 사용자가 접근할 수 이는 페이지를 만듬

- 아토믹 디자인에 관한 더 자세한 내용은 웹 사이트를 참고

### 유틸리티 구성

- 컴포넌트를 만들지 않는 코드 파일이 있는데이를 유틸리티 스크립트라고 함

- 다양한 목적으로 사용됨

- 이 구성은 하나의 기능이 여러 곳에서 사용될 때 사용되는 구성임

- 이 기능을 사용하는 모든 컴포넌트에 동일한 코드를 구현하는 대신 유틸리티 함수를 만들고 컴포넌트가 함수를 호출할 수 있도록 하는 것이 좋음

- 이런 유틸리티 함수는 utilty/ 디렉토리 아래에 저장하고 함수 각각 모적에 맞게 서로 다른 파일로 구분하는 것이 좋음

### 정적 자원 구성

- Next.js에서는 정적 파일을 쉽게 제공할 수 있음

- 제공할 파일은 public/ 디렉토리 아래에 두면 나머지는 프레임워크가 알아서 해주기 때운

- 정적 자원을 구성하기 전에 Next.js 애플리케이션ㅇ에서 어떤 정적 파일을 제공해야 할지 파악할 필요가 있음

- 다음은 일반적인 웹 사이트에서 사용되는 정적 자원임

  - 이미지
  - 컴파이한 자바스크립트 파일
  - 컴파일한 CSS 파일
  - 아이콘
  - manifest.jsom, robot.txt 등의 정적 파일

- public/ 디렉토리로 이동한 다음 assets/ 디렉토리를 만들고 그 아래에 정적 파일 유혈별로 디렉토리를 만듬

### 스타일 파일 구성

- 스타일 파일은 Next.js 애플리케이션에서 어떤 스타일 관련 기술을 사용하는가에 따라 그 구성이 달라짐

### lib 파일 구성

- lib파일은 third-party 라이브러리를 감싸는 스트립을 지칭하는 말임

- 유틸리티 스크립트는 범용이기 때문에 컴포넌트나 라이브러리에서 가져다 쓸 수 있지만 lib 파일은 특정 라이브러리에 특화건 것임

## 데이터 불러오기

- Next.js에서는 클라이언트와 서버 모두에서 데이터를 불러올 수 있음

- 서버는 두 가지 상황에서 데이터를 불러올 수 있음

- 정적 페이지를 만들 때 getStaticProps 함수를 사용해서 빌드 시점에 데이터를 불러올 수 있음

- 서버가 페이지를 렌더링할 때 getServerSideProps를 통해 실행 도중 데이터를 불러올 수 있음

### 서버가 데이터 불러오기

- Next.js에서는 서버가 내장 getStaticProps와 getServerSideProps 함수를 사용해서 데이터를 불러 올 수 있음

- Node.js는 웹 브라우저와 달리 자바스크립트 fetch API를 제공하지 않기 때문에 서버에서는두 가지 방법으로 HTTP요청을 만들고 처리해야 함

- 1. Node.js의 내장 HTTP 라이브러리를 사용할 수 있음

- 2. HTTP 클라이언트 라이브러리를 사용할 수 있음

## 9주차 정리 (10.23)

## 메타 데이터

- 페이스북의 오픈 그래프처럼 공유 자료를 카드 형태로 보내려면 몇가지 메타 데이터를 주 가해야 합니다
- Nextjs에서은 내장 Head 컴포넌트를 제공하여 이런 메타 데이터를 쉽게 다를 수 있습니다.
- 어떤 컴포넌트에서든 HTML페이지의 <Head> 내부 데이터를 변경, 추가, 삭제할 수 있습니 다.

다음은 index.js에 title 태그를 추가하는 코드입니다.

```jsx
export default function Home() {
  return (
    <>
      <Head>
        <title>이것은 index페이지입니다.</title>
      </Head>
      <Navbar></Navbar>
      <Widget pageName="index"></Widget>
    </>
  );
}
```

## 실습 1

```jsx
import React, { useState } from "react";
import Head from "next/head";

export default function Widget({ pageName }) {
  const [active, setActive] = useState(false);

  if (active) {
    return (
      <>
        <Head>
          <title>{pageName} false페이지 입니다.</title>
        </Head>
        <div>
          <button onClick={() => setActive(false)}>오리지널 타이틀</button>
          <br />
          타이틀을 확인하세요
        </div>
      </>
    );
  }
  return (
    <>
      <Head>
        <title>{pageName} true페이지 입니다.</title>
      </Head>
      <div>
        <button onClick={() => setActive(true)}>바뀐 페이지 타이틀</button>
      </div>
    </>
  );
}
```

- 버튼이 있는 컴포넌트를 만들고, 클릭하면 방문 페이지에 따라 페이지 title이 바뀌게 합니다.

## 실습 2

- HTMLS
  클라이언트에 보내기 전에 특정 작업을 처리해야 하는 경우는 pages/ 디렉토리
  안에 있는 \_app.js와 \_document.js 페이지를 이용합니다.

[_app.js 페이지]

Next 프로젝트를 생성하면 기본으로 다음과 같은 pages/\_appjs 파일이 생성됩니다.

```jsx
import "../styles/globals.css";
function MyAcp({ Component,page.Props}){
	return <Component { ,,,pagepropw).>;
}
export default myApp;
```

- 이 MyApp 컴포넌트와 그 속성인 pageProps를 반환합니다.
- 이에 앞서 제작한 Navbar 컴포넌트를 주가 하면 더 이상 index, about, contact 페이지에 Navbar 컴포넌트를 추가하지 않아도 됩니다.
- 이 뿐만 아니라 pages내의 모든 페이지에 적용 됩니다.

## 다크모드 설정

```jsx
import "@/styles/globals.css";

import { useState } from "react";
import ThemeContext from "@/components/ThemeContext";
import Navbar from "@/components/Navbar";

const themes = {
  dark: {
    background: "black",
    color: "white",
  },
  light: {
    background: "white",
    color: "black",
  },
};

export default function App({ Component, pageProps }) {
  const [theme, setTeme] = useState("light");
  const toggleTheme = () => {
    setTeme(theme === "dark" ? "light" : "dark");
  };
  return (
    <>
      <ThemeContext.Provider value={{ theme, toggleTheme }}>
        <div
          style={{
            width: "100%",
            minHeight: "100vh",
            ...themes[theme],
          }}
        >
          <Navbar></Navbar>
          <Component {...pageProps} />
        </div>
      </ThemeContext.Provider>
    </>
  );
}
```

## 7주차 정리 (10.9)

## 페이지에서 경로 매개변수 사용

```jsx
mport React from 'react'
import { useRouter } from 'next/router'

export async function getSeverSidePropsName({params}) {

  const {name} = params
  return {
    props:{
      name,
  },
}
}

export  default function Greet(props) {
  const {query} = useRouter();
  console.log(query)
  return (
  <h1>Hello {query.name}</h1>
  )
}
```

- 파일명은 [name].js로 해준다
- 내장 getSeverSidePropsName 함수를 통해 URL에서 동작하는 [name] 변수 값을 가져오는 것
- name/yun 주소로 가면 “Hello yun” 문구가 렌더링된다.

## 컴포넌트에서 경로 매개변수 사용

- pages 밖에서는 getSeverSideProps나 getStaticProps 함수를 사용하지 못한다
- useRouter 훅을 이용하면 컴포넌트 안에서 경로 매개변수를 사용할 수 있다.
- useRouter 훅을 사용해 query 매개 변수를 가져옵니다

## 클라이언트에서의 내비게이션

```jsx
import React from "react";
import Link from "next/link";

export default function Navbar() {
  return (
    <>
      <div>
        <Link href="/">Home</Link> |<Link href="/about">about</Link> |
        <Link href="/contact">contact</Link>
      </div>
    </>
  );
}
```

- Link 컴포넌트를 사용하여 서로 다른 페이지 간의 이동을 최적화 할 수 있음
- 다른 페이지 또는 웹 사이트의 일부를 연결할 때 LInk 컴포넌트를 사용합니다
- Link로 연결된 페이지는 이미 클라이언트에 다운로드된 상태이기 때문에 화면 전환 속도가 바쁨

## 동적 경로 매개 변수

- 중첩 라우팅으로 /blog/[date]/[slug].js 라는 페이지를 연결하는 경우 10버전 이후부터는 as 값을 href값처럼 사용하면 됩니다.

```jsx
<Link href="/blog/2000-04-01/happyhappy">Post</Link>
```

## 자동 이미지 최적화

```jsx
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  images: {
    domains: ["cdn.pixabay.com"],
  },
};

module.exports = nextConfig;
```

- 10 버전 이후부터 image 컴포넌트를 사용해서 이미지를 자동으로 최적화할 수 있습니다
- 먼저 next.config.js에 images 속성에 다음과 같이 서비스 호스팅명을 추가합니다
- 이렇게 설정해 두면 해당 도메인에서 가져오는 이미지는 자동으로 최적화 됩니다.

### layout 속성값

- fixed : 이미지의 크기를 지정하면 화면의 크기와 상관 없이 이미지 크기를 유지 합니다
- Responsive : fixed와 반대 방식으로 화면 크기를 조절하면 그에 따라 이미지를 최적화 해서 제공합니다
- Intrinsic : fixed와 Responsive를 절반씩 수용합니다. 크기가 작은 화면에서는 이미지 크기를 조절하고, 이미지보다 큰 화면에서는 이미지 크기를 조절하지 않습니다.
- fill : 부모 요소의 가로와 세로 크기에 따라 이미지를 늘립니다. fill을 사용할 경우 width와 height는 함께 사용할 수 없습니다.

<br>

## 10월 4일

### Page Project Layout - app

- app.jsx는 서버에 요청할 때 가장 먼저 실행되는 컴포넌트입니다.
- 페이지에 적용할 공통 레이아웃을 선언하는 곳입니다..
- 기본 코드는 다음과 같습니다

```js
import "@/styles/globals.css";
exprot default function App([Component, pageProps]) {
    return <Component (...pageProps)/>;
}
```

- Global CSS는 이곳에 추가됩니다.
- props 중 Component는 서버에 요청한 페이지입니다.
- pageProps는 App.getlnitialProps를 이용하여 prefetching된 데이터를 반환합니다.
- 데이터가 없다면 빈 객체를 반환합니다.
- 단, getStaticProps, getServerSideProps와 같은 Data Fetching methods는 동작하지 않습니다.

### Page Project Layout - document

- document.jsx는 app.jsx 다음에 실행됩니다.
- 각 페이지에서 공통적으로 사용될 html, head, body 안에 들어갈 내용을 선업합니다.
- onClick 같은 이벤트나 CSS는 이 곳에 선언하지 않습니다.
- 만일 로직이나 스타일이 필요하다면 app.jsx에 선언해야 합니다.
- 기본 코드는 다음과 같습니다.

```js
import {Html,Head,Main,NextScript} from "next/document"
exprot default function Document() {
    return(
        <Html lang="ko">
         <Head>
         </Head>
         <body>
         <Main/>
         <NextScript/>
         </body>
        </Html>
    )
}
```

### Page Project Layout - layout.jsx

- layout.jsx는 app 디렉토리 아래에 위치합니다.
- layout.jsx는 Page Project에서 사용하던 app.jsx와 document.jsx를 대체합니다.
- 이 파일은 삭제해도 프로젝트를 실행하면 자동으로 다시 생겨납니다.
- 프로젝트를 생성할 때 생성된 코드는 다음과 같습니다.

```js
export const metadata = {
    title: 'Next.js'
    description: 'Generated by Next.js',
}

export default function RootLayout({ children }) {
  return (
    <html lang="ko">
      <body className={inter.className}>{children}</body>
    </html>
  );
}

```

### Link vs a vs router.push

- Link component를 이용해서 Navibar componet를 만들어봅니다.
- `<a>` tag는 html 동기식으로 전체가 reload 되기 때문에, 외부 링크를 할 때 사용합니다.
- 일반적으로 내부 링크 이동시에는 사용하지 않는 것이 좋습니다.
- router.push는 빌드 후, 이동할 주소가 html 상에 노출되지 않기 때문에 SEO에 취약합니다.
- link 컴포넌트는 빌드 후, a tag로 자동 변환됩니다.
- a tag의 장점인 SEO 최적화, Prefetch 가능, 우 클릭 기능 등을 갖습니다.
- 내부 페이지로의 이동할 때 이 방식을 사용해야 SPA 방식으로 전체 html중 필요한 부분만 비동기식으로 리렌더링 된다.
- 따라서 특별한 경우가 아니면 link 컴포넌트 사용을 권장합니다.

### 정적 자원 제공

- 정적 자원은 이미지, 폰트, 아이콘, 컴파일한 css, js 등으로 /public 디렉토리 안에 저장합니다.
- 자세한 내용은 4장에서 다시 살펴봅니다.
- 정적 자원 중 이미지 파일은 SEO에 많은 영향을 미칩니다.
- 불러오는데 많은 시간이 걸리고, 불러온 후에도 이미지 주변의 레이아웃이 변경되는 등 ux관점에서 좋지 않은 영향을 줍니다.
- 이를 누적 레이아웃 이동(CLS)라고 합니다.
- 사용자가 2번째 문단을 읽고 있었다면, 위치가 바뀌어도 읽던 곳을 놓칠 수 있습니다.
- imagae 컴포넌트를 사용해서 이와 같은 CLS문제를 해결합니다.

### 자동 이미지 최적화

- Next.js 10부터 image 컴포넌트를 사용해서 이미지를 자동으로 최적화할 수 있습니다.
- 이 기능을 사용하면 이미지를 WebPage와 같은 최신 이미지 포맷으로 제공할 수 있습니다.
- 최신 포맷을 지원하지 않는 브라우저의 경우에는 png나 jpg와 같은 예전 이미지 포맷도 제공합니다.
- 필요한 경우 이미지 크기를 조정할 수도 있습니다.
- 특히 클라이언트가 이미지를 요구할 때 최적화 작업을 한다는 장점이 있습니다.
- 따라서 Unplash나 Pexel과 같은 외부 이미지 서비스로 이미지를 제공할 수 있습니다.
- 먼저 next.config.js의 images 속성에 다음과 같이 서비스 호스팅명을 추가합니다.

## 10월 2일

### 프로젝트 수업

## 9월 25일

### 프로젝트 수업

## 9월 11일

### 파이프라인 문법

```js
console.log(Math.random() * 10);

// 파이프라인 연산자를 사용하면 위 코드를 아래와 같이 바꿀 수 있습니다.

Math.random() |> (x) => x * 10 |> console.log;
```

- ECMAScript 내의 기술 위원회인 TC39에서 이 연산자를 공식적으로 채택하지는 않았지만 바벨 덕분에 사용할 수 있다.

- Next.js 앱에서 파이프라인 연산자를 사용하려면 npm으로 바벨 플러그인을 설치해야 한다.

### Transpile의 동작

- Babel

- ECMAScript 같은 js 최신 버전이나, TypeScript 이전 버전의 코드로 변환 시키는 Transpile 도구이다.

- AST(Abstract Syntax Tree)

- 소스 코드를 추상화된 트리 구조로 나타낸 것
- Babel의 parser는 js 코드를 컴퓨터가 이해하기 쉽게 변환해준다.

- 싱글 쓰레드로 실행되기 때문에 속도가 느리다는 단점

### SWC

- Next 12 이후 Babel에서 SWC로 교체되었다.

- SWC는 Rust로 작성되어 속도가 훨씬 빠르다

- ※ 속도가 빠른 이유는 Rust에는 WASM(WebAssembly)이라는게 있는데 이게 어셈블리어로 되어있다.(저급언어)

### 렌더링 전략

- 서버 사이드 렌더링(SSR)
- APM을 사용하는 웹 페이지 생성

- 자바스크립트 코드 적재되면 동적으로 페이지 내용을 렌더링한다.

- Next.js도 동적으로 페이지를 렌더링할 수 있다.

- 리액트 하이드레이션 :

- 서버에서 렌더링된 HTML 마크업에 기반하여 클라이언트 측에서 자바스크립트 이벤트와 상태를 연결하는 과정을 말한다.
- ### 장점

- 안전한 웹 애플리케이션 : 인증 또는 민감한 작업을 서버에서 수행하고 그 결과만 브라우저에 제공해 위협을 피할 수 있다.

- 뛰어난 웹 사이트 호환성 : 클라이언트 환경이 오래된 브라우저도 서비스를 제공한다.

- 뛰어난 SEO : 서버가 렌더링한 HTML을 받기에 웹 크롤러가 페이지를 렌더링할 필요가 없음

- ### 단점

- 페이지간의 이동은 CSR에 비해 느리다.

- 서버 과부하

- 깜빡임 이슈 (매번 새로고침 해야하기 때문에)

- SSR은 만능이 아니다.

- 단순히 서버가 SPA(Single Page App)를 렌더링한다고 모든 것이 해결되지 않음.
- 오히려 자바스크립트 코드를 증가시키며, 애플리케이션이 인터렉티브 할 때까지 걸리는 시간이 단순 클라이언트 렌더링보다 더 길어질 수 있다.
- 클라이언트 사이드 렌더링(CSR)
  실제 렌더링이 클라이언트에서 이루어지는 방식

- React 앱을 실행하면 렌더링 시작 전에 빈 화면이 한동안 유지 되는 것이 보임

- ### 장점

- 네이티브 앱처럼 느껴지는 웹 앱

- 전체 자바스크립트 번들을 다운로드 한다는 것은 렌더링할 모든 페이지가 이미 브라우저에 다운로드 되어 있다는 뜻

- 다른 페이지로 이동해도 서버에 요청할 필요 없이 바로 이동

- 페이지를 바꾸기 위해 새로 고침이 없다.

- ### 쉬운 페이지 전환

- 클라이언트에서 네비게이션이 새로고침이 발생하지 않아 UX에 도움이 된다.
  지연된 로딩과 성능

- 초기 로딩 이후 빠른 웹사이트 렌더링이 가능(웹사이트가 로딩되는 즉시 상호작용 가능)
- ### 단점

- 네크워크가 속도가 느린 환경에서는 번들이 모두 다운로드 될 때까지 빈 페이지를 보아야함

- 검색 로봇에게도 그 내용은 빈 것으로 보인다.

- 번들을 모두 받을 때까지 검색 로봇이 기다리기는 하지만 성능 점수는 낮다.

### 정적 사이트 생성(SSG)

- SSG는 일부 또는 전체 페이지를 빌드 시점에 미리 렌더링
  장점

- 쉬운 확장 : 정적 페이지는 HTML 파일으므로 CDN을 통해 파일을 제공하거나, 캐시에 저장하기 쉬움

- 뛰어난 성능 : 빌드 시점에 미리 렌더링하기 때문에 페이지를 요청해도 클라이언트나 서버가 무언가를 처리할 필요가 없음

- 더안전한 API 요청 : 외부 API를 호출하거나, DB에 접근하거나, 보호해야 할 데이터에 접근할 일이 없다. 필요한 모든 정보가 빌드 시 포함되어 있기 때문이다.

## 9월 4일

### 바벨과 웹팩 설정 커스터마이징

- 바벨이나 웹팩의 설정도 커스터마이징 할 수 있습니다.
- 바벨은 자바스크립트 트랜스컴파일러이며, 최신 자바스크립트 코드를 하위 호환성을 보장하는 스크립트 코드로 변환하는 일을 담당합니다.
- 하위 호환성이 보장되면 어떤 웹 브라우저에서든 자바스크립트 코드를 실행할 수 있습니다.
- 바벨을 사용하면 브라우저나 Node.js 등에서 지원하지 않는 새롭고 훌륭한 기능을 현재의 환경에서도 실행할 수 있습니다.
- 바벨 설정을 커스터마이징 하려면, 프로젝트 Root에 .babelrc라는 파일을 생성하면 됩니다.
- 이 설정 파일을 비워 두면 오류가 발생하기 때문에 최소한 다음 내용을 저장해야 합니다.

### 타입스크립트 지원

- Next.js는 타입스크립트로 작성되었기 때문에 고품질의 type definiton을 지원합니다.
- 기본 언어를 타입스크립트로 지정하려면 root에 tscoonfig.json이라는 설정파일 생성하면 됩니다.
- 그런 다음 `npm run dev` 명령을 실행하면 됩니다.

### 프로젝트의 기본 구조

- pages/ 디렉토리 안의 모든 js파일은 public 페이지가 됩니다.
- pages/ 의 Index.jsv 파일을 복사해서, about.js로 이름을 바꾸면, localhost:3000/about으로 접속할 수 있습니다.
- public/ 디렉토리에는 웹 사이트의 모든 퍼블릭 페이지와 정적 콘텐츠가 있습니다.
- styles/ 디렉토리에는 앱에서 사용하는 스타일시트 넣습니다.
- 용도가 정해져 있는 디렉토리는 pages/ 와 public 뿐입니다.
- 나머지 디렉토리는 필요에 따라서 다른 목적으로 사용하거나 삭제해도 됩니다.

### 프로젝트 생성 방법

- create-next-app을 이용하여 프로젝트를 생성해봅니다.
- `npx create-next-app<app-name>` -> `npx create-next-app@latest`
- Next 13.4 부터 라우터가 /src/pages에서 /src/app로 정식 변경
- 만일 pages를 사용하고 싶다면, App Router를 No라고 해주면 됩니다.
- 프로젝트가 생성되면 프로젝트 디렉토리로 이동하여 다음 명령을 실행합니다. npm run dev
- React처럼 바로 실행되지 않기 때문에 localhost:3000으로 접속하여 확인합니다. "Ctrl + 클릭"

### nvm의 주요 명령어

- 설치되어 있는 node 리스트 확인
- Node 설치 : install
  - nvm install 16.16.0 -> 16.16.0 버전 설치
  - nvm install latest -> latest current version 설치
  - nvm install lts
- Node 삭제 : uninstall
- 사용할 Node 버전 선택 : use
- 사용중인 버전 확인 : current
- 설치 가능한 node version 목록 확인 : list available

## 2024-09-04 강의 내용

### 프로젝트 생성 방법

`npx create-next-app<app-name>  => npx create-next-app`

1. 프로젝트의 기본구조

   - page/ 디렉토리 안의 모든 ks파일은 public 페이지가 됩니다.
   - public/ 디렉토리에는 웹 사이트의 모든 퍼블릭 페이지와 정적 콘텐츠가 있습니다.
   - styles/ 디렉토리에는 앱에서 사용하는 스타일시트를 넣습니다
   - 용도가 정해져 있는 디렉토리는 pages/ 와 public/뿐입니다.
   - 나머지 디렉토리는 필요에 따라서 다른 목적으로 사용하거나 삭제해도 됩니다.

2. 바벨과 웹팩 설정 커스터마이징
   - 바벨이나 웹팩의 설정도 커스터마이징 할 . 수있습니다.
   - 바벨은 자바스크립트 트랜스컴파일러이며, 최신 자바스크립트 코드를 하위 호환성을 보장하는 스크립트 코드로 변환하는 일을 담당합니다.
   - 하위 호환성이 보장되면 어떤 웹 브라우저에서든 자바스크립트 코드를 실행할 수 있습니다.
   - 바벨을 사용하면 브라우저나 Bode.js등에서 지원하지 않느 새롭고 훌륭한 기능을 현재의 한경에서도 실행할 수 있습니다.
   - 바벨 설정을 커스터마이징 하려면, 프로젝트 Root에 .babelrc라는 파일을 생성하면 됩니다.

## 8월 28일

### Page Router vs App Router

- React로 개발하다 처음 Next를 사용하면 제일 먼저 놀라는 기능이 Router 입니다.
- Next.js 13.4에서부터 App Router가 Stable하게 지원하기 시작했습니다.

#### [Page Router]

- pages 디렉토리가 root이고, index.js가 index page가 됩니다.
- about.js는 /about , team.js는 /team 경로로 라우팅 됩니다.
- 클라이언트 중심의 라우팅입니다.

#### [App Router]

- app 디렉토리가 root이고, page.js가 index page가 됩니다.
- /about/page.js는 /about, /login/page.js는 /page 경로로 라우팅 됩니다.
- 서버 중심의 라우팅입니다.
- 번들 사이즈가 작습니다.

### Next.js 13 vs 14

- Pages Router -> App Router
- Data Fetching : 13까지는 getServerSideProps, getStaticProps 메소드를 이용해서 구현 했으나, 14에서는 SSG(정적 사이트 생성), SSR(서버측 렌더링) 및 ISR(증분적 정적 재생성)에서 하나의 API만을 사용해서 구현할 수 있게 되었습니다.
- Tubopack : Rust 기반으로 개발된 새로운 번들러 사용으로 webpack보다 700배 빠르다고 발표했습니다.
- Tubopack은 3000개의 모듈이 있는 애플리케이션에서 1.8초 만에 부팅되고, Webpack은 16.5초, Vite는 11.4초가 걸립니다.

- 이미지 최적화 : 13까지는 도구를 사용하였으나, 14부터는 자체적으로 지원하기 시작했습니다.
- 보안 강화 : XSS 공격에 대한 보호 기능이 강화되고, 보안 관련 헤더 설정을 더욱 쉽게 만들었습니다.

### Next.js 알아보기

- Next.js는 리액트를 위해 만든 오픈소스 자바스크립트 웹 프레임워크 입니다.
- 리액트에는 없는 다양한 기능을 제공합니다.
  - 서버 사이드 렌더링(SSR: Server Side Rendering)
  - 정적 사이트 생성(SSG: Static Site Generation)
  - 증분 정적 재생성(ISR: Incremental Static Regenration)

<br>

`SSG(정적 페이지 생성)는 미리 만들어 놓은 페이지를 서비스 하기 때문에 속도는 빠르지만, 한번 생성하고 나면 수정이 불가능합니다. 이러한 단점을 보완하고자 나온 것이 ISR(증분 정적 재생성)입니다. 이미 생성된 페이지를 일정 시간이 지난 후에 다시 생성합니다. (최신 데이터로 업데이트)`

### [Chapter 1의 주요 내용]

- Next.js 소개 / 다른 프레임워크와의 비교 / 리액트와의 차이점
- 기본구조 타입스크립트를 사용하는 방법
- 바벨과 웹팩 설정 커스터 마이징 (Next.js 14는 Webpack에서 Tubopack으로 바뀜)

### 준비하기

- Node.js와 npm을 설치하거나 codesandbox.io 혹은 repl.it 등의 사이트를 이용합니다.
- 이 후 프로젝트별로 필요한 의존성 패키지를 npm으로 설치합니다.
- 잠시 확인을 위한 것이면 사이트를 이용해도 되지만, 그렇지 않은 경우라면 local에 환경을 설정하는 것이 좋습니다.

### Next.js란?

Angular, React, Vue 와 같은 프레임워크가 등장하면서 웹 개발 분야는 급속도로 변하기 시작

1. 리액트는 메타(페이스북)의 조던 발케가 만들어 2013년 오픈소를 발표합니다.
2. 리액트는 클라이언트 사이드(CSR)에서만 작동한다는 문제점이 있습니다.
3. 이 문제를 해결하기 위해 서버에서 미리 렌더링해 두는 방법을 연구하기 시작합니다.
4. 이러한 연구의 결과로 나온 것이 Next.js입니다.
5. 이 밖에 리액트가 제공하지 않는 여러가지 기능을 제공하게 됩니다.

#### [Next.js가 제공하는 새로운 기능들]

- 코드 분할 : 페이지를 로딩 할 때 번들을 여러 조각으로 나누어 필요한 부분만 전송
- 파일 기반 라우팅
- 경로 기반 프리페칭 : 사용자가 다음에 이동할 수 있는 페이지를 미리 가져오는 기술
- 서버 사이드 렌더링 : 페이지 요청이 올때마다 사전 렌더링
- 정적 사이트 생성 : 빌드하는 동안 페이지를 사전 생성
- 증분 정적 콘테츠 생성 : 배포 후에도 재 배포 없이 계속 업데이트
- 타입스크립트 기본 지원
- 자동 폴리필 적용 : 이전 브라우저에서 최신 기능을 제공하는데 필요한 코드를 제공
- 이미지 최적화 : Next/image 컴포넌트 제공하는 이미지의 최적화 기술(lazy loading-지연, 이미지 사이즈 최적화- webp 변환, Placeholder-영역 확보)
- 웹 애플리케이션의 국제화 지원 : 다국어 지원(local에 맞는 URL로 라우팅)
- Next.js는 현재 넷플릭스, 트위치, 틱톡, 나이키 등 사이트에서 사용 중입니다.

### Next.js와 비슷한 프레임워크

#### [Gatsby]

- 정적 웹 사이트를 만들 수 있는 프레임워크 입니다.
- 정적 사이트 생성만 지원합니다.
- 클라이언트 사이드 렌더링만 지원합니다.
- 동적으로 변하는 복잡한 웹 사이트는 만들 수 없습니다.

#### [Razzle]

- 서버 사이드 렌더링이 가능한 자바스크립트 애플리케이션 개발이 가능합니다.
- CRA와 유사하게 프로젝트를 구성할 수 있다는 장점이 있습니다.
- React, Preact, Reason-React, Angular 및 Vue 와 함께 사용할 수 있습니다.

#### [Nuxt.js]

- Vue를 사용한 웹 애플리케이션 개발에서 리액트의 Next.js에 해당하는 프레임워크입니다.
- Nuxt.js나 Next.js 모두 같은 목표를 갖는 프레임워크지만 Nuxt.js는 더 많은 설정이 필요합니다.
- 만약 Vue 개발자가 서버 사이드 렌더링이 필요하다면 Nuxt.js를 사용해 보는 것도 추천합니다.

#### [Angular Universal]

- 정적 사이트 생성과 서버 사이드 렌더링을 지원합니다.
- Nuxt나 Next와는 달리 대기업인 구글에서 만들었습니다.
- Angular로 개발하는 경우 Angular Universal을 사용하는 것이 대부분입니다.

**2024**
![alt text](images/stackover.png)

### 왜 Next.js 일까?

- React에서 제공하지 않는 여러 기능을 지원합니다.
- 설정이나 개발 옵션 등 다양한 부분에서도 유용한 기능들을 제공합니다.

### 리액트에서 Next.js로

- Next.js의 기본 철학은 React와 거의 같습니다.
- 설정보다 관습 이라는 리택트의 철학을 계승합니다.
- CoC : Convention over Configuration은 개발자가 해야 할 결정의 수를 줄여주면서도, 유연성은 잃지 않도록 하는 소프트웨어 설계 패러다임입니다.
- 반면 fs, child_process와 같이 Node.js에서만 사용할 수 있는 라이브러리나 API를 사용하려는 경우, 각 요청 별 데이터를 클라이언트로 보내기 전에 서버 사이드 코드를 실행하거나 페이지 생성 시점에 해당 코드를 처리하는 방식을 지원합니다.

  - 어떤 방식으로 지원하는지는 각 페이지가 어떤 렌더링 방식을 사용하는가에 따라 결정됩니다.

- 클라이언트 사이드 앱, 프로그레시브 웹 앱, 오프라인 웹 앱도 쉽게 만들 수 있습니다.
- 많은 내장 컴포넌트와 최적화 기능을 사용할 수 있다는 장점이 있습니다.

### Next.js 시작하기

- 새로운 앱을 만들고 웹팩과 바벨의 기본 설정을 커스터마이징 해봅니다.
- Next.js 앱을 만들 때 기본 언어로 타입스크립트를 사용하는 방법을 알아 봅니다.
- Typescirpt는 이번학기 수강하기 때문에, 이 강의는 js로 진행합니다.
- 개발 환경에는 Node.js npm만 설치하면 됩니다.
- Node.js만 설치하면 npm은 함께 설치됩니다.
- 설치 되어 있는지 확인하려면 버전을 확인해 봅니다.
- 이번 학기에는 v22.7.0 버전으로 진행합니다.
- 만일 다른 버전을 이미 사용하고 있다면 그대로 사용해도 됩니다.
- 사용 중 의존성에 문제가 있다고 판단될 때 변경하면 됩니다.
