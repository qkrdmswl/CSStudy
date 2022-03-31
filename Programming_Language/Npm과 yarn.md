# NPM 과 Yarn

## Npm
: Node Package Manager의 약자로 자바스크립트 언어를 위한 패키지 관리자를 의미한다. (이때 package = npm에 업로드된 js module을 의미)
### Package.json
- 프로젝트의 정보와 의존성을 관리하는 파일이다.
- 어떤 패키지와 버전을 사용하는지 기록하여 어느 곳에서든 동일한 개발환경을 구축할 수 있게한다.
- 직접 수정하는 대신 CLI를 통해 추가, 삭제, 업데이트하는 것을 추천한다
- `dependencies`에 의존 패키지들이 정의된다
- 버전 표기 방식(SemVer)
  |범위표기기호|설명|예시|버전 범위|
  |-----------|---|--------|-----|
  | |버전 표기와 같은 버전에서 자동 업데이트가 진행되지 않는다| 0.0.1|=0.0.1|
  |~|버전표기 규칙중 마지막 자리(patch버전)에서만 자동 업데이트|~0.0.1|>=0.0.1 and <0.1.0|
  |~|버전표기 규칙중 마지막 자리(patch버전)에서만 자동 업데이트|~0.1.1|>=0.1.1 and <0.2.0|
  |^|버전표기 규칙중 두번째 자리(minor버전)에서만 자동 업데이트|^1.0.2|>=1.0.2 and <2.0|
  |^|버전표기 규칙중 두번째 자리(minor버전)에서만 자동 업데이트|^1.0|>=1.0.0 and <2.0|
  |^|버전표기 규칙중 두번째 자리(minor버전)에서만 자동 업데이트|^1|>=1.0.0 and <2.0|

  [SemVer에 대한 자세한 내용은 해당 링크에서 확인](https://codingjerk-diary.tistory.com/entry/semVer-semVer%EB%B0%A9%EC%8B%9D%EC%9D%98-%EB%B2%84%EC%A0%84-%EB%84%98%EB%B2%84%EB%A7%81)

### 장점
- 간단한 명령어로 자바스크립트 모듈을 설치하고 버전을 관리할 수 있다. (npm없이 모듈을 직접설치할 경우 의존성이 있는 모듈의 설치 및 버전 문제가 있어 번거롭다.)

### 한계
- npm 저장소의 취약한 보안 이슈
- 의존 패키지의 버저닝 이슈
- 패키지가 많아질수록 빌드 성능의 감소

<hr>

## Yarn
: 거대해지는 프로젝트에서 npm의 성능, 보안적 문제를 겪은 페이스북이 만든 자바스크립트 패키지 매니저

### yarn.lock
- yarn은 package.json에 정의된 버전의 범위에 따라 패키지를 관리하지만, 이는 시스템마다 yarn install이 되는 시점에 따라 패키지 버전이 다를 수 있음을 의미한다. 이 문제를 해결하고자 `시스템 간에 일관적으로 패키지 버전을 제공하기 위해` yarn.lock파일을 프로젝트의 루트에 자동으로 생성하여 사용한다.
- yarn cli를 통해 패키지를 관리하면 자동으로 업데이트된다.
- 사용자는 이 파일을 `절대로 직접 수정해서는 안된다.`
- package.json과 yarn.lock은 Version control 시스템과 긴밀하게 연결되어야한다.
 
### 장점
-  npm에 비해 속도, 안정성이 높다 (하지만 npm@5이후로 npm도 안정적이고 성능적으로도 향상이 있었기에 필요에 따라 사용하면 된다)

<hr>

## NPM vs. yarn
### 성능
   #### 속도 (Performance)
   - npm은 패키지 설치를 순차적으로 진행하는 반면 yarn은 `병렬적으로 처리`하여 설치속도가 더 빠르다
   - npm은 종속된 패키지 중 중복된 패키지가 있어도 이를 다운로드 하는 반면에, yarn은 `중복된 데이터는 다운로드하지 않는다`
   - 성능 비교
     ![image](https://user-images.githubusercontent.com/48820696/160969838-752d47d8-5dbf-4325-a9b7-ed8df8a5bc23.png)

   
   #### 안정성, 보안성 (Security)
   - yarn이 사용하는 yarn.lock은 yarn cli를 통해서만 수정이 권장되며, yarn.lock이 package.json과 일치하지 않는 상태라면 install 명령으로 패키지가 업데이트 되고 package.json을 만족하기 위해 필요한 만큼 수정된다. 떄문에 디바이스마다 버전이 다른 패키지가 설치되는 npm의 문제를 해결되며 버전의 안전성이 보장된다.

### 코드
|명령어	|npm	|yarn|
|------|----|-----|
|dependencies 설치	|npm install	|yarn|
|패키지 설치	|npm install [패키지명]	|yarn add [패키지명]|
|dev 패키지 설치	|npm install --save-dev [패키지명]	|yarn add --dev [패키지명]|
|글로벌 패키지 설치	|npm install --global [패키지명]	|yarn global add [패키지명]|
|패키지 제거	|npm uninstall [패키지명]	|yarn remove [패키지명]|
|dev 패키지 제거	|npm uninstall --save-dev [패키지명]	|yarn remove [패키지명]|
|글로벌 패키지 제거	|npm uninstall --global [패키지명]	|yarn global remove [패키지명]||
|업데이트	|npm update	|yarn upgrade|
|패키지 업데이트|npm update [패키지명]	|yarn upgrade [패키지명]|

    

# Reference
- [Yarn 톺아보기](https://www.holaxprogramming.com/2017/12/21/node-yarn-tutorials/)
- [Codingjerk tistory(본인 블로그입니다)](https://codingjerk-diary.tistory.com/entry/semVer-semVer%EB%B0%A9%EC%8B%9D%EC%9D%98-%EB%B2%84%EC%A0%84-%EB%84%98%EB%B2%84%EB%A7%81)
- [joshua1988.github](https://joshua1988.github.io/vue-camp/package-manager/npm-vs-yarn.html#npm%E1%84%80%E1%85%AA-yarn%E1%84%8B%E1%85%B4-%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%A5%E1%86%B7)
