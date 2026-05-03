# playit-armv7-built
v 0.17.1, will not be supported
(поддерживать не буду) 
# playit-cli v0.17.1 (ARMv7 Build)


---

## English

Unofficial binary build of `playit-cli` for **ARMv7** architecture.  
Tested on **Samsung Galaxy Ace 4 Neo (SM-G318H)** running **Android 7.1.1 (LineageOS)** via **Termux**.

### How to run (Termux)
1. Download the binary from [Releases](https://github.com/ZlomZhopi/playit-armv7-built/releases/tag/v0.17.1-armv7) 
2. Move it to your Termux home directory:
   ```bash
   cp /sdcard/Download/playit-cli ~/
3. Give execution permissions:
   ```bash
   chmod +x playit
4. Run it
   ```bash
  ./playit-cli


How it was built (Cross-compilation)
​Compiled on Windows using Android NDK:
Target: armv7-linux-androideabi
Linker: Pointed to NDK's armv7a-linux-androideabi21-clang.exe in .cargo/config.toml.
Patch: Modified build.rs to prevent winres from running when the target is not Windows:
```rust
fn main() {
    #[cfg(target_os = "windows")]
    }
    
    let target_os = std::env::var("CARGO_CFG_TARGET_OS").unwrap_or_default();
    if target_os == "windows" {
        let mut res = winres::WindowsResource::new();
        res.set_icon("wix/Product.ico");
        res.compile().unwrap();
    }
}
```
**Configure Cargo:**
   In `.cargo/config.toml`, point the linker to your NDK:
   ```toml
   [target.armv7-linux-androideabi]
   linker = "path/to/ndk/toolchains/llvm/prebuilt/windows-x86_64/bin/armv7a-linux-androideabi21-clang.exe"

```
Then build
cargo build --release --target armv7-linux-androideabi


Русский ниасилил
