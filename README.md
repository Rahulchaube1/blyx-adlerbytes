<img src="assets/logo.png" width="112" height="112" alt="Blyx penguin feeding bytes through two linked checksum wheels.">

# AdlerBytes

Compute the RFC 1950 Adler-32 checksum over a sequence of bytes. This Blyx library is part of the validation and configuration collection.

A valid byte offset can point into the wrong serialized record if lengths have drifted. Verify the table and payload before interpreting the offset. [IETF RFC 1950, Adler-32](https://www.rfc-editor.org/rfc/rfc1950)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-adlerbytes.git
cd blyx-adlerbytes
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-adlerbytes) · [Package page](https://www.blyx-lang.space/packages/adlerbytes) · [Handbook](https://doc.blyx-lang.space/guide/swallow)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-adlerbytes.git vendor/adlerbytes
```

```blyx
use vendor::adlerbytes::adlerbytes;

fn main() {
    let bytes = [65, 66];
    let result = adlerbytes_digest(bytes);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
12976260
132
198
```

## API

`adlerbytes_digest(bytes)`

Returns [unsigned checksum, rolling low accumulator, rolling high accumulator]. The empty digest is 1. Use for accidental corruption detection. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| bytes | Vector of values, each a whole byte in [0,255] |

## In use

[Swallow](https://github.com/Rahulchaube1/blyx-swallow) uses this module to validate an exported payload's declared spans and checksum, then locate a byte.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-adlerbytes/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). Read the [artwork notice](assets/NOTICE.txt) for credits.

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
