# mptcp-bbr2
MPTCP enabled kernel (upstream) with bbr2

##  Build

1. Clone repo and add the upstream kernel:
```
git clone https://github.com/grapexy/mptcp-bbr2.git
cd mptcp-bbr2
git remote add stable git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git
git fetch stable --tags
```
2. Find the needed linux kernel version and checkout
```
git branch -r
git checkout stable/linux-5.19.y
```
3. Add this repo to the kernel path:
```
git merge --allow-unrelated-histories master --no-ff -X theirs
```


To create patch for a different kernel version, checkout the `v2alpha` branch of https://github.com/google/bbr and look for the most recent kernel base.
For example  > [Linux 5.13.12](https://github.com/google/bbr/commit/f428e49b8cb1fbd9b4b4b29ea31b6991d2ff7de1)

Then generate the patch from that point to `v2alpha`'s HEAD, including only what's necessary:
```
git checkout v2alpha
git diff {KERNEL_BASE_SHA}..HEAD -- 'net' 'include' 'Documentation' > bbr2.patch
```

Then fix up that patch as necessary.
