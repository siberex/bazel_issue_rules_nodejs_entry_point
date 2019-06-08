### Issue

Bazel rules_nodejs 0.31.1 issue with nodejs_binary entry_point defined as label.

### Description

After switching from (0.30.2)

```
entry_point = "workspace_name/src/main.js",
```

to

```
entry_point = ":main.ts",
```

Bazel run produces error:

```
INFO: Build completed successfully, 6 total actions
Error: No file entry_point_label/src/main.js found in module root entry_point_label/src/src/main.js
    at Function.module.constructor._resolveFilename (/private/var/tmp/_bazel_sib/5848ea03bd44a0920c5f5eda67e7a2b2/execroot/entry_point_label/bazel-out/darwin-fastbuild/bin/src/server_bin_loader.js:362:13)
    at Function.Module._load (internal/modules/cjs/loader.js:506:25)
    at Object.<anonymous> (/private/var/tmp/_bazel_sib/5848ea03bd44a0920c5f5eda67e7a2b2/execroot/entry_point_label/bazel-out/darwin-fastbuild/bin/src/server_bin_loader.js:501:24)
    at Module._compile (internal/modules/cjs/loader.js:688:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:699:10)
    at Module.load (internal/modules/cjs/loader.js:598:32)
    at tryModuleLoad (internal/modules/cjs/loader.js:537:12)
    at Function.Module._load (internal/modules/cjs/loader.js:529:3)
    at Function.Module.runMain (internal/modules/cjs/loader.js:741:12)
    at startup (internal/bootstrap/node.js:285:19)
```

### How to reproduce

```bash
git clone git@github.com:siberex/bazel_issue_rules_nodejs_entry_point.git /tmp/entry_point_label
cd /tmp/entry_point_label
bazel run //src:server
```

### Workaround

Add `src/src/main.ts`:

```
import '../main';
```

