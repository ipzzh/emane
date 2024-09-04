1.安装emane构建依赖项（如果有其他进程占用，sudo kill -9 进程号）

sudo apt-get install gcc g++ autoconf automake libtool libxml2-dev libprotobuf-dev \
libpcap-dev libpcre3-dev uuid-dev debhelper pkg-config protobuf-compiler git dh-python \
python3-protobuf python3-setuptools 
 
2.克隆emane存储库

git clone https://github.com/adjacentlink/emane.git
 
3.构建设计

cd emane
./autogen.sh && ./configure && make deb
PYTHON=python3 ./configure --prefix=/usr
 
cd .debbuild
sudo dpkg -i *.deb
sudo apt-get install -f
 
cd emane
cd src/python
sudo make
sudo make install
 
4.安装到core虚拟环境

cd <core绝对路径>/daemon
sudo <poetry的绝对路径> run pip install <EMANE的绝对路径>/src/python
 
cd <EMANE的绝对路径>src/python
PATH=/opt/protoc/bin:$PATH make
sudo core-python -m pip install .

