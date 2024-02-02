# mybatis 캐싱 처리

## 캐싱 처리 종류
- Local Session Cache(무조건 활성화)
- Second Level Cache(선택적 사용 가능)

## Local Session Cache
- sqlSession 객체마다 갖고 있는 Cache
- 개발자 임의로 비활성 불가능

## Second Level Cache