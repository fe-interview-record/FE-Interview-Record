# CSR과 SSR의 차이점에 대해 설명해주세요.

## CSR이란 

Client Side Rendering이란 클라이언트 영역에서 렌더링을 수행하는 방식이다.

사용자가 웹 브라우저를 통해서 웹사이트를 방문했을 때 웹페이지에 대한 리소스들을 클라이언트 단에서 다운로드 받고 
클라이언트 사이드에서 페이지 전환을 처리하여 보여주는 방식이다.

### CSR 동작 원리

1. 초기 요청 : 사용자가 홈페이지를 최초 접속한 경우 클라이언트는 이를 확인하고 서버로 HTML을 요청한다.
   서버는 클라이언트에게 필요한 Javascript 및 CSS 파일이 포함된 최소한의 HTML을 보낸다.
   이 때 서버에서 보내주는 초기 HTML파일에는 정보가 거의 없는 형태
   해당 HTML파일에는 스크립트 태그에 자바스크립트 파일만 링크되어 있고 화면을 실제 구성하는 요소가 없다.

2. 리소스 다운로드 : 브라우저는 서버로부터 받은 정적 리소스를 다운로드하고, JavaScript를 실행하기 시작

3. 앱 초기화: 다운로드된 JavaScript 내에서 정의된 웹 애플리케이션 로직에 따라 애플리케이션이 초기화 
   이 단계에서 라우팅 설정, 상태 관리 등 앱을 구동하기 위한 필수 작업이 이루어진다.

4. 콘텐츠 렌더링 : 초기화 과정에서 설정된 라우트에 따라 해당하는 뷰가 브라우저에 렌더링된다. 
   이때 필요한 데이터가 있다면, AJAX를 통해 비동기적으로 서버로부터 데이터를 요청하고, 받아온 데이터를 바탕으로 화면에 콘텐츠를 동적으로 생성

   사용자가 링크를 클릭하거나 어떠한 액션을 취할 때, 페이지 전체를 새로 고치는 대신 필요한 데이터만 서버로부터 비동기적으로 요청하고, 받아온 데이터로 화면을 업데이트

## SSR이란

Server Side Rendering이란 서버 영역에서 렌더링 과정을 수행하는 방식이다.

사용자가 웹페이지에 방문해서 접속하면 서버로 해당 페이지에 대한 요청이 진행되고,
서버에서는 필요한 HTML,CSS,Javascript를 이용해서 페이지를 렌더링하여 클라이언트로 보내주게 된다.
서버단에서 완전한 html파일을 직접 만들어서 제공

### SSR 동작 원리

1. 사용자가 브라우저를 통해 특정 URL에 접근하여 웹 페이지를 요청한다.

2. 서버는 해당 요청을 받고, 요청된 페이지에 필요한 데이터를 데이터베이스나 API 등으로부터 조회

3. HTML 생성: 서버는 조회한 데이터를 바탕으로 HTML 문서를 동적으로 생성합니다. 이 과정에서 서버는 해당 웹 페이지의 구조, 스타일, 내용을 포함한 완전한 HTML 문서를 만든다.

4. HTML 응답: 생성된 HTML 문서는 HTTP 응답의 일부로 클라이언트에게 전송됩니다. 이때, CSS와 JavaScript 파일 등의 정적 자원에 대한 참조도 함께 전송

5. 브라우저 렌더링: 클라이언트(브라우저)는 받은 HTML 문서를 해석하여 웹 페이지를 렌더링

# CSR, SSR의 차이

CSR, SSR의 가장 큰 차이점은 콘텐츠 렌더링이 발생하는 위치이다.

CSR에서는 브라우저(클라이언트)에서 대부분의 렌더링 작업이 이루어진다.
서버로부터 초기 로드시 받는 HTML은 비어 있거나 최소한의 구조만 가지며, 자바스크립트를 통해 동적으로 콘텐츠를 생성하고 페이지를 구성한다.

SSR에서는 서버에서 사용자의 요청에 따라 HTML 페이지를 완전히 구성하여 클라이언트로 전송한다.
이 방식에서 사용자는 서버로부터 완성된 HTML 페이지를 받아, 추가적인 처리 없이 바로 볼 수 있다.

이 차이는 웹 애플리케이션의 초기 로딩 시간, 검색 엔진 최적화(SEO), 서버 부하, 사용자 경험 등 여러 측면에 영향을 미친다.
