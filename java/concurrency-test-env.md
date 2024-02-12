# 동시성 테스트를 위한 코드

### 동시에 100명의 유저가 처리하는 테스트 환경 설정
``` java
int threadCount = 100;
ExecutorService executorService = Executors.newFixedThreadPool(25);
CountDownLatch latch = new CountDownLatch(threadCount);

for (int i = 0; i < threadCount; i++) {
    executorService.submit(() -> {
        try {
            // 처리 코드
        } finally {
            latch.countDown();
        }
    });
}

latch.await();
```
- ExecutorService 클래스를 사용해 간단하게 쓰레드 풀을 생성하여 병렬 처리 가능
  - newFixedThreadPool(int count) 메서드를 통해 쓰레드 풀 생성
  - submit() 메서드를 통해 작업 지시

- CountDownLatch 클래스를 사용해 어떤 쓰레드가 다른 쓰레드에서 작업이 완료될 때 까지 기다릴 수 있도록 함
  - countDown() 메서드를 통해 병렬로 처리되는 쓰레드 작업이 끝날 때마다 count을 1만큼 줄임
  - await() 메서드를 통해 latch의 숫자가 0이 될때까지 대기