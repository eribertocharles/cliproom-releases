# Cliproom Releases

This repository hosts the Sparkle appcast feed and release binaries for [Cliproom](https://github.com/eribertocharles/Cliproom).

## For Users

Cliproom checks for updates automatically. You can also check manually via **Cliproom > Check for Updates**.

## For Developers

### Release Process

1. **Archive the app** in Xcode (Product > Archive)

2. **Export** with Developer ID signing

3. **Create a zip**:
   ```bash
   cd /path/to/exported/app
   zip -r Cliproom-X.Y.Z.zip Cliproom.app
   ```

4. **Sign the zip**:
   ```bash
   /path/to/Sparkle/bin/sign_update Cliproom-X.Y.Z.zip
   ```
   This outputs the `sparkle:edSignature` value.

5. **Get file size**:
   ```bash
   stat -f%z Cliproom-X.Y.Z.zip
   ```

6. **Create GitHub release**:
   ```bash
   gh release create vX.Y.Z Cliproom-X.Y.Z.zip --title "Cliproom X.Y.Z" --notes "Release notes here"
   ```

7. **Update appcast.xml** with new `<item>` entry including:
   - Version numbers
   - Description
   - Publication date
   - Download URL
   - EdDSA signature
   - File size

8. **Commit and push** appcast.xml changes

### Appcast URL

```
https://raw.githubusercontent.com/eribertocharles/cliproom-releases/main/appcast.xml
```
