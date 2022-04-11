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