set(SRCROOT ${PROJECT_SOURCE_DIR}/src/cpp3ds/Audio)

set(SRC
    ${SRCROOT}/AlResource.cpp
    ${SRCROOT}/InputSoundFile.cpp
    ${SRCROOT}/Music.cpp
    ${SRCROOT}/OutputSoundFile.cpp
    ${SRCROOT}/Sound.cpp
    ${SRCROOT}/SoundBuffer.cpp
    ${SRCROOT}/SoundBufferRecorder.cpp
    ${SRCROOT}/SoundFileFactory.cpp
    ${SRCROOT}/SoundFileReaderWav.cpp
    ${SRCROOT}/SoundFileWriterWav.cpp
    ${SRCROOT}/SoundRecorder.cpp
    ${SRCROOT}/SoundSource.cpp
    ${SRCROOT}/SoundStream.cpp
)

if(ENABLE_OGG)
    find_package(Vorbis REQUIRED)
    include_directories(${VORBIS_INCLUDE_DIRS})
    list(APPEND SRC
        ${SRCROOT}/SoundFileReaderOgg.cpp
        ${SRCROOT}/SoundFileWriterOgg.cpp)
endif()
if(ENABLE_MP3)
	find_package(mpg123 REQUIRED)
	include_directories(${MPG123_INCLUDE_DIRS})
    list(APPEND SRC
        ${SRCROOT}/SoundFileReaderMp3.cpp)
endif()

add_cpp3ds_library(cpp3ds-audio
                   SOURCES ${SRC}
                   DEPENDS cpp3ds-system)
