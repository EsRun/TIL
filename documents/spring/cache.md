# 캐싱 처리 방법

## 어노테이션
- @EnableCaching : 캐시 활성화
- @CacheConfig : 캐시를 클래스 단위로 설정
- @Cacheable : 설정된 키를 이용해 캐시 저장 / 조회, 동일한 키일 경우 캐싱된 데이터 리턴
- @CachePut : 캐시 키 저장 및 갱신
- @CacheEvict : 캐시 정보 삭제
- @Caching : 여러개 캐시 어노테이션을 사용할 때 사용(예. cacheable = @Cacheable(...), evict = @CacheEvict(...))

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