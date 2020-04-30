# webrtc-m76-vs2017
webrtc m76 vs2017版本
编译说明：
一.支持h264 改动了如下地方：
1.src\modules\video_coding\codecs\h264文件夹下的h264_color_space.h，h264_decoder_impl.h，h264_encoder_impl.h
头文件中的error "See: bugs.webrtc.org/9213#c13." 注释掉
2.src\third_party\ffmpeg\libavcodec\pcm.c 注释掉此行  PCM_CODEC  (PCM_VIDC,         AV_SAMPLE_FMT_S16, pcm_vidc,         "PCM Archimedes VIDC");
3.src\third_party\ffmpeg\libavcodec\fft_template.c 修改了宏定义 具体 见该文件
4.修改了ffmpeg编译脚本C:\webrtc\webrtc-checkout\src\third_party\libyuv\BUILD.gn
注释掉了libyuv_internal(//build/toolchain/win:win_clang_x64 因为使用is_clang=false 时 默认是编码clang版本的yuv库，导致链接后的文件不能启动

二.编译选项说明：
1.debug版本
gn gen out/Debug64 --ide=vs2017 --args=" is_clang=false use_rtti=true rtc_include_tests=false rtc_libvpx_build_vp9=true enable_iterator_debugging=true 
symbol_level=0 proprietary_codecs=true is_debug=true  rtc_build_tools=false rtc_build_examples=false ffmpeg_branding=\"Chrome\"  rtc_use_h264=true rtc_include_tests=false"

ninja -C  out/Debug64

2.release版本
gn gen out/Release64 --ide=vs2017 --args=" is_clang=false use_rtti=true rtc_include_tests=false rtc_libvpx_build_vp9=true enable_iterator_debugging=true 
symbol_level=0 proprietary_codecs=true is_debug=false  rtc_build_tools=false rtc_build_examples=false ffmpeg_branding=\"Chrome\"  rtc_use_h264=true rtc_include_tests=false"

ninja -C  out/Release64


