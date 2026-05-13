# amalgame-compress

zlib **gzip + raw-deflate** codec for [Amalgame](https://github.com/amalgame-lang/Amalgame).
Round-trips `List<int>` byte buffers through `deflate` / `inflate`
with the appropriate `windowBits` for each wire format.

Originally shipped in amc's bundled `runtime/Amalgame_Compress.h`;
extracted into this external package as part of the v0.7.8
bundled-runtime trim.

## Install

```bash
amc package add compress                  # via the curated index
amc package add github.com/amalgame-lang/amalgame-compress@v0.1.0
```

Requires **amc 0.7.7+** and the system `zlib` (`-lz`) — installed
out of the box on Linux, macOS, MSYS2.

## Surface

```amalgame
import Amalgame.Collections
import Amalgame.Compress

class Program {
    public static void Main() {
        let raw: List<int> = new List<int>()
        for c in "Hello, Amalgame! Hello, Amalgame! Hello, Amalgame!" {
            raw.Add(c)
        }

        // gzip: full RFC 1952 wrapper, gzip(1)/zcat compatible
        let z: List<int> = Compress.Gzip(raw)
        Console.WriteLine("gzip:    " + String_FromInt(z.Count()) + " bytes")
        let back: List<int> = Compress.Gunzip(z)
        Console.WriteLine("back:    " + String_FromInt(back.Count()) + " bytes")

        // raw deflate: no wrapper, ~10 bytes smaller — useful when
        // you have your own framing (e.g. HTTP Content-Encoding).
        let d: List<int> = Compress.Deflate(raw)
        Console.WriteLine("deflate: " + String_FromInt(d.Count()) + " bytes")
    }
}
```

## Tests

```bash
./tests/run_tests.sh /path/to/amc
```

## License

Apache-2.0 — see `LICENSE`. No vendored third-party code; links
against system zlib (zlib license, BSD-style).
