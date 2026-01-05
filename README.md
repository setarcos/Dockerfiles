# Dockerfiles used in my pipeline

* rust
* texlive
* tauri-xwin
* debian-dev
* qt5-dev
* qt6-dev
* atc
* tauri

# Building image

The tauri dockerfile can be built with following command to support arm platform. 
```
docker build --platform=linux/arm64 --build-arg NODE_VERSION=24.12.0 -t pi-tauri tauri
```
