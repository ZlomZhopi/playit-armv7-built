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
​## How to build (Cross-compilation)

If you want to compile it yourself for ARMv7 Android (Termux), here is a quick roadmap:

1. **Install Android NDK** on Windows.
2. **Add Rust target:**
   `rustup target add armv7-linux-androideabi`
3. **Configure Cargo:**
   In `.cargo/config.toml`, point the linker to your NDK:
   ```toml
   [target.armv7-linux-androideabi]
   linker = "path/to/ndk/toolchains/llvm/prebuilt/windows-x86_64/bin/armv7a-linux-androideabi21-clang.exe"

4. Patch build.rs to prevent winres from running when the target is not Windows:
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
5. build
cargo build --release --target armv7-linux-androideabi

Hash sha256:344f94f996079cb9b845ea3eda524ce8cb8f70abb33cbe0d143ee2e4e9f5d6da

## Русский

Неофициальная сборка `playit-cli` для архитектуры **ARMv7**.
Протестировано на **Samsung Galaxy Ace 4 Neo (SM-G318H)** под управлением **Android 7.1.1 (LineageOS)** через **Termux**.

### Как запустить (Termux)

1. Скачайте бинарник из [Releases](https://github.com/ZlomZhopi/playit-armv7-built/releases/tag/v0.17.1-armv7)
2. Переместите его в домашнюю директорию Termux:

   ```bash
   cp /sdcard/Download/playit-cli ~/
   ```
3. Выдайте права на выполнение:

   ```bash
   chmod +x playit
   ```
4. Запустите:

   ```bash
   ./playit-cli
   ```

## Как это было собрано (кросс-компиляция)

Если хотите собрать самостоятельно под ARMv7 Android (Termux), вот краткий план:

1. **Установите Android NDK** на Windows.
2. **Добавьте target в Rust:**

   ```
   rustup target add armv7-linux-androideabi
   ```
3. **Настройте Cargo:**
   В `.cargo/config.toml` укажите линкер из NDK:

   ```toml
   [target.armv7-linux-androideabi]
   linker = "path/to/ndk/toolchains/llvm/prebuilt/windows-x86_64/bin/armv7a-linux-androideabi21-clang.exe"
   ```
4. Пропатчите `build.rs`, чтобы отключить запуск winres не на Windows:

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
5. Сборка:

   ```
   cargo build --release --target armv7-linux-androideabi
   ```

Хеш sha256:
344f94f996079cb9b845ea3eda524ce8cb8f70abb33cbe0d143ee2e4e9f5d6da













