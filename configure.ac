#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_INIT([libg15render],[3.0.4],[dmenelkir@gmail.com])
AC_CONFIG_AUX_DIR(config)
AM_INIT_AUTOMAKE()
AC_CONFIG_SRCDIR([libg15render.h])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIRS([m4])

# Checks for programs.
AC_PROG_CC
LT_INIT

# Checks for --enable args
AC_ARG_ENABLE(ttf, [  --enable-ttf		enable FreeType2 support],,[enable_ttf=no])
AS_IF([test "x$enable_ttf" != "xno"], [
    m4_ifdef([PKG_PROG_PKG_CONFIG], [
	PKG_PROG_PKG_CONFIG
	PKG_CHECK_MODULES(FREETYPE, freetype2,
		[
			AC_DEFINE(TTF_SUPPORT, [1], [Define to 1 to enable FreeType2 support])
			CFLAGS="$CFLAGS $FREETYPE_CFLAGS"
			FTLIB="$FREETYPE_LIBS"
		], [
			AS_IF([test "x$enable_ttf" = "xyes"], [
				AC_MSG_ERROR([Cannot find freetype2])
			])
		])
	], [
		AC_MSG_CHECKING(whether to enable FreeType2 support)
		AC_PATH_PROG([FTCONFIG], [freetype-config])
		AS_IF([test -n "$FTCONFIG" ], [
			CFLAGS="$CFLAGS `$FTCONFIG --cflags`"
			FTLIB="-lfreetype"
			AC_DEFINE(TTF_SUPPORT, [1])
			AC_MSG_RESULT([yes])
		], [
			AS_IF([test "x$enable_ttf" = "xyes"], [
				AC_MSG_ERROR([Cannot find freetype-config])
			], [
				AC_DEFINE(TTF_SUPPORT, [0])
			])
		])
		AC_MSG_RESULT([no])
	]
    )
], [
	AC_MSG_RESULT(No Freetype is being used)
])

# Checks for libraries.
AC_CHECK_LIB([g15], [writePixmapToLCD], ,AC_MSG_ERROR(["libg15 not found. please install it"]))
AC_CHECK_LIB([m], [ceil], ,AC_MSG_ERROR(["libm not found.  Please install it"]))

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST

# Checks for header files.
AC_CHECK_INCLUDES_DEFAULT
AC_PROG_EGREP

AC_CHECK_HEADERS([string.h ft2build.h])

# Checks for library functions.
AC_CHECK_INCLUDES_DEFAULT
AC_PROG_EGREP

AC_CHECK_FUNCS([memset])

AC_SUBST(FTLIB)
AC_CONFIG_FILES([Makefile])
AC_OUTPUT
