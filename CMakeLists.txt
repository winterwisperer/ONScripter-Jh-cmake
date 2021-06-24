cmake_minimum_required(VERSION 3.10.0)

set(PKG_CONFIG_EXECUTABLE "D:/BuildTools/vcpkg/pkgconfig/bin/pkg-config")
set(CMAKE_TOOLCHAIN_FILE "D:/BuildTools/vcpkg/scripts/buildsystems/vcpkg.cmake")
set(VCPKG_TARGET_TRIPLET "x64-windows-static")

project(onscripter-jh VERSION 1.0)

find_package(SDL2 REQUIRED)
find_package(SDL2-mixer REQUIRED)
find_package(SDL2-image REQUIRED)
find_package(SDL2-ttf REQUIRED)
find_package(Ogg REQUIRED)
find_package(Opus REQUIRED)
find_package(Vorbis REQUIRED)

set(GUI_OBJS  
    src/ONScripter.cpp 
	src/ONScripter_animation.cpp 
	src/ONScripter_command.cpp 
	src/ONScripter_effect.cpp 
	src/ONScripter_effect_breakup.cpp 
	src/ONScripter_event.cpp 
	src/ONScripter_file.cpp 
	src/ONScripter_file2.cpp 
	src/ONScripter_image.cpp 
	src/ONScripter_lut.cpp 
	src/ONScripter_rmenu.cpp 
	src/ONScripter_sound.cpp 
	src/ONScripter_text.cpp 
	src/AnimationInfo.cpp 
	src/FontInfo.cpp 
	src/DirtyRect.cpp 
	src/resize_image.cpp 
	src/ONScripter_directdraw.cpp 
	src/builtin_dll/layer_snow.cpp 
	src/builtin_dll/ONScripter_effect_cascade.cpp 
	src/builtin_dll/ONScripter_effect_trig.cpp 
	src/builtin_dll/layer_oldmovie.cpp
)

set(DECODER_OBJS 
	src/DirectReader.cpp
	src/SarReader.cpp
	src/NsaReader.cpp
	src/sjis2utf16.cpp
	src/coding2utf16.cpp
	src/gbk2utf16.cpp
)

set(ONSCRIPTER_OBJS 
	src/onscripter_main.cpp
	src/ScriptHandler.cpp 
    src/ScriptParser.cpp 
    src/ScriptParser_command.cpp
	${GUI_OBJS}
	${DECODER_OBJS}
   )

set(SARDEC_OBJS 
	src/sardec.cpp
	src/DirectReader.cpp
	src/SarReader.cpp
	src/sjis2utf16.cpp
	src/coding2utf16.cpp
	src/gbk2utf16.cpp
)

set(SARCONV_OBJS 
	src/sarconv.cpp
	src/conv_shared.cpp
	src/resize_image.cpp
	src/DirectReader.cpp
	src/SarReader.cpp
	src/sjis2utf16.cpp
	${DECODER_OBJS}
)

set(NSADEC_OBJS
	src/nsadec.cpp
	${DECODER_OBJS}
)

set(NSACONV_OBJS 
	src/nsaconv.cpp
	src/conv_shared.cpp
	src/resize_image.cpp
	${DECODER_OBJS}
)

set(PARSER_HEADER 
	src/BaseReader.h 
	src/ButtonLink.h 
	src/DirectReader.h 
	src/SarReader.h 
	src/NsaReader.h 
	src/ScriptHandler.h 
	src/ScriptParser.h 
	src/AnimationInfo.h
	src/FontInfo.h 
	src/DirtyRect.h
	src/LUAHandler.h
)

include_directories(${Sdl2_INCLUDE_DIRS})

add_executable(onscripter  ${ONSCRIPTER_OBJS}) 
set_target_properties(onscripter PROPERTIES COMPILE_DEFINITIONS "_CRT_SECURE_NO_WARNINGS;WIN32;USE_OGG_VORBIS;UTF8_CAPTION;USE_SDL_RENDERER")
target_link_libraries(onscripter PRIVATE SDL2::SDL2main SDL2::SDL2-static SDL2::SDL2_mixer SDL2::SDL2_image SDL2::SDL2_ttf Ogg::ogg Opus::opus Vorbis::vorbis Vorbis::vorbisfile )

add_executable(sarconv  ${SARCONV_OBJS}) 
set_target_properties(sarconv PROPERTIES COMPILE_DEFINITIONS "_CRT_SECURE_NO_WARNINGS;WIN32;USE_OGG_VORBIS;UTF8_CAPTION;USE_SDL_RENDERER")
target_link_libraries(sarconv PRIVATE SDL2::SDL2main SDL2::SDL2-static SDL2::SDL2_mixer SDL2::SDL2_image SDL2::SDL2_ttf Ogg::ogg Opus::opus Vorbis::vorbis Vorbis::vorbisfile )

add_executable(nsaconv  ${NSACONV_OBJS}) 
set_target_properties(nsaconv PROPERTIES COMPILE_DEFINITIONS "_CRT_SECURE_NO_WARNINGS;WIN32;USE_OGG_VORBIS;UTF8_CAPTION;USE_SDL_RENDERER")
target_link_libraries(nsaconv PRIVATE SDL2::SDL2main SDL2::SDL2-static SDL2::SDL2_mixer SDL2::SDL2_image SDL2::SDL2_ttf Ogg::ogg Opus::opus Vorbis::vorbis Vorbis::vorbisfile )

add_executable(sardec  ${SARDEC_OBJS}) 
set_target_properties(sardec PROPERTIES COMPILE_DEFINITIONS "_CRT_SECURE_NO_WARNINGS;WIN32;USE_OGG_VORBIS;UTF8_CAPTION;USE_SDL_RENDERER")
target_link_libraries(sardec PRIVATE SDL2::SDL2main SDL2::SDL2-static SDL2::SDL2_mixer SDL2::SDL2_image SDL2::SDL2_ttf Ogg::ogg Opus::opus Vorbis::vorbis Vorbis::vorbisfile )

add_executable(nsadec  ${NSADEC_OBJS}) 
set_target_properties(nsadec PROPERTIES COMPILE_DEFINITIONS "_CRT_SECURE_NO_WARNINGS;WIN32;USE_OGG_VORBIS;UTF8_CAPTION;USE_SDL_RENDERER")
target_link_libraries(nsadec PRIVATE SDL2::SDL2main SDL2::SDL2-static SDL2::SDL2_mixer SDL2::SDL2_image SDL2::SDL2_ttf Ogg::ogg Opus::opus Vorbis::vorbis Vorbis::vorbisfile )

#add_executable(simple_aviplay  simple_aviplay.cpp AVIWrapper.cpp) 
#set_target_properties(nsadec PROPERTIES COMPILE_DEFINITIONS "_CRT_SECURE_NO_WARNINGS;WIN32;USE_OGG_VORBIS;UTF8_CAPTION;USE_SDL_RENDERER")
#target_link_libraries(nsadec PRIVATE SDL2::SDL2main SDL2::SDL2-static SDL2::SDL2_mixer SDL2::SDL2_image SDL2::SDL2_ttf Ogg::ogg Opus::opus Vorbis::vorbis Vorbis::vorbisfile )