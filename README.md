# Tarpaulin

![Build Status](https://travis-ci.org/xd009642/tarpaulin.svg?branch=master) [![Latest Version](https://img.shields.io/crates/v/cargo-tarpaulin.svg)](https://crates.io/crates/cargo-tarpaulin)  [![License:MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Tarpaulin is designed to be a code coverage reporting tool for the Cargo build system, named for a waterproof cloth used to cover cargo on a ship. Currently, tarpaulin is in the early development stage and as thus is largely unstable although it may be possible to use certain features. But check out our roadmap for planned features.

Tarpaulin only supports x86/x86_64 processors running linux. This is because instrumenting breakpoints into executables and tracing their execution requires processor and OS specific code. It is a goal when greater stability is reached to add wider system support, however this is sufficient to run Tarpaulin on popular CI tools like Travis. 

## Features

Below is a list of features currently implemented. As Tarpaulin loads binary files into memory and parses the debugging information, different setups could lead to coverage not working. In this instance, please raise an issue detailing your setup and an example project and I'll attempt to fix it. 

* Line coverage
* Uploading coverage to https://coveralls.io

## Usage
To get detailed help on available arguments when running tarpaulin call:
```text
cargo tarpaulin --help
```
Currently no options are required, if no root directory is defined Tarpaulin will run in the current working directory.

Below is a Tarpaulin run utilising one of our example projects. This is a relatively simple project to test and the output is still rather rough. This is an area which is likely to have large amounts of change. If you check the test, you can see the output correctly reports the lines the test hits.


```text
cargo tarpaulin
"/home/xd009642/rust/tarpaulin/data/simple_project/Cargo.toml"
       Fresh simple_project v0.1.0 (file:///home/xd009642/dev/rust/tarpaulin/data/simple_project)
    Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
Running Tarpaulin
Processing simple_project
Coverage Results
src/unused.rs:4 - hits: 0
src/unused.rs:5 - hits: 0
src/unused.rs:6 - hits: 0
src/unused.rs:7 - hits: 0
src/lib.rs:4 - hits: 1
src/lib.rs:5 - hits: 1
src/lib.rs:6 - hits: 0
src/lib.rs:8 - hits: 1
src/lib.rs:10 - hits: 1
src/lib.rs:21 - hits: 1
src/lib.rs:22 - hits: 1
src/lib.rs:23 - hits: 1
Total of 7/12 lines covered
```

Hint: if using coveralls.io with travis-ci run with the options "--ciserver travis-ci --coveralls $TRAVIS_JOB_ID". The coveralls.io repo-token is mainly designed for private repos and it won't generate a badge for the coverage results submitted (although you can still see them on the coveralls web interface).

## Limitations

Currently Tarpaulin only works on projects where tests are located within a tests module (either by being in a tests directory or within a mod tests block. Also, any functions in the tests module which aren't tests will be ran as well. Tarpaulin is also untested in most situations so if any issues are spotted please raise them to help support our continued development

## Roadmap

- [x] Line coverage for tests
- [ ] Branch coverage for tests
- [ ] Condition coverage for tests
- [ ] Annotated coverage reports
- [ ] Coverage reports in the style of existing tools (i.e. kcov)
- [x] Integration with 3rd party tools like coveralls or codecov
- [ ] Optional coverage statistics for doctests
- [ ] MCDC coverage reports

## License

Tarpaulin is currently licensed under the terms of both the MIT license and the Apache License (Version 2.0). See LICENSE-MIT and LICENSE-APACHE for more details.

## Thanks

I wouldn't have been able to make progress as quickly in this project without Joseph Kain's blog on writing a debugger in Rust and C. It's a great read, so I recommend you check it out [here](http://system.joekain.com/debugger/).
