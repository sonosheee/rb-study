# RB-VISION-GUI

* **Qt Creator, Visual Studio, VS Code**에서 모두 이용 가능한 프로젝트.

## Features
* 물체의 중심좌표 및 각도 추출 (Image and Stream)
* 웹캠 캡쳐 기능
* 캘리브레이션 기능(Intrinsic, and Extrinsic)
* 컬러 인식 (Red, Green, Blue, Yellow)
* 협동로봇 소켓통신


## Tested Machine and IDE

* Desktop - Windows 10 Pro
  * Visual Studio 2019
  * Visual Studio 2017
  * VS code(using MinGW)
  * Qt Creator5.14.1 (using MSVC and MinGW)

* Laptop - Windows 10 Enterprise
  * Visual Studio 2019
  * Visual Studio 2017
  * VS code(using minGW)
  * Qt Creator5.14.3 (using MSVC and MinGW)
  
* Rapberry Pi 4 - Raspbian(Debian) 
  * Qt Creator 5.11.3 (using GCC)

## Dependency

* OpenCV  
  * OpenCV 4.1.2 (MSVC 15 이상, MinGW) -> [Download](https://drive.google.com/file/d/1VYrfwCyywHqawlOrp3KnaG1CN8ZRJ88e/view?usp=sharing)
  * OpenCV 4.3.0 (MSVC 15 이상) -> [Download](https://drive.google.com/file/d/1_Z6FgMc3f8aO4V8XGiv6dRD4D-Mc9N9t/view?usp=sharing)
  * OpenCV 4.1.2 (GCC) -> [참조](https://make.e4ds.com/make/learn_guide_view.asp?idx=116)


* OpenCV 3 이상이면 버전은 크게 상관이 없으며, 현재 테스트 된 버전은 아래와 같음.
* OpenCV 홈페이지에서 이미 빌드된 라이브러리를 다운 받는다면, 추가적인 CMake과정이 요구됨(nonfree 모듈을 포함하여 build)  
  
  
## Usage
### 1. Git (CLI 기반 저장소 복제)
* 해당 [Link](https://git-scm.com/) 에서 git 다운로드.
* 아래의 명령어를 통해 사용자 정보 설정(GitHub 정보와 동일하게 설정할 것을 추천)
* 지역옵션은 현재 저장소에 유효한 설정, 전역옵션은 현재 사용자에 유효한 옵션, 시스템옵션은 PC 전체 사용자에 유효한 옵션
* 우선순위는 **지역옵션>전역옵션>시스템옵션**

```shell
git config --global user.name "이름"
git config --global user.email "이메일"
```

* 사용자 설정 후 로컬 저장소로 복제함.

```shell
git clone "저장소 주소" "폴더명"
```

* 해당 repo는 아래의 명령어를 통해서 복제 가능함.
* 폴더명을 따로 지정하지 않으면, 현재 repo의 이름으로 폴더가 생성됨.
```shell
git clone https://github.com/messy-snail/rb-vision-gui.git
```

* 해당 repo 주소는 아래의 그림 위치에서 확인 가능함.

![image](https://user-images.githubusercontent.com/38720524/79522581-0c1f0d00-8097-11ea-8412-d75f69c2332b.png)



### 2. Qt Creator(Windows)에서의 사용법
* MSVC도 컴파일 가능하기는 하지만 **minGW**로 컴파일하는 것을 추천함.
* 복제된 저장소에서 *.pro 파일을 이용하여 qt 프로젝트를 불러옴.
* *.pro파일에서 opencv에 대해 include와 library에 대해 설정이 필요함.
* 코드 수정없이 사용하기 위해서는 해당 [라이브러리](https://drive.google.com/file/d/1VYrfwCyywHqawlOrp3KnaG1CN8ZRJ88e/view?usp=sharing)를 사용하는 것을 추천함.
* common412폴더 안의 minGW폴더를 common 폴더로 이름을 변경하고, *.pro와 같은 위치에 배치하면 바로 사용가능함.

```c++
win32:CONFIG(release, debug|release): LIBS += -L$$PWD/common/lib/ -lopencv_world412
else:win32:CONFIG(debug, debug|release): LIBS += -L$$PWD/common/lib/ -lopencv_world412d

INCLUDEPATH += $$PWD/common/include
DEPENDPATH += $$PWD/common/include
```

* PWD는 현재 working directory를 의미함.
* 다른 버전의 opencv를 사용하고자 한다면, nonfree 모듈을 포함하여 CMake 후 사용하면 됨.
* CMake 시 **world 모듈**을 포함하는 것이 사용에 편리함.그렇지 않으면 무수히 많은 라이브러리를 기술하여야함.


### 3. Qt Creator(Raspberry Pi)에서의 사용법
* 앞서 윈도우에서의 방법과 동일함.
* **world 모듈**을 포함하여 빌드하지 않아서 라이브러리의 수가 많음.

```c++
INCLUDEPATH +=-I/usr/local/include/opencv4
LIBS +=-L/usr/local/lib -lopencv_gapi -lopencv_stitching -lopencv_aruco -lopencv_bgsegm -lopencv_bioinspired -lopencv_ccalib -lopencv_cvv -lopencv_dnn_objdetect -lopencv_dnn_superres -lopencv_dpm -lopencv_highgui -lopencv_face -lopencv_freetype -lopencv_fuzzy -lopencv_hfs -lopencv_img_hash -lopencv_line_descriptor -lopencv_quality -lopencv_reg -lopencv_rgbd -lopencv_saliency -lopencv_stereo -lopencv_structured_light -lopencv_phase_unwrapping -lopencv_superres -lopencv_optflow -lopencv_surface_matching -lopencv_tracking -lopencv_datasets -lopencv_text -lopencv_dnn -lopencv_plot -lopencv_videostab -lopencv_video -lopencv_videoio -lopencv_xfeatures2d -lopencv_shape -lopencv_ml -lopencv_ximgproc -lopencv_xobjdetect -lopencv_objdetect -lopencv_calib3d -lopencv_imgcodecs -lopencv_features2d -lopencv_flann -lopencv_xphoto -lopencv_photo -lopencv_imgproc -lopencv_core
```

### 4. Visual Studio 2019에서의 사용법
* Visual Studio를 이용하면, OpenCV 디버깅에 용이함.
* 코드 수정없이 사용하기 위해서는 해당 [라이브러리](https://drive.google.com/file/d/1VYrfwCyywHqawlOrp3KnaG1CN8ZRJ88e/view?usp=sharing)를 사용하는 것을 추천함.
* common412폴더를 common 폴더로 이름을 변경하고, *.sln과 같은 위치에 배치하면 바로 사용가능함.
  
* OpenCV include path : 속성-C/C++-일반-추가 포함 디렉토리
```
common/include
```
* OpenCV lib path : 링커-일반-추가 라이브러리 디렉토리
```
common/lib
```
* OpenCV lib file : 링커-입력-추가 종속성 ()
```shell
$(debug) opencv_world412d.lib
$(release) opencv_world412.lib 
```


### 5. VS Code에서의 사용법
* VS Code를 이용하면, 다양한 extension 활용에 용이함.
* 코드 수정없이 사용하기 위해서는 해당 [라이브러리](https://drive.google.com/file/d/1VYrfwCyywHqawlOrp3KnaG1CN8ZRJ88e/view?usp=sharing)를 사용하는 것을 추천함.
* common412폴더 안의 minGW폴더를 common 폴더로 이름을 변경하고, 소스 코드와 같은 위치에 배치하면 바로 사용가능함.
* VS Code는 텍스트 에디터로 컴파일러를 직접 설정하여 사용해야함.
* Intellisense를 활성화하기 위해서 **c_cpp_properties.json**을 수정해야함.
* **Ctrl+Shift+P**를 입력하고, C/C++: Edit Configuration을 선택함.

![image](https://user-images.githubusercontent.com/38720524/79541752-5b7c3200-80c5-11ea-84e9-290ea1bf8ec6.png)


* JSON을 선택하면 includePath에 원하는 디렉토리를 입력하면 됨.
* 해당 예시에서는 OpenCV와 Qt를 설정해주었음.
* Qt의 경우 본인의 설치 경로와 맞는지 확인해야할 필요가 있음.
* path의 경우 full path를 권장하며, 상대경로를 이용하고자 한다면, ```${workspaceFolder}``` 매크로를 이용할 것.

```json
{
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceFolder}/**",
                "C:/Users/hansol/source/repos/common/minGW/include",
                "C:/Qt/Qt5.14.2/5.14.2/mingw73_64/include/QtWidgets",
                "C:/Qt/Qt5.14.2/5.14.2/mingw73_64/include",
                "C:/Qt/Qt5.14.2/5.14.2/mingw73_64/include/QtCore"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "windowsSdkVersion": "10.0.18362.0",
            "compilerPath": "C:/Program Files (x86)/Microsoft Visual Studio/2019/Community/VC/Tools/MSVC/14.25.28610/bin/Hostx64/x64/cl.exe",
            "cStandard": "c11",
            "cppStandard": "c++17",
            "intelliSenseMode": "msvc-x64",
            "configurationProvider": "vector-of-bool.cmake-tools"
        }
    ],
    "version": 4
}
```

* JSON이 익숙하지 않은 유저는 UI에서도 수정이 가능함.  

![image](https://user-images.githubusercontent.com/38720524/79542138-10165380-80c6-11ea-92d4-75315ad3e996.png)

* **Ctrl+Shift+P**를 입력하고, Tasks: Configuration Default Build Task를 선택함.
* 만약 MinGW이외에 MSVC를 사용하고자 한다면, "command"와 "args"를 수정 작성하여야함.

![image](https://user-images.githubusercontent.com/38720524/79545027-f0cdf500-80ca-11ea-8a19-430f10b1d1b5.png)


```json
{
    "version": "2.0.0",
    "runner": "terminal",
    "type": "shell",
    "echoCommand": true,
    "presentation" : { "reveal": "always" },
    "tasks": [
          //C++ 컴파일
          {
            "label": "minGW for C++",
            "command": "cd ${workspaceRoot} && cmake . -G \"MinGW Makefiles\" && mingw32-make",
            "group": "build",

            "problemMatcher": {
                "fileLocation": [
                    "relative",
                    "${workspaceRoot}"
                ],
                "pattern": {
                    "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning error):\\s+(.*)$",
                    "file": 1,
                    "line": 2,
                    "column": 3,
                    "severity": 4,
                    "message": 5
                }
            }
        },
        // 바이너리 실행(Windows)
        {
            "label": "execute",
            "command": "cmd",
            "group": "test",
            "args": [
                "/C", "${fileDirname}\\${workspaceFolderBasename}"
            ]
        }
    ]
}
```

* 혹시 ```&&```라는 명령어가 없다는 에러가 발생한다면, 기본 쉘을 cmd로 변경할 것.
* **Ctrl+Shift+P**를 누르고 ```>Terminal: Select Default Shell```를 입력.
* CMakeLists.txt도 본인의 경로에 맞게 수정이 요구됨.

```cmake
cmake_minimum_required(VERSION 3.5)

project(rb-vision-gui LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_PREFIX_PATH C:/Qt/Qt5.14.2/5.14.2/mingw73_64)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(pathOPENCV C:/Users/hansol/source/repos/common/minGW)
include_directories(${pathOPENCV}/include)
set(LIBOPENCV ${pathOPENCV}/lib/libopencv_world412.dll.a)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt5 COMPONENTS Widgets Network REQUIRED)
file (GLOB SOURCES 
    *.cpp
    *.h)
if(ANDROID)
  add_library(qt-cmake-test SHARED
    main.cpp
    mainwindow.cpp
    mainwindow.h
    mainwindow.ui
  )
else()
  add_executable(rb-vision-gui
    main.cpp
    mainwindow.cpp
    mainwindow.h
    mainwindow.ui
    main.qrc
    CommonHeader.h
    VisionModule.h
    VisionModule.cpp
    LAN/RBLANCommon.h
    LAN/RBTCPServer.cpp
    LAN/RBTCPServer.h

  )
endif()

target_link_libraries(rb-vision-gui PRIVATE Qt5::Widgets Qt5::Network ${LIBOPENCV})

```

* Qt와 OpenCV 경로에 대한 확인이 필요함. 자세한 내용은 아래와 같음.

```cmake
set(CMAKE_PREFIX_PATH C:/Qt/Qt5.14.2/5.14.2/mingw73_64)

set(pathOPENCV C:/Users/hansol/source/repos/common/minGW)
include_directories(${pathOPENCV}/include)
set(LIBOPENCV ${pathOPENCV}/lib/libopencv_world412.dll.a)
```

* 설정이 끝났다면, **Ctrl+Shift+B**를 눌러서 정상적으로 빌드가 되는지 확인하면 됨.