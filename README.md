## 개요
![deploy drawio](https://github.com/user-attachments/assets/caceec84-ebb5-43b1-82c9-e93ba6295717)

GitHub Actions에 워크플로우를 작성해 다음과 같이 배포가 진행되도록 합니다.

1. 저장소를 체크아웃합니다.
2. Node.js 18.x 버전을 설정합니다.
3. 프로젝트 의존성을 설치합니다.
4. Next.js 프로젝트를 빌드합니다.
5. AWS 자격 증명을 구성합니다.
6. 빌드된 파일을 S3 버킷에 동기화합니다.
7. CloudFront 캐시를 무효화합니다.

## 주요 링크

- S3 버킷 웹사이트 엔드포인트: http://hanghae-chapter4.s3-website.ap-northeast-2.amazonaws.com/
- CloudFrount 배포 도메인 이름: https://d9ki7wmurfuc6.cloudfront.net/

## 주요 개념

- GitHub Actions과 CI/CD 도구: _________
- S3와 스토리지: _________
- CloudFront와 CDN: _________
- 캐시 무효화(Cache Invalidation): _________
- Repository secret과 환경변수: _________

## CDN과 성능최적화
|s3|cloudfront|
|------|---|
|<img width="765" alt="image" src="https://github.com/user-attachments/assets/18370c7d-7140-41d8-8faf-7836fb84fb23">|<img width="687" alt="image" src="https://github.com/user-attachments/assets/1eb1d28e-761a-413b-b724-227ad544cbd6">|


