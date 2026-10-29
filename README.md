# NDS-Game-Builder ZIP workflow

## Use it

1. Upload your project as a `.zip` file into `uploads/`.
2. Commit and push the ZIP to GitHub.
3. Open **Actions → Build Nintendo ZIP**.
4. Download the `Nintendo-Build-*` artifact from the completed run.

The workflow extracts the ZIP, rejects unsafe ZIP paths, inspects the contents, installs devkitPro DS/3DS development packages, builds recognized projects, and uploads produced binaries plus a build report.

## Supported input expectations

- Best results: ZIP contains an existing Makefile and source/assets for a devkitPro DS or 3DS project.
- Common DS markers: `<nds.h>`, libnds Makefile/toolchain references, `.nds` target configuration.
- Common 3DS markers: `<3ds.h>`, libctru Makefile/toolchain references, `.3dsx` target configuration.
- Source-only archives without an identifiable target are deliberately stopped with an explanation rather than silently compiling for the wrong platform.
- CIA packaging is included only if the project already defines a working CIA target and has the required metadata/packaging setup. A CIA cannot be made by renaming a 3DSX.

## Important limitations

This is an automatic ZIP intake and build workflow, not a magical converter for arbitrary data. Raw assets alone are not executable. Multiple Makefiles, custom dependency trees, submodules, generated assets, and platform-specific code may require project-specific configuration. Review the workflow and only build ZIPs you trust.

## Files

- `.github/workflows/compile.yml`: ZIP detection/build workflow.
- `uploads/`: place ZIPs here; do not extract them yourself.
