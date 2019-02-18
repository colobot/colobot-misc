# We need the latest version of Ubuntu, the current release doesn't have the latest version of GCC8 which has even more warnings
FROM ubuntu:devel

MAINTAINER TerranovaTeam <contact@colobot.info>

# Set up colobot build environment, including GCC8 so that we catch the latest warnings
RUN apt update && apt install -y --no-install-recommends build-essential cmake libsdl2-dev libsdl2-image-dev libsdl2-ttf-dev libsndfile1-dev libvorbis-dev libogg-dev libpng-dev libglew-dev libopenal-dev libboost-dev libboost-system-dev libboost-filesystem-dev libboost-regex-dev libphysfs-dev gettext git po4a vorbis-tools librsvg2-bin xmlstarlet gcc-8 g++-8
ENV CC gcc-8
ENV CXX g++-8

# wtf, how is that not installed by default, "git clone" fails without it
RUN apt install -y --no-install-recommends ca-certificates

# Set up MXE
RUN apt install -y --no-install-recommends autoconf automake autopoint bison flex gperf intltool libtool libtool-bin python ruby scons unzip wget p7zip-full libgtk2.0-dev lzip && git clone https://github.com/mxe/mxe.git /opt/mxe

# see https://github.com/colobot/colobot/issues/1196
COPY 0001-Revert-sdl2-build-with-libsamplerate-support.patch /usr/src/0001-Revert-sdl2-build-with-libsamplerate-support.patch
RUN cd /opt/mxe && git apply /usr/src/0001-Revert-sdl2-build-with-libsamplerate-support.patch

RUN cd /opt/mxe && make -j9 binutils boost bzip2 cairo dbus expat flac fontconfig freetype gcc gettext glew glib harfbuzz icu4c jpeg libffi libiconv libpng libsndfile libwebp lzo mingw-w64 ogg openal pcre physfs pixman pkgconf portaudio sdl2 sdl2_image sdl2_ttf tiff vorbis xz zlib

RUN apt install -y --no-install-recommends patchelf doxygen graphviz
