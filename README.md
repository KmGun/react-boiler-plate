## Directory structure

- src - 개발한 모든 소스가 존재한다.
  - assets : 정적 리소스, img, 웹폰트등
  - components : 컴포넌트들이 위치한다.
    - atoms : Button.tsx, Input.tsx 등 가장 작은 component단위들 저장
      - styled component가 아닌 css 를 활용할거면 폴더단위로 저장 : ex. Button 폴더 내 Button.tsx , Button.css
    - molecules : TopBanner , NavBar 등 atom들이 모인 단위
    - organisms :
    - pages : Router.tsx , 각 Route 별 페이지
      - Route 별 페이지는 routeName/subRoute.tsx 방식으로 관리한다.
        - ex. auth/register : auth/Register.tsx
  - lib : 전역 스타일, 커스텀 훅, api, util등이 위치한다.
    - api.ts : API와의 통신 관련 AJAX 로직
    - util : 특수한 기능 하는 함수 등
      - ex. function beDataToFeData
  - store : 상태관리 관련 코드들
    - atoms.ts : recoil atom관련 코드들
  - app - 어플리케이션 entry로 라우팅이나 기타 리소스들을 관리한다.
  - index - 프로그램 entry로 리액트 시작점.
  - etc : 기타

## naming

- 기본 작명 규칙
  - 명사 + 동사인 경우 : 동사 → 명사 순으로
    ```tsx
    function getGoogleId() {}
    ```
- PascalCase : 컴포넌트 파일명, 컴포넌트, styled-component, interface, type

  ```tsx
  // Modal.tsx
  function Modal(){

  }

  ...
  <Modal/>
  ...

  interface IComponentProps {

  }

  type TIdType {

  }
  ```

- camelCase : 그외 모두(변수명, 함수명, prop 등)
- Typescript
  - **interface, type은 기본적으로 파일 가장 위에 정의**
  - 객체는 전부 interface 사용
  - interface : I + PascalCase
  - Type : T + PascalCase
- etc

  - 폴더명 : PascalCase
  - recoil atom :
    ```tsx
    export const userInfoDataAtom = atom<IuserInfoData>({
      key: "userInfoData",
      default: {} as any,
      effects_UNSTABLE: [persistAtom],
    });
    ```
  - api.ts
    - 아래와 같은 형식으로 작성
    - 작명 : fetch + 요청종류 + PascalCase
    ```tsx
    export function fetchGetGoogleId() {
      return axios
        .get<{ googleId: string }>(`/api/get-google-id`, {
          withCredentials: true,
        })
        .then((res) => res.data);
    }
    ```
  - Event Handler
    → 이벤트 핸들러를 받는 prop 이름은 `on___`으로 짓고, 이벤트 함수 이름은 `handle___`로 짓는다.

    ```tsx
    const handleClickSearchButton = function(){

    }
    ...
    return (
    	<SearchButton onClick={handleClickSearchButton} />
    )
    ```

  - Custom Hook
    → Custom Hook 이름은 `use___` 로 지정

## javascript

- 중괄호는 생략하지 X

  ```tsx
  if ( ) {
    ...
  } else if ( ) {
    ...
  } else {
    ...
  }

  function functionName() {
    ...
  }
  ```

- 함수 : 익명함수는 arrow function, 이름 있는 함수는 function으로

  ```tsx
  useQuery("queryName", () => {
    getData;
  });

  function Modal() {}
  ```

- 함수 parameter 기본값은 ES6 사용

## React

- 폴더 구조
- .tsx 파일 기본 구조

  - component의 경우 export default로 하는것 주의

    ```tsx
    // FunctionComponent.tsx

    const Wrapper = styled.div`

    `

    interface IModal = {
      ...
    }

    function Modal({ ... }: IModal) {
      ...
    }

    export default FunctionComponent
    ```

  - Styled Components
    - 컴포넌트 파일 안에 정의, Import하는건 지양
  - State Management
    - 전역 상태 관리는 recoil활용한다.
    - 되도록이면, 전역상태는 사용하지 않도록 한다

- 참고 자료
  [React 코딩 규칙](https://velog.io/@gwak2837/React-%EC%BD%94%EB%94%A9-%EA%B7%9C%EC%B9%99)
  [[react] react 코딩 컨벤션](https://phrygia.github.io/react/2022-04-05-react/)
  [React 아키텍쳐, 디자인 시스템, 파일 구조에 대한 고찰](https://kyung-a.tistory.com/35)
  [Atomic Design으로 Todo 만들기](https://velog.io/@thsoon/%EC%93%B8%EB%95%8C%EC%97%86%EC%9D%B4-%EA%B3%A0%ED%80%84%EC%9D%B8-%ED%88%AC%EB%91%90%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0-FE-2.-%EB%B7%B0-%EC%84%A4%EA%B3%84)
