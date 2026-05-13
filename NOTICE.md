# NOTICE — amalgame-compress

## Authorship

Copyright 2026 Bastien Mouget. The Amalgame binding code in this
repository is original work — see `runtime/Amalgame_Compress.h`
and the `amalgame.toml` manifest.

This package is part of the Amalgame ecosystem
([github.com/amalgame-lang/Amalgame](https://github.com/amalgame-lang/Amalgame)).
It was extracted from amc's bundled `runtime/Amalgame_Compress.h`
during the v0.7.8 bundled-runtime trim.

## License

Licensed under the Apache License, Version 2.0 — see `LICENSE`.

## Third-party content

No vendored sources. Calls into:

- **zlib** (`<zlib.h>` — `deflate` / `inflate`) — link with
  `-lz`. Available out of the box on Linux, macOS, MSYS2.
  Distributed under the zlib license (BSD-style, attribution-only).
