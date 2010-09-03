dnl required version of autoconf
AC_PREREQ([2.53])

dnl package name and package version
AC_INIT([gst-shrtsp],[0.1.0])

dnl required version of gstreamer and gst-plugins-base
GST_REQUIRED=0.10.25

AC_CONFIG_SRCDIR([src/rtsp-shcodecs.c])
AC_CONFIG_HEADERS([config.h])

dnl required version of automake
AM_INIT_AUTOMAKE([1.10])

dnl enable mainainer mode by default
AM_MAINTAINER_MODE([enable])

dnl check for tools (compiler etc.)
AM_PROG_CC_C_O

dnl libtool
dnl LT_PREREQ(2.2.6)
LT_INIT

dnl error out if we can't find pkg-config
AC_CHECK_PROG(HAVE_PKGCONFIG, pkg-config, [ ], [
  AC_MSG_ERROR([You need to have pkg-config installed or set the PATH.])
])

dnl Check for the required version of GStreamer
dnl This will export GST_CFLAGS and GST_LIBS variables for use in Makefile.am
PKG_CHECK_MODULES(GST, [
    gstreamer-0.10              >= $GST_REQUIRED
    gstreamer-base-0.10         >= $GST_REQUIRED
    gstreamer-controller-0.10   >= $GST_REQUIRED
    gstreamer-rtsp-0.10         >= $GST_REQUIRED
  ], [
    AC_SUBST(GST_CFLAGS)
    AC_SUBST(GST_LIBS)
  ], [
  AC_MSG_ERROR([
    Can't find the following GStreamer development packages:
      gstreamer-0.10              >= $GST_REQUIRED
      gstreamer-base-0.10         >= $GST_REQUIRED
      gstreamer-controller-0.10   >= $GST_REQUIRED
      gstreamer-rtsp-0.10         >= $GST_REQUIRED
  ])
])

PKG_CHECK_MODULES(GSTRTSPSERVER, gst-rtsp-server-0.10 >= 0.10.5)


dnl check if compiler understands -Wall (if yes, add -Wall to GST_CFLAGS)
AC_MSG_CHECKING([to see if compiler understands -Wall])
save_CFLAGS="$CFLAGS"
CFLAGS="$CFLAGS -Wall"
AC_COMPILE_IFELSE([AC_LANG_PROGRAM([ ], [ ])], [
  GST_CFLAGS="$GST_CFLAGS -Wall"
  AC_MSG_RESULT([yes])
], [
  AC_MSG_RESULT([no])
])


dnl =======================================================================
dnl Finally, create Makefiles in all directories
dnl =======================================================================

AC_CONFIG_FILES([
Makefile
src/Makefile
])
AC_OUTPUT

