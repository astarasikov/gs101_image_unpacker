# Android Google Image Unpacker

Tool to extract meta & packed Google images used in Android devices. These type of images are
mostly used from bootloader and modem images. List of currently supported magic headers are:

1. "46 42 50 4B 02": FBPK v2


## Compile

* Clone this repository
* Install Android NDK if you want to cross-compile for Android devices
* Invoke `make.sh` bash script with desired build target
  * `$ ./make.sh` - if CC not defined from env, gcc is used by default
  * `$ ./make.sh gcc` - compile with gcc
  * `$ ./make.sh clang` - compile with clang
  * `$ ./make.sh cross-android` - cross-compile (arm64-v8a, x86 & x86_64) for Android with NDK
* Executables are copied under the `bin` directory
* For debug builds use `$ DEBUG=true ./make.sh`


## Usage

```
             qc_image_unpacker - ver. 0.1.0
       Anestis Bechtsoudis <anestis@census-labs.com>
  Copyright 2019 - 2020 by CENSUS S.A. All Rights Reserved.

 -i, --input=<path>   : input path (directory to search recursively or single file)
 -o, --output=<path>  : output path (default is same as input)
 -f, --file-override  : allow output file override if already exists (default: false)
 -v, --debug=LEVEL    : log level (0 - FATAL ... 4 - DEBUG), default: '3' (INFO)
 -h, --help           : this help
 ```

### Example of Pixel 6 Google Silicon GS101 bootloader unpack

```
qc_image_unpacker  -i bootloader-oriole-slider-1.0-7683913.img 
[INFO] GS101 FBPK V2 unpacker. Based on qc_image_unpacker by Census Labs
[INFO] Processing 1 file(s) from bootloader-oriole-slider-1.0-7683913.img
[INFO] Number of entries 15
0: ufs (type:0x1 start:0x800 size:0xc5)
[INFO] Partition is smaller than 0x1000 bytes, NOT skipping digest header
1: ufs (type:0x1 start:0xa00 size:0xc5)
[INFO] Partition is smaller than 0x1000 bytes, NOT skipping digest header
2: partition:0 (type:0x1 start:0xc00 size:0xe98)
[INFO] Partition is smaller than 0x1000 bytes, NOT skipping digest header
3: partition:1 (type:0x1 start:0x1c00 size:0x590)
[INFO] Partition is smaller than 0x1000 bytes, NOT skipping digest header
4: partition:2 (type:0x1 start:0x2200 size:0x590)
[INFO] Partition is smaller than 0x1000 bytes, NOT skipping digest header
5: partition:3 (type:0x1 start:0x2800 size:0x150)
[INFO] Partition is smaller than 0x1000 bytes, NOT skipping digest header
6: bl1 (type:0x1 start:0x2a00 size:0x3000)
7: pbl (type:0x1 start:0x5a00 size:0xc000)
8: bl2 (type:0x1 start:0x11a00 size:0x85000)
9: abl (type:0x1 start:0x96a00 size:0x1aa000)
10: bl31 (type:0x1 start:0x240a00 size:0x15000)
11: tzsw (type:0x1 start:0x255a00 size:0x41b000)
12: gsa (type:0x1 start:0x670a00 size:0x40000)
13: ldfw (type:0x1 start:0x6b0a00 size:0x3e8000)
14: ufsfwupdate (type:0x2 start:0xa98a00 size:0x54)
[INFO] Partition is smaller than 0x1000 bytes, NOT skipping digest header
[INFO] 1 known images found from 1 input files
[INFO] Extracted images files are available in '.'
```


## Changelog

* __0.2.0__ - TBC
  * Print size when traversing partition table entries
  * Various code cleanups
* __0.1.0__ - 29 December 2019
  * Initial release


## License

```
   Anestis Bechtsoudis <anestis@census-labs.com>
   Copyright 2019 - 2020 by CENSUS S.A. All Rights Reserved.

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

     http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
```
