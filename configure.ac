AC_INIT([http-launch], [0.0.1])
AC_CONFIG_SRCDIR([Makefile.am])
AC_CONFIG_HEADERS(config.h)

AM_INIT_AUTOMAKE([dist-bzip2 -Wno-portability])
AM_MAINTAINER_MODE

LT_INIT([pic-only])

m4_ifdef([AM_SILENT_RULES],
  [AM_SILENT_RULES([yes])],
  [
    AM_DEFAULT_VERBOSITY=1
    AC_SUBST(AM_DEFAULT_VERBOSITY)
  ]
)

AC_PROG_CC
AC_PROG_CC_STDC
AC_PROG_CPP
AC_PROG_GREP
AC_PROG_INSTALL
AM_PROG_CC_C_O

AC_HEADER_STDC
AC_C_CONST
AC_C_INLINE
AC_ISC_POSIX
AC_SYS_LARGEFILE

AC_C_BIGENDIAN

AC_CHECK_LIBM
AC_SUBST(LIBM)

PKG_PROG_PKG_CONFIG

PKG_CHECK_MODULES(GST, gstreamer-1.0 >= 1.0.8)
PKG_CHECK_MODULES(GIO, gio-2.0 >= 2.22)

CFLAGS="$CFLAGS -Wall"

AC_ARG_ENABLE(more-warnings,
AC_HELP_STRING([--enable-more-warnings], [Enable more compiler warnings]),
set_more_warnings="$enableval", set_more_warnings=no)

AC_MSG_CHECKING(for more warnings)
if test "$GCC" = "yes" -a "$set_more_warnings" != "no"; then
  AC_MSG_RESULT(yes)
  
  for option in -Wchar-subscripts -Wmissing-declarations -Wmissing-prototypes -Wnested-externs -Wpointer-arith -Wcast-align -Wredundant-decls -Wundef -Wwrite-strings -Wformat-nonliteral -Wformat-security -Wold-style-definition -Winit-self -Wmissing-include-dirs -Waddress -Waggregate-return -Wno-multichar; do
    SAVE_CFLAGS="$CFLAGS"
    CFLAGS="$CFLAGS $option"
    AC_MSG_CHECKING([whether gcc understands $option])
    AC_TRY_COMPILE([], [],
      has_option=yes,
      has_option=no,)
    if test $has_option = no; then
      CFLAGS="$SAVE_CFLAGS"
    fi
    AC_MSG_RESULT($has_option)
    unset has_option
    unset SAVE_CFLAGS
  done
  unset option
else
  AC_MSG_RESULT(no)
fi

AC_ARG_ENABLE(warnings-as-errors,
AC_HELP_STRING([--enable-warnings-as-errors], [Handle compiler warnings as errors]),
set_werror="$enableval", set_werror=no)

AC_MSG_CHECKING(for handling compiler warnings as errors)
if test "$GCC" = "yes" -a "$set_werror" != "no"; then
  AC_MSG_RESULT(yes)
  CFLAGS="$CFLAGS -Werror"
else
  AC_MSG_RESULT(no)
fi

AC_CONFIG_FILES([
  Makefile
  src/Makefile
])

AC_OUTPUT
