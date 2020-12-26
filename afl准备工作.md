## 安装AFL

```shell 
git clone https://github.com/google/AFL.git
cd AFL
git checkout v2.55b
make
cd llvm-mode
make
cd ..
sudo make install
```

注意：高版本AFL有坑，使用`afl-clang-fast`编译目标软件的时候需要使用v2.55b版本来搞，不然报重复定义错误

## 编译ImageMagick

```shell
git clone https://github.com/ImageMagick/ImageMagick.git
cd ImageMagick
CC="afl-clang-fast" CXX="afl-clang-fast++" ./configure # 实际上`afl-clang-fast`和`afl-clang-fast++`是同一个文件
make
sudo make install
```

## 准备运行AFL

```shell
cd utilities
mkdir fuzzing_input fuzzing_output
cp ../logo.gif fuzzing_input
afl-fuzz -i fuzzing_input -o fuzzing_output -t 1000 -m 200 magick convert @@ /dev/null
```







