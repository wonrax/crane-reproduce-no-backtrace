Backtrace has filenames and line numbers when run via the CLI (`nix develop -c cargo run`) but not when built with crane (`nix run .#myapp`)

```shell
>: RUST_BACKTRACE=full nix develop -c cargo run --release

    Finished `release` profile [optimized + debuginfo] target(s) in 0.03s
     Running `target/release/crane-reproduce-no-backtrace`

thread 'main' panicked at src/main.rs:2:5:
explicit panic
stack backtrace:
   0:        0x100bc3a80 - std::backtrace_rs::backtrace::libunwind::trace::h72f4b72e0962905d
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/../../backtrace/src/backtrace/libunwind.rs:117:9
   1:        0x100bc3a80 - std::backtrace_rs::backtrace::trace_unsynchronized::hff394536698b6b10
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/../../backtrace/src/backtrace/mod.rs:66:14
   2:        0x100bc3a80 - std::sys::backtrace::_print_fmt::h64d1e3035850353e
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/sys/backtrace.rs:66:9
   3:        0x100bc3a80 - <std::sys::backtrace::BacktraceLock::print::DisplayBacktrace as core::fmt::Display>::fmt::hf35f9734f9a29483
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/sys/backtrace.rs:39:26
   4:        0x100bd6fe4 - core::fmt::rt::Argument::fmt::hedf6f2a66f855f69
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/core/src/fmt/rt.rs:173:76
   5:        0x100bd6fe4 - core::fmt::write::h60ec6633daab7b35
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/core/src/fmt/mod.rs:1468:25
   6:        0x100bc2154 - std::io::default_write_fmt::h0e30d7b1295222cb
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/io/mod.rs:639:11
   7:        0x100bc2154 - std::io::Write::write_fmt::hc29709fdab2e34e2
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/io/mod.rs:1954:13
   8:        0x100bc3934 - std::sys::backtrace::BacktraceLock::print::hca95bffd78053951
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/sys/backtrace.rs:42:9
   9:        0x100bc4920 - std::panicking::default_hook::{{closure}}::h357ed4fbef22679d
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/panicking.rs:300:27
  10:        0x100bc4778 - std::panicking::default_hook::h0a4e133b151d5758
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/panicking.rs:327:9
  11:        0x100bc52f8 - std::panicking::rust_panic_with_hook::h557a23724a5de839
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/panicking.rs:833:13
  12:        0x100bc4fdc - std::panicking::begin_panic_handler::{{closure}}::h269cace6208fef05
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/panicking.rs:706:13
  13:        0x100bc3f30 - std::sys::backtrace::__rust_end_short_backtrace::h5be0da278f3aaec7
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/sys/backtrace.rs:174:18
  14:        0x100bc4cb8 - __rustc[de2ca18b4c54d5b8]::rust_begin_unwind
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/panicking.rs:697:5
  15:        0x100bde5ec - core::panicking::panic_fmt::h477ff48eff31ffa4
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/core/src/panicking.rs:75:14
  16:        0x100bde71c - core::panicking::panic_display::hf5e4e2b0a7e11286
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/core/src/panicking.rs:268:5
  17:        0x100bde71c - core::panicking::panic_explicit::h62c859e5857c8bb0
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/core/src/panicking.rs:241:5
  18:        0x100bda898 - crane_reproduce_no_backtrace::main::panic_cold_explicit::h4e30cd2d656e73bf
                               at /nix/store/lfndsjpm8zfgbzj4xmdhwyac05yym1ns-rust-default-1.90.0/lib/rustlib/src/rust/library/core/src/panic.rs:88:13
  19:        0x100bda884 - crane_reproduce_no_backtrace::main::h2ac14e3cb6a76e5d
                               at /Users/wonrax/code/crane-reproduce-no-backtrace/src/main.rs:2:5
  20:        0x100baa194 - core::ops::function::FnOnce::call_once::h859c08fddb2fe7da
                               at /nix/store/lfndsjpm8zfgbzj4xmdhwyac05yym1ns-rust-default-1.90.0/lib/rustlib/src/rust/library/core/src/ops/function.rs:253:5
  21:        0x100baa194 - std::sys::backtrace::__rust_begin_short_backtrace::h3d2e9a0421467fc7
                               at /nix/store/lfndsjpm8zfgbzj4xmdhwyac05yym1ns-rust-default-1.90.0/lib/rustlib/src/rust/library/std/src/sys/backtrace.rs:158:18
  22:        0x100baa17c - std::rt::lang_start::{{closure}}::h9c07d2ebe311fb60
                               at /nix/store/lfndsjpm8zfgbzj4xmdhwyac05yym1ns-rust-default-1.90.0/lib/rustlib/src/rust/library/std/src/rt.rs:206:18
  23:        0x100bc0338 - core::ops::function::impls::<impl core::ops::function::FnOnce<A> for &F>::call_once::hbb2eb0e6976088d9
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/core/src/ops/function.rs:290:21
  24:        0x100bc0338 - std::panicking::catch_unwind::do_call::h93858ce5ba09f3d9
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/panicking.rs:589:40
  25:        0x100bc0338 - std::panicking::catch_unwind::h129a241a010f1b76
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/panicking.rs:552:19
  26:        0x100bc0338 - std::panic::catch_unwind::h5ca6b885cfe10586
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/panic.rs:359:14
  27:        0x100bc0338 - std::rt::lang_start_internal::{{closure}}::hed6353a412388a00
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/rt.rs:175:24
  28:        0x100bc0338 - std::panicking::catch_unwind::do_call::h6579b7caa3691f01
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/panicking.rs:589:40
  29:        0x100bc0338 - std::panicking::catch_unwind::h4557f88752b89087
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/panicking.rs:552:19
  30:        0x100bc0338 - std::panic::catch_unwind::h82809ba82b8374af
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/panic.rs:359:14
  31:        0x100bc0338 - std::rt::lang_start_internal::hdb28e94b6865fa11
                               at /rustc/1159e78c4747b02ef996e55082b704c09b970588/library/std/src/rt.rs:171:5
  32:        0x100baa1ec - _main

```

