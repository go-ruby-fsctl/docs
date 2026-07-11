# go-ruby-fsctl

Pure-Go core of the Ruby `fsctl` gem (Linux dm/btrfs/zfs/loop ioctls).

`go-ruby-fsctl` is the pure-Go, Ruby-runtime-independent core of the Ruby `fsctl` gem: a reflective adapter over the [go-fsctl](https://github.com/go-fsctl) family (loop/dm/btrfs/zfs) of pure-Go Linux kernel-ioctl wrappers, returning Ruby-shaped values. It is equally usable as a standalone Go library.


!!! note
    The rbgo `require "fsctl"` binding that wires this adapter into the Ruby interpreter lives in [go-embedded-ruby](https://github.com/go-embedded-ruby), not in this org.

## Repositories

<div class="repo-grid" markdown>
<a class="repo-card" href="repos/fsctl.md"><code>fsctl</code><br><small>Reflective adapter over the go-fsctl family (loop/dm/btrfs/zfs) of Linux ioctl wrappers.</small></a>
</div>
