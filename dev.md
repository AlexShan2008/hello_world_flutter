# Flutter 开发环境的搭建

## Flutter

[Install Flutter SDK](https://flutter.dev/docs/get-started/install)

### Get the Flutter SDK

1. 下载安装 Flutter SDK 安装文件
2. 解压文件
```sh
cd ~/development
unzip ~/Downloads/flutter_macos_1.17.5-stable.zip

```
3. 配置环境变量

```sh
vi ~/.zshrc
# Dart
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn

# flutter flutter 解压
export PATH="$PATH:/Users/alexshan/Documents/development/flutter/bin"
```
4. 重新加载配置文件
```sh
echo $PATH
```
5. 检查环境变量是否配置成功
```
which flutter
```

## Dart

### [Install Dart SDK](https://dart.dev/get-dart)

Mac install by homebrew 

[install homebrew](https://brew.sh/)

```sh
 brew tap dart-lang/dart
 brew install dart
```

问题：

`curl: (35) LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to storage.googleapis.com:443
Error: Failed to download resource "dart"
Download failed: https://storage.googleapis.com/dart-archive/channels/stable/release/2.8.4/sdk/dartsdk-macos-x64-release.zip`

解决办法：
手动下载 sdk

地址就是错误信息返回的地址: https://storage.googleapis.com/dart-archive/channels/stable/release/2.8.4/sdk/dartsdk-macos-x64-release.zip

获取文件的缓存目录：

```sh
github brew --cache
# /Users/alexshan/Library/Caches/Homebrew
```

把刚下载好的软件包拷贝到这个目录下:

```sh
cp ~/Downloads/dartsdk-macos-x64-release.zip /Users/alexshan/Library/Caches/Homebrew
```

我们再执行安装命令，不出意外，那么恭喜你，成功解决了问题。

但凡是也就有意外，不幸的你跟我一样，发现还是报错了:

```sh
brew install dart
==> Installing dart from dart-lang/dart
==> Downloading https://storage.googleapis.com/dart-archive/channels/stable/release/2.4.1/sdk/dartsdk-macos
 
curl: (56) LibreSSL SSL_read: SSL_ERROR_SYSCALL, errno 54
Error: An exception occurred within a child process:
  DownloadError: Failed to download resource "dart"
Download failed: https://storage.googleapis.com/dart-archive/channels/stable/release/2.8.4/sdk/dartsdk-macos-x64-release.zip
```

那该怎么解决？我们给命令加个 -v 打印命令的详细日志看看:

```sh
brew install dart -v
```
注意到这条信息:

```sh
/Users/alexshan/Library/Caches/Homebrew/downloads/cc890b64dedeca4d34ac8849fc5d9aedd2398d0bcd4b4c5b3aeee911fa8c9656--dartsdk-macos-x64-release.zip.incomplete https://storage.googleapis.com/dart-archive/channels/stable/release/2.8.4/sdk/dartsdk-macos-x64-release.zip
```

我们看到 Homebrew 下载 dart 的缓存地址为:

```sh
/Users/shockerli/Library/Caches/Homebrew/downloads/4d2412a5d84521393e0e1ecdce0662569e13c2c47762093a760939fa9dd4a917--dartsdk-macos-x64-release.zip.incomplete
```

XXX.incomplete 表示下载未完成，但这是 Homebrew 期望的下载文件路径。

那我们就将下载的软件包拷贝到这个路径，并去除 .incomplete:

```sh
mv ~/Downloads/dartsdk-macos-x64-release.zip /Users/alexshan/Library/Caches/Homebrew/downloads/cc890b64dedeca4d34ac8849fc5d9aedd2398d0bcd4b4c5b3aeee911fa8c9656--dartsdk-macos-x64-release.zip
```

此时我们再执行安装命令:


#### 升级dart

```sh
brew upgrade dart
```

指定dart版本

```sh
brew switch dart 2.1.0
```

## 创建一个 Flutter app

```sh
flutter create my_app
cd my_app
flutter run
```

## Deploy to iOS devices

Install and set up CocoaPods by running the following commands:

```sh
sudo gem install cocoapods
pod setup
```

## Q&A

1. `[Error: Could not resolve the package 'characters' in 'package:characters/characters.dart'.] after enabling web`

```sh
flutter clean
flutter run
```
