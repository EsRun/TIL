# 캐싱 처리 방법

## 어노테이션
- @EnableCaching : 캐시 활성화, 캐시 매니저 설정 가능
- @CacheConfig : 캐시를 클래스 단위로 사용하고 관리
- @Cacheable : 설정된 키를 이용해 캐시 저장 / 조회, 동일한 키일 경우 캐싱된 데이터 리턴
- @CachePut : 캐시 키 저장 및 갱신
- @CacheEvict : 캐시 정보 삭제
- @Caching : 여러개 캐시 어노테이션을 사용할 때 사용(예. cacheable = @Cacheable(...), evict = @CacheEvict(...))

## 중요
- 캐싱 처리를 하기 위해선 하나의 프로젝트에서 모든 C.R.U.D 가 이루어져야하고, 작업 시 캐싱 처리가 되어야 한다.
- DB 데이터를 외부 프로젝트에서 했을 경우 캐싱 처리 유무를 확인할 수 없으므로(insert를 별도의 api에서 했을 경우) 
- @CacheAble은 동일한 데이터만 출력하게 된다. 실제로는 DB 결과값이 바뀌었지만 캐시에는 키가 갱신 되었다는 정보가 없기 때문이다.

## Cacheable(캐시 등록)
- cacheName(공통) : 저장할 캐시 이름
- key(공통) : 캐시를 구분할 키(사용할 메소드의 파라미터도 넣을 수 있다. 예) @Cacleable(key="'상수'") 또는 @Cacleable(key="'#파라미터 변수'"))
- value(공통) : cacheName의 alias
- condition(공통) : or, and 및 논리연산 가능
- unless : true 일 경우에만 캐싱하지 않음
- cacheManager(공통) : 사용할 CacheManager 설정
- sync : 여러 쓰레드가 동일한 키를 사용할 경우, 호출을 동기화한다. 
```html
    @Cacheable(cacheNames = "mobile", key="'#userId' + #type'")
    public Phone getManufacturing(String userId, int type){}

    @Cacheable(cacheNames = "mobile", condition = "'#user.compnay == samsung'")
    public Phone getPhone(User user){}

    @Cacheable(cacheNames = "mobile", unless="'#user.compnay == apple'")
    public Phone getPhone(User user){}
```

## CacleEvict(캐시 삭제)
- allEntries : 캐시 내 모든 데이터를 삭제할지 여부
- beforeInvocation : 메소드 수행 전 캐시 데이터 삭제(true), 메소드 수행 후 캐시 데이터 삭제(false)
## CachePut(캐시 저장)
- Cacheable과 동일
## Cacheable / CachePut 차이점
- Cacheable : 캐시에 값이 있을 경우 메소드를 실행하지 않고 캐시된 값 반환
- CachePut : 캐시 값 유무와 상관없이 무조건 메소드를 실행하고 결과값을 캐시에 저장
## Caching
- cacheable : @Cacheable array 이름
- evict : @CacheEvict array 이름
- put : @Cacheput array 이름

## 구현 코드
```hmtl
    @EnableCaching
    @Configuration
    public class cacheConfig {
        
        @Bean
        public CacheManager cacheManager() {
            ConcurrentMapCacheManager cacheManager = new ConcurrentMapCacheManager();
            cacheManager.setAllowNullValues(false);
            cacheManager.setCacheNames(Arrays.asList("fruit", "mobile", "department"));
            return cacheManager;
        }
        
    }
```

```html
    @Service
    @CacheConfig(cacheNames = "fruit")
    public class fruitService{
        private final fruitMapper mapper;

        public fruitService(fruitMapper mapper){
            this.mapper = mapper;
        }

        @Cacheable(key = "'#idx'")
        public List<Map<String, Object>> getFruitList(int idx) throws Exception{
            return mapper.getFruitList(idx);
        }

        @CachePut(key = "'#idx'")
        @CacheEvict(key = "'#idx'")
        public List<Map<String, Object>> updateFruit(int idx) throws Exception{
            return mapper.updateFruit(idx);
        }
    }
```

### 캐시 매니저 종류
#### 메모리 상에 저장
- ConcurrentMapCacheManager : ConcurrentHashMap 기반 캐시 구현체
- CaffeineCacheManager : Caffeine 기반 캐시 구현체
- SimpleCacheManager : 단순 캐시 구현체
- HazelcastCacheManager : Hazelcast 기반 캐시 구현체
- InfinispanCacheManager : Infinispan 기반 캐시 구현체
#### 디스크 또는 데이터베이스에 저장
- EhCacheCacheManager : Ehcache 기반 캐시 구현체
#### 자체 저장소에 저장
- GemfireCacheManager : Gemfire 기반 캐시 구현체
- CoherenceCacheManager : Oracle Coherence 기반 캐시 구현체
#### Redis 내 저장
- RedisCacheManager : Redis 기반 캐시 구현체
#### Couchbase 내 저장
- CouchbaseCacheManager : Couchbase 기반 캐시 구현체