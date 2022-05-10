```rust
impl ConfigPrivateExt for Config {
    fn unpack(self) -> (Vec<Appender>, Root, Vec<Logger>) {
        let Config {
            appenders,
            root,
            loggers,
        } = self;
        (appenders, root, loggers)
    }
}
```
Mutex: m.lock().some_member , Mutex加锁后获得MutexGuard，可以直接调用成员变量
```rust
// 
impl<T: ?Sized> DerefMut for MutexGuard<'_, T> {
    fn deref_mut(&mut self) -> &mut T {
        unsafe { &mut *self.lock.data.get() }
    }
}

```