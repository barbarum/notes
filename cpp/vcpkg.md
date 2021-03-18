# VCPKG 

https://github.com/microsoft/vcpkg

1. Add vcpkg features into your environment (`~/.bashrc`, `~/.zshrc`)

```bash
export VCPKG_FEATURE_FLAGS="versions manifests"
```

## Versioning 

[Versioning Support](https://devblogs.microsoft.com/cppblog/take-control-of-your-vcpkg-dependencies-with-versioning-support/)

1. Add cmake configuration for your project `.vscode/settings.json` in VS Code 

```bash
{
    "cmake.configureSettings": {
        "CMAKE_TOOLCHAIN_FILE": "{vcpkg_root}/scripts/buildsystems/vcpkg.cmake"
    }
}
```

2. Configure `CMakeLists.txt` to enable versioning feature 

```bash
set(VCPKG_FEATURE_FLAGS "versions")
```

3. Add `vcpkg.json` into root directory of your c++ project

```bash 
{
    "name": "mall-grpc-api-cpp-tutorial",
    "version": "0.1.0", 
    "dependencies": [
        {
            "name": "protobuf"
        }
    ],
    "builtin-baseline": "319b8f06ebbf8f524df78b4578fb0efeb6772c50",
    "overrides": [
        {
            "name": "protobuf", 
            "version": "3.6.0.1"
        }
    ]
}
```
> Notes: 
> 1. `builtin-baseline` matches to vcpkg git commit id (`git rev-parse HEAD`). 
> 2. Downgraded version is written by `overrides`.
> 3. All dependencies from `CMakeLists.txt` must define in `vcpkg.json`.

4. 