## unwrap / ?
```rust
fn read_username_from_file() -> Result<String, io::Error> {
    let mut file = File::open("./Cargo.toml")?;
    let mut str = String::new();
    file.read_to_string(&mut str)?;
    Result::Ok(str)
}
```
// 问号意味着如果处理正常，则当前表达式返回处理结果，
// 如果报错，则将表达式所在的函数结束执行并返回Result::Err错误信息。

- https://zhuanlan.zhihu.com/p/377739309

## format! 格式

- https://www.cnblogs.com/jiangbo44/p/15626702.html

## Box、Rc、Arc、Cell、RefCell、Cow简介

- https://blog.csdn.net/hbuxiaofei/article/details/113814516