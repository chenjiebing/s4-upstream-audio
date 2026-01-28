# s4-upstream-audio
base on https://patchwork.kernel.org/project/linux-amlogic/list/?series=1046918
First, apply the first patch(0001-Add-DRM-support-for-Amlogic-S4).
and apply 0002-ASoC-meson-add-s4-tohdmitx-control

buildin deconfig
+CONFIG_DRM=y
+CONFIG_DRM_DISPLAY_CONNECTOR=y
+CONFIG_DRM_MESON_DW_HDMI=y
+CONFIG_DRM_MESON=y
+CONFIG_SOUND=y
+CONFIG_SND=y
+CONFIG_SND_SOC=y
+CONFIG_SND_SOC_SIMPLE_AMPLIFIER=y
+CONFIG_SND_MESON_AXG_SOUND_CARD=y
+CONFIG_SND_MESON_G12A_TOHDMITX=y
+CONFIG_COMMON_CLK_AXG_AUDIO=y

test cmd
amixer cset numid=44,iface=MIXER,name='FRDDR_A SINK 1 SEL' 1
amixer cset numid=77,iface=MIXER,name='TDMOUT_B SRC SEL' 0
amixer cset numid=41,iface=MIXER,name='FRDDR_A SRC 1 EN Switch' 1
amixer cset numid=1,iface=MIXER,name='TOACODEC Lane Select' 0
amixer cset numid=66,iface=MIXER,name='TOACODEC SRC' 1
amixer cset numid=67,iface=MIXER,name='TOACODEC OUT EN Switch' 1
amixer cset numid=17,iface=MIXER,name='ACODEC Playback Volume' 251 251
amixer cset numid=63,iface=MIXER,name='TOHDMITX I2S OUT EN Switch' 1
amixer cset numid=62,iface=MIXER,name='TOHDMITX I2S SRC' 1

aplay bbg.wav -Dhw:0,0 --period-size=1024 --buffer-size=4096
