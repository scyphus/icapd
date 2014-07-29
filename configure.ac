#
# Copyright (c) 2014 Scyphus Solutions Co. Ltd.  All rights reserved.
# Authors:
#      Hirochika Asai  <asai@scyphus.co.jp>
#

AC_PREREQ(2.59)
AC_INIT([icap], [0.1.0], [bug@scyphus.co.jp])
AC_CONFIG_SRCDIR([icapctl.c])
AC_CONFIG_HEADER([config.h])

# Get hostname and other information.
AC_CANONICAL_BUILD
AC_CANONICAL_HOST
AC_CANONICAL_TARGET

AM_INIT_AUTOMAKE
AC_SUBST(SUBDIRS)

# arguments
AC_ARG_ENABLE(debug,
  [  --enable-debug    Turn on debugging [default no]],
  [case "${enableval}" in
    yes) debug=yes; AC_MSG_RESULT(Checking for debug... yes); AC_DEFINE(DEBUG, 1, debugging option) ;;
    no)  debug=no;;
    *) AC_MSG_ERROR(bad value ${enableval} for --enable-debug) ;;
  esac],[debug=no])
AM_CONDITIONAL(DEBUG, test x$debug = xtrue)

# Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL
#AC_PROG_LIBTOOL

# Checks for libraries.

# Checks for header files.
AC_CHECK_HEADERS([stdlib.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST

# Checks for library functions.
#AC_CHECK_FUNCS([])

# configure date
CONFDATE=`date '+%Y%m%d'`
AC_SUBST(CONFDATE)

# set paths for state directory
if test "${prefix}" = "NONE"; then
  icap_statedir_prefix="";
else
  icap_statedir_prefix=${prefix}
fi
if test "${localstatedir}" = '${prefix}/var'; then
  AC_CACHE_CHECK(state directory,ac_cv_statedir,
  [for ICAP_STATE_DIR in ${icap_statedir_prefix}/var/run dnl
                        ${icap_statedir_prefix}/var/adm dnl
                        ${icap_statedir_prefix}/etc dnl
                        /var/run dnl
                        /var/adm dnl
                        /etc dnl
                        /dev/null;
  do
    test -d $ICAP_STATE_DIR && break
  done
  icap_statedir=$ICAP_STATE_DIR])
else
  icap_statedir=${localstatedir}
  AC_MSG_CHECKING(directory to use for state file)
  AC_MSG_RESULT(${icap_statedir})
  AC_SUBST(icap_statedir)
fi
if test $icap_statedir = "/dev/null"; then
    AC_MSG_ERROR('STATE DIRECTORY NOT FOUND! FIX OR SPECIFY --localstatedir!')
fi
AC_DEFINE_UNQUOTED(PATH_ICAPD_PID, "$icap_statedir/icapd.pid", nsd PID)

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
