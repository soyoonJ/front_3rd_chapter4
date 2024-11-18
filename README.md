## 개요
![deploy drawio](https://github.com/user-attachments/assets/caceec84-ebb5-43b1-82c9-e93ba6295717)

GitHub Actions에 deployment.yml 워크플로우를 작성해 다음과 같은 단계로 배포가 진행되도록 합니다.

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

- GitHub Actions과 CI/CD 도구: Github Actions과 같은 자동화 도구를 사용할 경우 push, pr 등의 이벤트 발생 시 린트체크, 테스트, 빌드, 배포 등을 실행할 수 있다.
- S3와 스토리지: S3는 AWS에서 제공하는 객체 스토리지 서비스이며 정적 웹사이트 호스팅에도 사용된다.
- CloudFront와 CDN: CDN은 Content Delivery Network의 약자로 웹 컨텐츠를 사용자와 가까운 곳에서 전달할 수 있게 해준다. CloudFront는 AWS에서 제공하는 CDN 서비스이다.
- 캐시 무효화(Cache Invalidation): CloudFront에서 캐시된 컨텐츠를 무효화하여 강제로 최신 버전으로 업데이트 한다.
- Repository secret과 환경변수: key value 형태로 저장되며 Environment Variable과 비슷하게 동작하지만 외부로는 공개되지 않기 때문에, AWS 키와 같이 보안이 필요한 정보들을 저장하는데에 사용한다.

## CDN과 성능최적화
|s3|cloudfront|
|------|---|
|<img width="765" alt="image" src="https://github.com/user-attachments/assets/18370c7d-7140-41d8-8faf-7836fb84fb23">|<img width="687" alt="image" src="https://github.com/user-attachments/assets/1eb1d28e-761a-413b-b724-227ad544cbd6">|


