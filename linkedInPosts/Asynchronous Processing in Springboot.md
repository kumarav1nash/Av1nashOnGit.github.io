@Async annotation can help to achieve this, to use this we need to use @EnableAsync annotation in main class of spring application

@Async annotation uses default executor to create and manage threads, if no default executor present it'll create new SimpleAsyncTaskExecutor.

We should always create custom ThreadPoolTaskExecutor to have more control of thread management in spring boot
```java


```


