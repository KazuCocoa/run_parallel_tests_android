## Run tests against available devices/emulators
### Apks
- https://github.com/googlesamples/android-testing/blob/master/ui/espresso/BasicSample

```
$ ./gradlew assemble # include assembleDebug and assembleDebugAndroidTest
```

You can use apks under `apks/`

### Create emulators
- https://github.com/gojuno/swarmer

```
java -jar bin/swarmer-0.2.0.jar start \
--emulator-name Nexus_5_API_23 \
--package "system-images;android-25;google_apis;x86_64" \
--android-abi google_apis/x86_64 \
--path-to-config-ini avd_configs/Nexus_5_API_23.ini \
--emulator-start-options -prop persist.sys.language=en -prop persist.sys.country=US \
--emulator-name Nexus_5X_API_25 \
--package "system-images;android-23;default;x86" \
--android-abi default/x86 \
--path-to-config-ini avd_configs/Nexus_5X_API_25.ini \
--emulator-start-options -prop persist.sys.language=en -prop persist.sys.country=US \
```

### Run instruments tests
- https://github.com/gojuno/composer

#### with sharding
- Run 1 test suite with multiple devices. "Shared"
    - You can run tests fast.

```
java -jar bin/composer-0.2.4.jar \
--apk apks/app-debug.apk \
--test-apk apks/app-debug-androidTest.apk \
--test-package com.example.android.testing.espresso.BasicSample.test \
--test-runner android.support.test.runner.AndroidJUnitRunner \
--output-directory artifacts/composer-output \
--verbose-output false
--shard true
```

#### without sharding

```
java -jar composer-0.2.4.jar \
--apk apks/app-debug.apk \
--test-apk apks/app-debug-androidTest.apk \
--test-package com.example.android.testing.espresso.BasicSample.test \
--test-runner android.support.test.runner.AndroidJUnitRunner \
--output-directory artifacts/composer-output \
--verbose-output false
--shard false
```

#### for multiple languages
- https://github.com/KazuCocoa/DroidTestHelper
- https://github.com/linkedin/test-butler

### Stop all emulators

```
java -jar bin/swarmer-0.2.0.jar stop
```
