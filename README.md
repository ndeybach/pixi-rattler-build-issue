# pixi-rattler-build-issue
This is a repo for a minimaly reproducible example of what seems like a current limitation of using rattler-build recipe.yaml directly in pixi's project definition ==> errors on build string.


# How to reproduce:

1. Clone this repo

2. Run ` pixi install --all` in the root of the repo

You will see an error like this:

```bash
pixi install --all
Error:   × failed to build 'demo-context-buildstring' from './demo-recipe'
  ╰─▶   × the requested output demo-context-buildstring/0.1.0=_py_hb0f4dca_@linux-64 was not found in the recipe
```

3. Now comment the build.string line in `demo-recipe/recipe.yaml`:
```yaml
build:
  number: 0
#   string: ${{ build_string_prefix }}_py${{ python | version_to_buildstring }}_h${{ hash }}_${{ build_number }}
  script:
    - echo "demo" > "$PREFIX/demo.txt"
```

4. Run ` pixi install --all` again:

You will see that the build now succeeds:

<details>

<summary>Pixi install output on success</summary>

```bash
pixi install --all

 ╭─ Running build for recipe: demo-context-buildstring-0.1.0-hb0f4dca_0
 │
 │ ╭─ Fetching source code
 │ │ No sources to fetch
 │ │
 │ ╰─────────────────── (took 0 seconds)
 │
 │ ╭─ Externally resolved dependencies recipe: demo-context-buildstring-0.1.0-hb0f4dca_0
 │ │ 
 │ │ Resolved build dependencies(demo-context-buildstring-0.1.0-hb0f4dca_0):
 │ │ ╭──────────────────┬───────────────┬────────────┬────────────────────┬─────────────┬────────────╮
 │ │ │ Package          ┆ Spec          ┆ Version    ┆ Build              ┆ Channel     ┆       Size │
 │ │ ╞══════════════════╪═══════════════╪════════════╪════════════════════╪═════════════╪════════════╡
 │ │ │ python           ┆ python 3.11.* ┆ 3.11.14    ┆ hd63d673_2_cpython ┆ conda-forge ┆  29.44 MiB │
 │ │ │ _libgcc_mutex    ┆               ┆ 0.1        ┆ conda_forge        ┆ conda-forge ┆   2.50 KiB │
 │ │ │ _openmp_mutex    ┆               ┆ 4.5        ┆ 2_gnu              ┆ conda-forge ┆  23.07 KiB │
 │ │ │ bzip2            ┆               ┆ 1.0.8      ┆ hda65f42_8         ┆ conda-forge ┆ 254.24 KiB │
 │ │ │ ca-certificates  ┆               ┆ 2025.11.12 ┆ hbd8a1cb_0         ┆ conda-forge ┆ 148.86 KiB │
 │ │ │ icu              ┆               ┆ 75.1       ┆ he02047a_0         ┆ conda-forge ┆  11.57 MiB │
 │ │ │ ld_impl_linux-64 ┆               ┆ 2.45       ┆ h1aa0949_0         ┆ conda-forge ┆ 736.08 KiB │
 │ │ │ libexpat         ┆               ┆ 2.7.1      ┆ hecca717_0         ┆ conda-forge ┆  73.06 KiB │
 │ │ │ libffi           ┆               ┆ 3.5.2      ┆ h9ec8514_0         ┆ conda-forge ┆  56.47 KiB │
 │ │ │ libgcc           ┆               ┆ 15.2.0     ┆ h767d61c_7         ┆ conda-forge ┆ 803.27 KiB │
 │ │ │ libgcc-ng        ┆               ┆ 15.2.0     ┆ h69a702a_7         ┆ conda-forge ┆  28.63 KiB │
 │ │ │ libgomp          ┆               ┆ 15.2.0     ┆ h767d61c_7         ┆ conda-forge ┆ 437.42 KiB │
 │ │ │ liblzma          ┆               ┆ 5.8.1      ┆ hb9d3cd8_2         ┆ conda-forge ┆ 110.25 KiB │
 │ │ │ libnsl           ┆               ┆ 2.0.1      ┆ hb9d3cd8_1         ┆ conda-forge ┆  32.94 KiB │
 │ │ │ libsqlite        ┆               ┆ 3.51.0     ┆ hee844dc_0         ┆ conda-forge ┆ 923.41 KiB │
 │ │ │ libstdcxx        ┆               ┆ 15.2.0     ┆ h8f9b012_7         ┆ conda-forge ┆   3.72 MiB │
 │ │ │ libstdcxx-ng     ┆               ┆ 15.2.0     ┆ h4852527_7         ┆ conda-forge ┆  28.66 KiB │
 │ │ │ libuuid          ┆               ┆ 2.41.2     ┆ he9a06e4_0         ┆ conda-forge ┆  36.26 KiB │
 │ │ │ libxcrypt        ┆               ┆ 4.4.36     ┆ hd590300_1         ┆ conda-forge ┆  98.04 KiB │
 │ │ │ libzlib          ┆               ┆ 1.3.1      ┆ hb9d3cd8_2         ┆ conda-forge ┆  59.53 KiB │
 │ │ │ ncurses          ┆               ┆ 6.5        ┆ h2d0b736_3         ┆ conda-forge ┆ 870.74 KiB │
 │ │ │ openssl          ┆               ┆ 3.6.0      ┆ h26f9b46_0         ┆ conda-forge ┆   3.02 MiB │
 │ │ │ readline         ┆               ┆ 8.2        ┆ h8c095d6_2         ┆ conda-forge ┆ 275.86 KiB │
 │ │ │ tk               ┆               ┆ 8.6.13     ┆ noxft_ha0e22de_103 ┆ conda-forge ┆   3.13 MiB │
 │ │ │ tzdata           ┆               ┆ 2025b      ┆ h78e105d_0         ┆ conda-forge ┆ 120.09 KiB │
 │ │ │ zstd             ┆               ┆ 1.5.7      ┆ hb8e6e7a_2         ┆ conda-forge ┆ 554.28 KiB │
 │ │ ╰──────────────────┴───────────────┴────────────┴────────────────────┴─────────────┴────────────╯
 │ │ Resolved host dependencies(demo-context-buildstring-0.1.0-hb0f4dca_0):
 │ │ ╭──────────────────┬───────────────┬────────────┬────────────────────┬─────────────┬────────────╮
 │ │ │ Package          ┆ Spec          ┆ Version    ┆ Build              ┆ Channel     ┆       Size │
 │ │ ╞══════════════════╪═══════════════╪════════════╪════════════════════╪═════════════╪════════════╡
 │ │ │ python           ┆ python 3.11.* ┆ 3.11.14    ┆ hd63d673_2_cpython ┆ conda-forge ┆  29.44 MiB │
 │ │ │ _libgcc_mutex    ┆               ┆ 0.1        ┆ conda_forge        ┆ conda-forge ┆   2.50 KiB │
 │ │ │ _openmp_mutex    ┆               ┆ 4.5        ┆ 2_gnu              ┆ conda-forge ┆  23.07 KiB │
 │ │ │ bzip2            ┆               ┆ 1.0.8      ┆ hda65f42_8         ┆ conda-forge ┆ 254.24 KiB │
 │ │ │ ca-certificates  ┆               ┆ 2025.11.12 ┆ hbd8a1cb_0         ┆ conda-forge ┆ 148.86 KiB │
 │ │ │ icu              ┆               ┆ 75.1       ┆ he02047a_0         ┆ conda-forge ┆  11.57 MiB │
 │ │ │ ld_impl_linux-64 ┆               ┆ 2.45       ┆ h1aa0949_0         ┆ conda-forge ┆ 736.08 KiB │
 │ │ │ libexpat         ┆               ┆ 2.7.1      ┆ hecca717_0         ┆ conda-forge ┆  73.06 KiB │
 │ │ │ libffi           ┆               ┆ 3.5.2      ┆ h9ec8514_0         ┆ conda-forge ┆  56.47 KiB │
 │ │ │ libgcc           ┆               ┆ 15.2.0     ┆ h767d61c_7         ┆ conda-forge ┆ 803.27 KiB │
 │ │ │ libgcc-ng        ┆               ┆ 15.2.0     ┆ h69a702a_7         ┆ conda-forge ┆  28.63 KiB │
 │ │ │ libgomp          ┆               ┆ 15.2.0     ┆ h767d61c_7         ┆ conda-forge ┆ 437.42 KiB │
 │ │ │ liblzma          ┆               ┆ 5.8.1      ┆ hb9d3cd8_2         ┆ conda-forge ┆ 110.25 KiB │
 │ │ │ libnsl           ┆               ┆ 2.0.1      ┆ hb9d3cd8_1         ┆ conda-forge ┆  32.94 KiB │
 │ │ │ libsqlite        ┆               ┆ 3.51.0     ┆ hee844dc_0         ┆ conda-forge ┆ 923.41 KiB │
 │ │ │ libstdcxx        ┆               ┆ 15.2.0     ┆ h8f9b012_7         ┆ conda-forge ┆   3.72 MiB │
 │ │ │ libstdcxx-ng     ┆               ┆ 15.2.0     ┆ h4852527_7         ┆ conda-forge ┆  28.66 KiB │
 │ │ │ libuuid          ┆               ┆ 2.41.2     ┆ he9a06e4_0         ┆ conda-forge ┆  36.26 KiB │
 │ │ │ libxcrypt        ┆               ┆ 4.4.36     ┆ hd590300_1         ┆ conda-forge ┆  98.04 KiB │
 │ │ │ libzlib          ┆               ┆ 1.3.1      ┆ hb9d3cd8_2         ┆ conda-forge ┆  59.53 KiB │
 │ │ │ ncurses          ┆               ┆ 6.5        ┆ h2d0b736_3         ┆ conda-forge ┆ 870.74 KiB │
 │ │ │ openssl          ┆               ┆ 3.6.0      ┆ h26f9b46_0         ┆ conda-forge ┆   3.02 MiB │
 │ │ │ readline         ┆               ┆ 8.2        ┆ h8c095d6_2         ┆ conda-forge ┆ 275.86 KiB │
 │ │ │ tk               ┆               ┆ 8.6.13     ┆ noxft_ha0e22de_103 ┆ conda-forge ┆   3.13 MiB │
 │ │ │ tzdata           ┆               ┆ 2025b      ┆ h78e105d_0         ┆ conda-forge ┆ 120.09 KiB │
 │ │ │ zstd             ┆               ┆ 1.5.7      ┆ hb8e6e7a_2         ┆ conda-forge ┆ 554.28 KiB │
 │ │ ╰──────────────────┴───────────────┴────────────┴────────────────────┴─────────────┴────────────╯
 │ │ Resolved run dependencies(demo-context-buildstring-0.1.0-hb0f4dca_0):
 │ │ ╭──────────────────┬───────────────────────────────────────╮
 │ │ │ Name             ┆ Spec                                  │
 │ │ ╞══════════════════╪═══════════════════════════════════════╡
 │ │ │ Run dependencies ┆                                       │
 │ │ │ python           ┆ 3.11.*                                │
 │ │ │ python_abi       ┆ 3.11.* *_cp311 (RE of [host: python]) │
 │ │ ╰──────────────────┴───────────────────────────────────────╯
 │ │
 │ ╰─────────────────── (took 0 seconds)
 │
 │ ╭─ Packaging new files
 │ │ Copying done!
 │ │ ⚠ warning Overdepending against python_abi
 │ │ Post-processing done!
 │ │ Writing test files
 │ │ Writing metadata for package
 │ │ Copying license files
 │ │ Copying recipe files
 │ │ Creating entry points
 │ │ 
 │ │ Files in package:
 │ │   - demo.txt
 │ │   - info/about.json
 │ │   - info/hash_input.json
 │ │   - info/index.json
 │ │   - info/paths.json
 │ │   - info/tests/tests.yaml
 │ │ Creating target folder '<repo-root>/.pixi/build/work/demo-context-buildstring-zeUeUnUSyyU/output/li
 │ │ nux-64'
 │ │ Compressing archive...
 │ │ Archive written to '<repo-root>/.pixi/build/work/demo-context-buildstring-zeUeUnUSyyU/output/linux-
 │ │ 64/demo-context-buildstring-0.1.0-hb0f4dca_0.conda'
 │ │
 │ ╰─────────────────── (took 0 seconds)
 │
 ╰─────────────────── (took 0 seconds)
✔ The default environment has been installed.
```

</details>