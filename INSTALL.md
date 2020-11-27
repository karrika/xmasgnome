The Game Blender tools are not available from Raspi OS directly.
So we must compile them by ourselves.

sudo apt update
sudo apt install build-essential git subversion cmake libx11-dev libxxf86vm-dev libxcursor-dev libxi-dev libxrandr-dev libxinerama-dev libglew-dev
sudo apt -y install gcc-7 g++-7
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 7
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 7
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 8
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-8 8
sudo update-alternatives --config gcc
(choose version 7)
sudo update-alternatives --config g++
(choose version 7)
cd
git clone -b upbge0.2.5 https://github.com/UPBGE/upbge.git
cd upbge
git submodule sync
git submodule update --init --recursive --remote
git submodule foreach git checkout master
git submodule foreach git pull --rebase origin master
./build_files/build_environment/install_deps.sh --skip-ocio --skip-oiio --skip-osl --skip-alembic
make update
make -j4 BUILD_CMAKE_ARGS="-U *SNDFILE* -U *PYTHON* -U *BOOST* -U *Boost* -U *OPENCOLORIO* -U *OPENEXR* -U *OPENIMAGEIO* -U *LLVM* -U *CYCLES* -U *OPENSUBDIV* -U *OPENVDB* -U *COLLADA* -U *FFMPEG* -U *ALEMBIC* -D WITH_CODEC_SNDFILE=ON -D PYTHON_VERSION=3.5 -D WITH_CYCLES_OSL=OFF -D WITH_CYCLES=OFF -D WITH_LLVM=OFF -D WITH_OPENSUBDIV=ON -D OPENSUBDIV_ROOT_DIR=/opt/lib/osd -D WITH_OPENVDB=ON -D WITH_OPENVDB_BLOSC=ON -D WITH_CODEC_FFMPEG=OFF -D FFMPEG_LIBRARIES='avformat;avcodec;avutil;avdevice;swscale;swresample;lzma;rt;theora;theoradec;theoraenc;vorbis;vorbisenc;vorbisfile;ogg;x264;openjpeg;openjpeg_JPWL'"
