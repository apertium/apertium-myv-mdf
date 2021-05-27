AC_PREREQ(2.52)

AC_INIT([apertium-myv-mdf], [0.1.0], [trondtr@users.sourceforge.net])
AM_INIT_AUTOMAKE([apertium-myv-mdf], [0.1.0], no-define)
AC_PROG_AWK

PKG_CHECK_MODULES(APERTIUM, apertium >= 3.6.1)
PKG_CHECK_MODULES(LTTOOLBOX, lttoolbox >= 3.5.1)
PKG_CHECK_MODULES(CG3, cg3 >= 1.3.0)
PKG_CHECK_MODULES(APERTIUM_LEX_TOOLS, apertium-lex-tools >= 0.2.3)
PKG_CHECK_MODULES(HFST, hfst >= 3.15.0)

AC_PATH_PROGS(ZCAT, [gzcat zcat], [false])
AS_IF([test x$ZCAT = xfalse], [AC_MSG_ERROR([You don't have zcat nor gzcat installed])])

m4_ifdef([AP_CHECK_LING],[],[AC_MSG_ERROR([AP_CHECK_LING not defined, is apertium.m4 in ACLOCAL_PATH? See: https://wiki.apertium.org/wiki/Installation_troubleshooting])])

AP_CHECK_LING([1], [giella-myv])
AP_CHECK_LING([2], [giella-mdf])

AP_MKINCLUDE

AC_OUTPUT([Makefile])
