<h1 align="center">Jellyfin Tizen</h1>
<h3 align="center">Part of the <a href="https://jellyfin.media">Jellyfin Project</a></h3>

## Build Process

### Getting Started

1. Download and install Tizen Studio (<a href="https://developer.tizen.org/development/tizen-studio/download">https://developer.tizen.org/development/tizen-studio/download</a>).
2. Setup Samsung certificate (need Samsung account).
3. Clone or download this repository.
   ```sh
   git clone https://github.com/jellyfin/jellyfin-tizen.git
   ```
4. Clone or download Jellyfin Web repository.
   ```sh
   git clone https://github.com/jellyfin/jellyfin-web.git
   ```
5. Go to Jellyfin Tizen directory.
   ```sh
   cd jellyfin-tizen
   ```

### Prepare Interface

If any changes are made to `jellyfin-web/`, the `www/` directory will need to be rebuilt using the following command.

```sh
JELLYFIN_WEB_DIR=../jellyfin-web/src npx gulp
```

> If `NODE_ENV=development` is set in the environment, then the source files will be copied without being minified.

> The `JELLYFIN_WEB_DIR` environment variable can be used to override the location of `jellyfin-web`.

### Build WGT

```sh
tizen build-web -e ".*" -e gulpfile.js
tizen package -t wgt -o . -- .buildResult
```

### Deploy to Emulator

1. Run emulator.
2. Install package.
   ```sh
   tizen install -n *.wgt -t T-samsung-5.0-x86
   ```
   > Specify target with `-t` option.

### Deploy to TV

1. Run TV.
2. Activate Developer Mode on TV (<a href="https://developer.samsung.com/tv/develop/getting-started/using-sdk/tv-device">https://developer.samsung.com/tv/develop/getting-started/using-sdk/tv-device</a>).
3. Connect to TV with Device Manager from Tizen Studio. Or with sdb.
   ```sh
   sdb connect YOUR_TV_IP
   ```
4. Install package.
   ```sh
   tizen install -n *.wgt -t UE65NU7400
   ```
   > Specify target with `-t` option.