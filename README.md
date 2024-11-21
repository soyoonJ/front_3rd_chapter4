## 개요
![deploy drawio](https://github.com/user-attachments/assets/caceec84-ebb5-43b1-82c9-e93ba6295717)

GitHub Actions에 deployment.yml 워크플로우를 작성하여, main 브랜치에 push될 때 다음과 같은 단계로 배포가 진행됩니다.

1. 저장소를 체크아웃합니다.
2. Node.js 18.x 버전을 설정합니다.
3. npm ci로 프로젝트 의존성을 설치합니다.
4. Next.js 프로젝트를 빌드합니다.
5. AWS 자격 증명을 구성합니다.
6. 빌드된 파일을 S3 버킷에 동기화합니다.
7. CloudFront 캐시를 무효화합니다.

## 주요 링크

- S3 버킷 웹사이트 엔드포인트: http://hanghae-chapter4.s3-website.ap-northeast-2.amazonaws.com/
- CloudFrount 배포 도메인 이름: https://d9ki7wmurfuc6.cloudfront.net/

## 주요 개념

- GitHub Actions과 CI/CD 도구
  - CI/CD는 각각 지속적 통합과 지속적 배포를 의미한다.
  - Github Actions과 같은 자동화 도구를 사용할 경우 push, pr 등의 이벤트 발생 시 린트체크, 테스트, 빌드, 배포 등을 실행할 수 있다.
  - 워크플로우를 작성하여 환경을 세팅하고, 일부 action의 경우 Github 세팅에 등록해둔 secrets를 연결하여 배포를 진행할 수도 있다.
  - 이번 프로젝트의 경우 main 브랜치에 push 되었을 때 Action이 구동되고 있다.
- S3와 스토리지
  - S3는 AWS에서 제공하는 객체 스토리지 서비스이며 정적 웹사이트 호스팅에도 사용된다.
  - 이번 프로젝트에서는 Next.js 프로젝트의 정적 호스팅을 위해 사용했지만, 저장소의 역할을 하기 때문에 파일/이미지 등을 저장하는 용도로도 사용될 수 있다.
- CloudFront와 CDN
  - CDN은 Content Delivery Network의 약자로 웹 컨텐츠를 사용자와 가까운 곳에서 전달할 수 있게 해준다.
  - CloudFront는 AWS에서 제공하는 CDN 서비스이다.
- 캐시 무효화(Cache Invalidation)
  - 이번 프로젝트에서 CloudFront는 기본적으로 S3의 리소스를 캐시하여 관리하고 있는데, 업데이트 되었는데도 캐시를 유지할 경우 사용자에게 잘못된 정보를 보여줄 수 있다.
  - 때문에 컨텐츠를 무효화하여 강제로 최신 버전으로 업데이트 하는 방식으로 업데이트를 진행해줄 수 있다.
  - 현재는 deployment.yml에서 무효화 경로를 /*로 설정하여 전체 경로에 대해 무효화되게끔 설정하였다.
- Repository secret과 환경변수
  - key value 형태로 저장되며 Environment Variable과 비슷하게 동작하지만 외부로는 공개되지 않기 때문에, AWS 키와 같이 보안이 필요한 정보들을 저장하는데에 사용한다.

## CDN과 성능최적화
S3에만 호스팅했을 때 로드까지 293ms가 소요되었는데에 반해 CloudFront를 거치며 152ms로 시간이 약 51% 감소하며 성능이 개선됨
|S3|cloudfront|
|------|---|
|<img width="765" alt="image" src="https://github.com/user-attachments/assets/18370c7d-7140-41d8-8faf-7836fb84fb23">|<img width="687" alt="image" src="https://github.com/user-attachments/assets/1eb1d28e-761a-413b-b724-227ad544cbd6">|


