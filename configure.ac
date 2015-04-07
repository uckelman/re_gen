# Process this file with autoconf to produce a configure script.
# TODO: Unknown whether 2.64 works; was a bit of a milestone release, though
AC_PREREQ([2.64])
# TODO: required versions for automake, libtool?

AC_INIT([re_gen], [0.1], [joel@lightboxtechnologies.com])

# Set the default C and C++ compilation flags to nothing.
# Do this immediately after AC_INIT, as other macros might invoke
# AC_PROG_CC or AC_PROG_CXX and stomp our defaults.
: ${CFLAGS=''}
: ${CXXFLAGS=''}

## FIXME: Argh, there appears to be no way to distinguish between the
## flags set by mingw64-configure and ones set by the user...
#AC_MSG_NOTICE([Default CPPFLAGS: $CPPFLAGS])
#AC_MSG_NOTICE([Default CFLAGS:   $CFLAGS])
#AC_MSG_NOTICE([Default CXXFLAGS: $CXXFLAGS])
#AC_MSG_NOTICE([Default LDFLAGS:  $LDFLAGS])

AC_CONFIG_AUX_DIR([config])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_SRCDIR([src/forms.cpp])
AC_CONFIG_HEADERS([config.h])

#AM_INIT_AUTOMAKE([1.12 foreign serial-tests subdir-objects])
AM_INIT_AUTOMAKE([foreign subdir-objects])
LT_INIT

#
# metadata
#

# Decompose the version number.
#
# We must do this rather than construct PACKAGE_VERSION from the components
# because AC_INIT rejects anything but a literal for the version number.
PACKAGE_VERSION_MAJOR=`echo "$PACKAGE_VERSION" | cut -d. -f1`
PACKAGE_VERSION_MINOR=`echo "$PACKAGE_VERSION" | cut -d. -f2`
PACKAGE_VERSION_MICRO=`echo "$PACKAGE_VERSION" | cut -d. -f3`

AC_SUBST([PACKAGE_VERSION_MAJOR])
AC_SUBST([PACKAGE_VERSION_MINOR])
AC_SUBST([PACKAGE_VERSION_MICRO])

AC_DEFINE_UNQUOTED(PACKAGE_VERSION_MAJOR, $PACKAGE_VERSION_MAJOR, [Define to the major version of this package.])
AC_DEFINE_UNQUOTED(PACKAGE_VERSION_MINOR, $PACKAGE_VERSION_MINOR, [Define to the minor version of this package.])
AC_DEFINE_UNQUOTED(PACKAGE_VERSION_MICRO, $PACKAGE_VERSION_MICRO, [Define to the micro version of this package.])

PACKAGE_YEAR=`date +%Y`

AC_SUBST([PACKAGE_YEAR])
AC_DEFINE_UNQUOTED(PACKAGE_YEAR, $PACKAGE_YEAR, [Define to the current year.])

PACKAGE_COMPANY="Lightbox Technologies, Inc."

AC_SUBST([PACKAGE_COMPANY])
AC_DEFINE_UNQUOTED(PACKAGE_COMPANY, "$PACKAGE_COMPANY", [Define to the owner of this package.])

PACKAGE_DESCRIPTION="not the worst forensics regexp engine"
AC_SUBST([PACKAGE_DESCRIPTION])
AC_DEFINE_UNQUOTED(PACKAGE_DESCRIPTION, "$PACKAGE_DESCRIPTION", [Define to the description of this package.])

#
# common
#
AC_PROG_CC
AC_PROG_CXX
AM_PROG_CC_C_O

AC_LANG([C++])
AX_CXX_COMPILE_STDCXX_11([noext], [mandatory])
AX_APPEND_COMPILE_FLAGS([-W -Wall -Wextra -Wnon-virtual-dtor -pedantic -pipe -O3], [LG_CXXFLAGS])

AC_PROG_INSTALL

# FIXME: mingw defaults to -g -O2, along with a bunch of other flags which
# we want to keep.
case "$host" in
*-*-mingw*)
  LG_REMOVE_FLAGS([CFLAGS], ['-O2'])
  LG_REMOVE_FLAGS([CXXFLAGS], ['-O2'])
  ;;
esac

AC_SUBST([LG_CXXFLAGS])
AC_SUBST([LG_LDFLAGS])

#
# Cleanup flags
#

AC_MSG_NOTICE([CC:       $CC])
AC_MSG_NOTICE([CXX:      $CXX])
AC_MSG_NOTICE([CPPFLAGS: $CPPFLAGS])
AC_MSG_NOTICE([CFLAGS:   $CFLAGS])
AC_MSG_NOTICE([CXXFLAGS: $CXXFLAGS])
AC_MSG_NOTICE([LIBS:     $LIBS])
AC_MSG_NOTICE([LDFLAGS:  $LDFLAGS])

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
