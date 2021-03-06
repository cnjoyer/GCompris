# Passthrough, do not break uplevel make rule
install-activity:

## Process this file with automake to produce Makefile.in
if PYTHON_PLUGIN
python_ldadd = $(PYTHON_LIBS)
python_ldflags = -u Py_Initialize
else
python_ldadd =
python_ldflags =
endif

if USE_SQLITE
sqlite_ldadd = $(SQLITE3_LIBS)
sqlite_cflags = $(SQLITE3_CFLAGS)
else
sqlite_ldadd =
sqlite_cflags =
endif

if PLATFORM_WIN32
no_undefined = -no-undefined
shared = -shared
else
no_undefined =
shared =
endif

bin_PROGRAMS = gcompris

INCLUDES = \
	-I$(top_srcdir)/intl \
	-DDATADIR=\""$(datadir)"\" \
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/src/goocanvas/src \
	$(GCOMPRIS_CFLAGS) \
	$(GNOME_INCLUDEDIR) \
	$(XML_CFLAGS) \
	-DGNOME_DISABLE_DEPRECATED \
        $(sqlite_cflags) \
	$(GNET_CFLAGS) \
	$(AUDIO_CFLAGS) \
	$(cairo_cflags) \
	${GTK_MAC_CFLAGS}

gcompris_SOURCES = \
	$(cairo_c) \
	$(cairo_h) \
	about.c \
	about.h \
	anim.c \
	anim.h \
	bar.c \
	bar.h \
	binreloc.c \
	binreloc.h \
	board.h board.c \
	board_config_common.c board_config_common.h \
	board_config_combo.c board_config_radio.c\
	board_config_textview.c board_config_wordlist.c \
	board_config.h board_config.c \
	bonus.c \
	bonus.h \
	config.c \
	dialog.c \
	drag.c \
	drag.h \
	file_selector.c \
	gameutil.c \
	gameutil.h \
	gc_core.h \
	gcompris-board.h \
	gcompris.c \
	gcompris.h \
	gcompris_alphabeta.c \
	gcompris_alphabeta.h \
	gcompris_config.h \
	gcompris_confirm.c \
	gcompris_db.c \
	gcompris_db.h \
	gcompris_im.c \
	gcompris_im.h \
	help.c \
	images_selector.c \
	log.c \
	menu.c \
	pixbuf_util.c \
	pixbuf_util.h \
	plugin.h \
	profile.c \
	profile.h \
	properties.c \
	properties.h \
	score.c \
	score.h \
	skin.c \
	skin.h \
	soundutil.c \
	soundutil.h \
	status.c \
	status.h \
	gstreamer.c \
	soundutil_sdl.c \
	soundutil_sdl.h \
	sdlplayer.c \
	timer.c \
	timer.h \
	wordlist.c \
	wordlist.h

gcompris_LDFLAGS = \
	-export-dynamic $(cairo_ldflags)


gcompris_LDADD = \
	$(top_builddir)/src/goocanvas/src/libgoocanvas.la \
	$(GCOMPRIS_LIBS) $(sqlite_ldadd) $(XML_LIBS) $(GNET_LIBS) \
	$(AUDIO_LIBS) \
        $(INTLLIBS) \
	${GTK_MAC_LIBS}

marshal_sources =				\
	gc-marshal.c				\
	gc-marshal.h

BUILT_SOURCES =					\
	$(marshal_sources)

gc-marshal.c: gc-marshal.list
	$(GLIB_GENMARSHAL) --prefix=gc_marshal $< --header --body > $@

gc-marshal.h: gc-marshal.list
	$(GLIB_GENMARSHAL) --prefix=gc_marshal $< --header > $@

EXTRA_DIST = \
	Makefile.mingw gcomprisrc.rc \
	gc-marshal.list

DONT_DIST_SOURCE = $(marshal_sources)

if SUGAR
INCLUDES += $(SUGAR_CFLAGS)
gcompris_SOURCES += \
	sugar.c sugar.h \
	sugar_gc.c sugar_gc.h \
	sugar_cli.c \
	sugar_srv.c \
	sugar_share.c sugar_share.h \
	sugar_db.h
gcompris_LDADD += $(SUGAR_LIBS)
if USE_SQLITE
gcompris_SOURCES += sugar_db.c
endif
endif