```shell
>: RUST_BACKTRACE=full nix run .#myapp

thread 'main' panicked at src/main.rs:2:5:
explicit panic
stack backtrace:
   0:        0x1005efa80 - <std::sys::backtrace::BacktraceLock::print::DisplayBacktrace as core::fmt::Display>::fmt::hf35f9734f9a29483
   1:        0x100602fe4 - core::fmt::write::h60ec6633daab7b35
   2:        0x1005ee154 - std::io::Write::write_fmt::hc29709fdab2e34e2
   3:        0x1005ef934 - std::sys::backtrace::BacktraceLock::print::hca95bffd78053951
   4:        0x1005f0920 - std::panicking::default_hook::{{closure}}::h357ed4fbef22679d
   5:        0x1005f0778 - std::panicking::default_hook::h0a4e133b151d5758
   6:        0x1005f12f8 - std::panicking::rust_panic_with_hook::h557a23724a5de839
   7:        0x1005f0fdc - std::panicking::begin_panic_handler::{{closure}}::h269cace6208fef05
   8:        0x1005eff30 - std::sys::backtrace::__rust_end_short_backtrace::h5be0da278f3aaec7
   9:        0x1005f0cb8 - __rustc[de2ca18b4c54d5b8]::rust_begin_unwind
  10:        0x10060a5ec - core::panicking::panic_fmt::h477ff48eff31ffa4
  11:        0x10060a71c - core::panicking::panic_explicit::h62c859e5857c8bb0
  12:        0x100606898 - crane_reproduce_no_backtrace::main::panic_cold_explicit::h4e30cd2d656e73bf
  13:        0x100606884 - crane_reproduce_no_backtrace::main::h2ac14e3cb6a76e5d
  14:        0x1005d6194 - std::sys::backtrace::__rust_begin_short_backtrace::h3d2e9a0421467fc7
  15:        0x1005d617c - std::rt::lang_start::{{closure}}::h9c07d2ebe311fb60
  16:        0x1005ec338 - std::rt::lang_start_internal::hdb28e94b6865fa11
  17:        0x1005d61ec - _main
```
