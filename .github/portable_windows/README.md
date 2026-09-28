# Windows portable installer package

The CI workflow builds an installer ZIP containing ComfyUI, the ComfyUI-nunchaku plugin, and setup and launch scripts. Python, PyTorch, and Nunchaku are downloaded during first-time setup. Building the ZIP does not validate dependency installation or GPU inference.

## Build and download

1. Open **Actions → Build Portable Windows Release → Run workflow**.
1. Select the branch and Nunchaku version. Leave **publish_release** disabled; **release_tag** can be empty.
1. After the Windows job succeeds, download the **ComfyUI-nunchaku-portable-v\<version>** artifact from the run page.
1. Extract the artifact, then extract its `ComfyUI_nunchaku_portable_v<version>.zip` into the desired installation directory.

Users can download the CI-built package without running the build script locally.

## First-time setup

Run `install.bat` from the extracted package with an internet connection. After installation succeeds, run `run.bat` to start ComfyUI. If the Nunchaku wheel installation fails, setup exits with an error and does not create the `.installed` marker; resolve the reported error and run `install.bat` again.

## Publish a release

To publish a package, run the workflow with **publish_release** enabled and provide **release_tag**, for example `v1.2.0-portable`. The workflow builds the ZIP, uploads the Actions artifact, and then creates or updates that GitHub Release with the ZIP attached. Publishing with an empty tag fails before the build starts.

With **publish_release** disabled, the workflow only builds and uploads the artifact. It does not create a release or tag.
