#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_INIT([libg15render],[3.0.4],[menelkir@itroll.org])
AC_CONFIG_AUX_DIR(config)
AM_INIT_AUTOMAKE()
AC_CONFIG_SRCDIR([libg15render.h])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIRS([m4])

# Checks for programs.
AC_PROG_CC
LT_INIT

# Checks for --enable args
AC_MSG_CHECKING(whether to enable FreeType2 support)
AC_ARG_ENABLE(ttf, [  --enable-ttf		enable FreeType2 support],
	if [[[ "$enableval" = "yes" ]]]; then
		AC_DEFINE(TTF_SUPPORT, [1], [Define to 1 to enable FreeType2 support])
		CFLAGS="$CFLAGS `freetype-config --cflags`"
		FTLIB="-lfreetype"
		ttf_support="yes"
	else
		ttf_support="no"
	fi,
	ttf_support="no"
)
AC_MSG_RESULT($ttf_support)

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
