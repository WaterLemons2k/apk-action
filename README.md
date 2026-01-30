# APK action

Build a signed, release-ready, or debug APKs with GitHub Actions

> Based on [victorbnl/build-signed-apk](https://github.com/victorbnl/build-signed-apk)

## Usage

```yml
- uses: WaterLemons2k/apk-action@v1
  with:
    # Contents of the keystore file (.jks), base64 encoded
    keystore: ${{ secrets.KEYSTORE }}
    # Password of the keystore
    keystore-password: ${{ secrets.KEYSTORE_PASSWORD }}
    # Alias of the key
    key-alias: ${{ secrets.KEY_ALIAS }}
    # Password of the key
    key-password: ${{ secrets.KEY_PASSWORD }}

    # Optioanl
    #
    # The Java version to set up
    # Default: see `src/java-version.js`
    java-version: ''
    # The arguments passed to Gradle
    # Default: '--no-daemon'
    gradle-args: ''
    # Whether to build a release or debug APK
    # Default: 'true'
    release: true
```

## The APK

Default location of the APK:

| `release: true`                                 | `release: false`                            |
| ----------------------------------------------- | ------------------------------------------- |
| `app/build/outputs/apk/release/app-release.apk` | `app/build/outputs/apk/debug/app-debug.apk` |

### Follow-up

Now you can do whatever you want with the APK, such as release it:

```yml
- uses: softprops/action-gh-release@v2
  with:
    files: app/build/outputs/apk/release/*.apk
```

or upload it as an artifact (`release: false`):

```yml
- uses: actions/upload-artifact@v6
  with:
    name: APK
    path: app/build/outputs/apk/debug/*.apk
```

Enjoy it!
