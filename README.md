# agemobile

Gomobile bind is limited by types and while it allows you to generate identity, you cannot encrypt/decrypt.

This package wraps age library into usable mobile library.

<img src="./misc/android_screenshot.png" width="250">

## Install

### Android

1. Get `age.aar` (You can get `age.aar` from [release page](https://github.com/MarinX/agemobile/releases) or clone the repo and execute `make build-android` to build .aar yourself - Build artifact is located in `build/android` folder.)
2. Add `age.aar` to `libs` folder in your app project
3. Include dependency for Android in `build.gradle`

```gradle
dependencies {
    ...
    // AgeMobile aar from Go
    implementation fileTree(include: ['age.aar'], dir: 'libs')
}
```

### iOS

1. Get `Age.xcframework` (You can get `Age.xcframework` from [release page](https://github.com/MarinX/agemobile/releases) or clone the repo and execute `make build-ios` to build yourself - Build artifact is located in `build/ios` folder.)
2. Copy `Age.xcframework` into iOS project framework folder
3. Import `Age` in Swift

## Usage

### Android

There is an example project in [\_examples/android](./_examples/android/AgeMobile) folder

#### Generate key

```java
import agemobile.Agemobile;

try {
    age.X25519Identity identity = Agemobile.generateX25519Identity();
    String privateKey = identity.string();
    String publicKey = identity.recipient().string();
} catch (Exception e) {
    e.printStackTrace();
}
```

#### Decrypt

```java
import agemobile.Agemobile;

// decrypt text
try {
    String decryptedText = Agemobile.decrypt("age-key/s","with or without armor encrypted text");
} catch (Exception e) {
    e.printStackTrace();
}

// decrypt file
try {
    Agemobile.decrypt("age-key/s","input file to decrypt", "output path where to write decrypted file");
} catch (Exception e) {
    e.printStackTrace();
}
```

#### Encrypt

```java
import agemobile.Agemobile;

// encrypt text
try {
    Agemobile.encrypt("age-keys","text to encrypt");
} catch (Exception e) {
    e.printStackTrace();
}

// encrypt file
try {
    Agemobile.encryptFile("age-keys","input file to encrypt", "output path where to write encrypted file");
} catch (Exception e) {
    e.printStackTrace();
}
```

### iOS

There is an example project in [\_examples/ios](./_examples/ios/AgeMobile) folder

#### Generate Key

```swift
import Age

let identity = AgemobileGenerateX25519Identity(nil)
let privateKey = identity?.string()
let publicKey = identity?.recipient()?.string()

```

#### Encrypt

```swift
import Age

let input = "my secret"
let encrypted = AgemobileEncrypt(identity?.recipient()?.string(), input, true, nil)
```

#### Decrypt

```swift
import Age

let decrypted = AgemobileDecrypt(identity?.string(), encrypted, nil)
```

## Contributing

PR's are welcome. Please read [CONTRIBUTING.md](https://github.com/MarinX/agemobile/blob/main/CONTRIBUTING.md) for more info

## License

MIT
