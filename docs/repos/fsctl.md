# fsctl

Reflective adapter over the go-fsctl family (loop/dm/btrfs/zfs) of Linux ioctl wrappers.

A `Session` maps a snake_case method name to the corresponding go-fsctl operation, coerces the Ruby arguments, and normalises the result to a Hash, Array or scalar — the surface an rbgo binding drives from `method_missing`.

## Highlights

- Wraps the four go-fsctl subpackages (loop, dm, btrfs, zfs) behind one surface.
- Returns Ruby-shaped values: Hash (`map[string]any`), Array (`[]any`) or scalar.
- `Call(ctx, method, args...)` reflective dispatch drives `method_missing`.
- Compiles on darwin, windows and linux; off Linux the wrapped operations surface `ErrUnsupported` (the stubbing already lives in go-fsctl).
- Function-seam design lets tests inject fakes without root or a live kernel — **100% statement coverage** (Linux CI is the authoritative coverage gate).

## Method surface

| Prefix | Methods |
| ------ | ------- |
| `loop_`  | `available`, `attach`, `detach`, `set_capacity`, `status`, `find` |
| `dm_`    | `available`, `version`, `create`, `remove`, `suspend`, `resume`, `info`, `list`, `status`, `table`, `message`, `create_linear` |
| `btrfs_` | `available`, `subvolume_create`, `subvolume_delete`, `snapshot_create`, `subvolume_list`, `subvolume_info`, `subvolume_id`, `is_readonly`, `sync` |
| `zfs_`   | `available`, `pool_names`, `create_filesystem`, `destroy`, `snapshot`, `rename`, `clone`, `rollback`, `holds` |

## Example

```go
s := fsctl.NewSession()
dev, _  := s.Call(ctx, "loop_attach", "/tmp/disk.img")   // "/dev/loop3"
subs, _ := s.Call(ctx, "btrfs_subvolume_list", "/mnt")   // Array of Hashes
_, _    = s.Call(ctx, "zfs_snapshot", "tank", "tank/fs@backup")
```

## Install

```sh
go get github.com/go-ruby-fsctl/fsctl
```

Requires Go 1.26 or newer.

## Links

- Source — <https://github.com/go-ruby-fsctl/fsctl>
- API reference — <https://pkg.go.dev/github.com/go-ruby-fsctl/fsctl>

!!! note
    The rbgo `require "fsctl"` binding that wires this adapter into the Ruby interpreter lives in [go-embedded-ruby](https://github.com/go-embedded-ruby), not in this org.
