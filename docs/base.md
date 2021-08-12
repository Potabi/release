# Potabi RE Team Documentation
## Base Releases
A "base release" is a release on the [Potabi RE Repository](https://github.com/Potabi/release) that is dedicated to only three files:
- `base.txz`
- `kernel.txz`
- `disc1.iso`

They should be in no way treated as "regular releases". Base releases are part of the build process for building regular releases. This hosts the important build files without having to wait for a src build to release. This will also help standardize point releases.

## Building Base Releases
When you either want to for personal reasons, or have to for releasing Potabi, here is how to build a base release.

### The Dependencies
- FreeBSD: Either bare metal or VM works.
  - VM works best as it wont screw with your current system
  - Must have the minimum specs set below:
  ```
  CPU CORES: 4
  MEMORY: 6GB
  DISK: 50GB or more
  ```
- Git: This is the only vital program you need

When you have the dependencies in your build system, proceed.

### Getting the Source
Unless you are building an experimental release, you should NEVER build a base release from the `main` branch of the [potabi-src](https://github.com/Potabi/potabi-src) repository. The best option should be to pick the latest stable release branch. You will extract this contents into `/usr/src`. If `/usr/src` is not empty, it would be best to either reinstall without it. Sometimes deleing the `/usr/src` directory doesn't happen cleanly. 


Here is an example using the `stable/13` upstream branch.
```sh
cd /usr/src
git clone https://github.com/potabi/potabi-src -b stable/13 . --depth 1
```

Once you have the required files, to build base, run the following commands:
```sh
make buildworld buildkernel # Adding -j4, -j6, -j8, -j12, or higher depending on your system specs is highly recommended.
cd /usr/src/release 
make obj
make real-release NODOCS=1 NOSRC=1 NOPORTS=1 # -j* arguments tend to have issues here
```

After this, you should find the release information in the following directory:
```sh
/usr/obj/usr/src/$(uname -m).$(uname -p)/release
```

An example directory would be
```sh
/usr/obj/usr/src/amd64.amd64/release
```
