## unwrap / ?

```rust
fn read_username_from_file() -> Result<String, io::Error> {
    let mut file = File::open("./Cargo.toml")?;
    let mut str = String::new();
    file.read_to_string(&mut str)?;
    Result::Ok(str)
}
```

// 问号意味着如果处理正常，则当前表达式返回处理结果， // 如果报错，则将表达式所在的函数结束执行并返回Result::Err错误信息。

- https://zhuanlan.zhihu.com/p/377739309

## format! 格式

- https://www.cnblogs.com/jiangbo44/p/15626702.html

## Box、Rc、Arc、Cell、RefCell、Cow简介

- https://blog.csdn.net/hbuxiaofei/article/details/113814516
- 查看代码，Box,Rc 的 `borrow` 和 `as_ref` 的实现一样
    ```rust
    fn borrow(&self) -> &T {
        &**self
    }
    ```
- Syn: 跨线程共享
  - rust 的可变引用要求过于严苛导致我们很多时候必须使用不可变引用来改变自身，所以 Sync 是用来标记不可变借用可线程安全地访问的
  - 对于可变引用 &mut 天然可以，因为只存在一个，且不和可变共存
  - 对于不可变 ，需要 Arc<Mutex<T>> 或`其他？`

- RefCell
  - 可以多次 borrow(读), 只能一次 borrow_mut(写)
  - 不能同时读和写
  - 内部使用 BorrowFlag 来判断，初始化时为0，读+1，写-1，见`RefCell::try_borrow`
  