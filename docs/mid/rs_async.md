## JoinHandle

tokio::spawn 得到 thread : tokio::runtime::JoinHandle<_>,它
```rust
impl<T> Future for JoinHandle<T> {
    type Output = super::Result<T>;

    fn poll(self: Pin<&mut Self>, cx: &mut Context<'_>) -> Poll<Self::Output> {
        ...
    }
}
```
所以可以这么使用
```rust
thread.await.unwrap();
```


## oneshot

```rust
let ( tx1, rx1) = oneshot::channel();
    let atx1 = Arc::new(tx1);

    tokio::spawn(async {
        atx1.send("xx")
    });
```
会报错`cannot move out of an Arc`
因为
```rust
pub fn send(mut self, t: T) -> Result<(), T>
```

而一般的 `mpsc::channel`
```rust
pub fn send(&self, t: T) -> Result<(), SendError<T>>
```
不会 *move out self*

## cannot borrow data in an `Arc` as mutable

`Arc` 没有 DerefMut, `Mutex`有 
```rust
impl<'a, T: ?Sized> DerefMut for MutexGuard<'a, T> {
    fn deref_mut(&mut self) -> &mut T {
        &mut *self.inner
    }
}
```
所以跨线程调用的东西需要包起来 `Arc<Mutex<T>>`