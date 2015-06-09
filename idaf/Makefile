## =============================================================================expat
##
## Global variables
##
## =============================================================================

username=`whoami`
prefix=/home/${username}/sw
basedir=${prefix}/src
WGET=wget -c
sf_projects="http://sourceforge.net/projects"

url_gnu="http://ftp.gnu.org/gnu"
url_apache="http://apache.xl-mirror.nl"

## === Package version ===============================================

version_apr=1.5.1
version_apr_util=1.5.4
version_autoconf=2.69
version_autogen=5.18.2
version_automake=1.14
version_cfitsio=3360
version_clang=3.5.1
series_cmake=3.1
version_cmake=${series_cmake}.1
version_curl=7.40.0
version_expat=2.1.0
version_file=5.17
version_git=2.2.2
version_gmp=5.1.3
version_gsl=1.16
version_gtk=3.12.2
version_guile=2.0.9
version_hdf5=1.8.12
version_libconfig=1.4.9
version_libffi=3.0.13
version_libiconv=1.14
version_libtool=2.4
version_libunistring=0.9
version_netcdf=4.3.1.1
version_ncurses=5.9
version_openmpi=1.6.5
version_openssl=1.0.2
version_pango=1.36.8
version_pcre=8.36
version_perl=5.20.1
version_ruby=2.2.0
version_scons=2.3.1
version_serf=1.3.8
version_sqlite=3080802
version_subversion=1.8.11
version_swig=3.0.5
version_szip=2.1
version_zlib=1.2.8

## =============================================================================
##
## Build targets
##
## =============================================================================

default: swir

swir: swir_devel

swir_devel: cmake git

swir_3rdparty: swir_devel gsl cfitsio netcdf

## === Apache Portable Runtime ======================================

apr:
	# Download and unpack the archive
	${WGET} http://apache.xl-mirror.nl//apr/apr-${version_apr}.tar.gz
	tar -xzf apr-${version_apr}.tar.gz
	# Configure package
	cd apr-${version_apr} && ./configure --prefix=${prefix}
	# Build and install package
	cd apr-${version_apr} && make && make install
	# Clean-up
	rm -rf apr-${version_apr}*

## === Apache Portable Runtime Utilities =============================

apr-util: apr
	# Download and unpack the archive
	${WGET} http://apache.xl-mirror.nl//apr/apr-util-${version_apr_util}.tar.gz
	tar -xzf apr-util-${version_apr_util}.tar.gz
	# Configure package
	cd apr-util-${version_apr_util} && ./configure --prefix=${prefix} --with-apr=${prefix}
	# Build and install package
	cd apr-util-${version_apr_util} && make && make install
	# Clean-up
	rm -rf apr-util-${version_apr_util}*

## === Autoconf ======================================================

autoconf:
	# Download and unpack the archive
	${WGET} ${url_gnu}/autoconf/autoconf-${version_autoconf}.tar.gz
	tar -xzf autoconf-${version_autoconf}.tar.gz
	# Configure package
	cd autoconf-${version_autoconf} && ./configure --prefix=${prefix}
	# Build and install package
	cd autoconf-${version_autoconf} && make && make install
	# Clean-up
	rm -rf autoconf-${version_autoconf}*

## === Autogen =======================================================

autogen: guile
	# Download and unpack the archive
	${WGET} ${url_gnu}/autogen/rel${version_autogen}/autogen-${version_autogen}.tar.gz
	tar -xzf autogen-${version_autogen}.tar.gz
	# Configure package
	cd autogen-${version_autogen} && ./configure --prefix=${prefix}
	# Clean-up
	rm -rf autogen-${version_autogen}*

## === Automakef =====================================================

automake: autoconf
	# Download and unpack the archive
	${WGET} ${url_gnu}/automake/automake-${version_automake}.tar.gz
	tar -xzf automake-${version_automake}.tar.gz
	# Configure package
	cd automake-${version_automake} && ./configure --prefix=${prefix}
	# Build and install package
	cd automake-${version_automake} && make && make install
	# Clean-up
	rm -rf file

## === Cairo =========================================================

cairo:
	${WGET} http://cairographics.org/releases/cairo-1.14.0.tar.xz
	tar -xJf cairo-1.14.0.tar.xz
	cd cairo-1.14.0 && ./configure --prefix=${prefix}

## === CFITSIO library ===============================================

cfitsio:
	# Download and unpack the archive
	${WGET} http://heasarc.gsfc.nasa.gov/FTP/software/fitsio/c/cfitsio${version_cfitsio}.tar.gz
	tar -xzf cfitsio${version_cfitsio}.tar.gz
	# Configure package
	cd cfitsio && ./configure --prefix=${prefix}
	# Build and install package
	cd cfitsio && make && make install
	# Clean-up
	rm -rf cfitsio*

## === LLVM and Clang ================================================

clang:
	# Download and unpack archives
	${WGET} http://llvm.org/releases/3.4/llvm-${version_clang}.src.tar.gz
	${WGET} http://llvm.org/releases/${version_clang}/clang-${version_clang}.src.tar.gz
	tar -xzf llvm-${version_clang}.src.tar.gz
	tar -xzf clang-${version_clang}.src.tar.gz
	# Move Clang sources into LLVM code base
	mv clang-${version_clang} llvm-${version_clang}/tools/clang
	# Configure package
	cd llvm-${version_clang} && ./configure --prefix=${prefix}
	# Build and install  package
	cd llvm-${version_clang} && make && make install
	# Clean-up
	rm -rf llvm-${version_clang}*
	rm -rf clang-${version_clang}*

## === CMake Makefile generator ======================================

cmake: ncurses_patch
	# Download and unpack archive
	${WGET} http://www.cmake.org/files/v${series_cmake}/cmake-${version_cmake}.tar.gz
	tar -xzf cmake-${version_cmake}.tar.gz
	# Configure package
	cd cmake-${version_cmake} && ./bootstrap --prefix=${prefix}
	# Build and install package
	cd cmake-${version_cmake} && make && make install
	# Clean-up
	rm -rf cmake-${version_cmake}*
	rm -rf ${prefix}/include/ncurses/ncurses

## === cURL library ==================================================

curl: openssl zlib
	# Download and unpack archive
	${WGET} http://curl.haxx.se/download/curl-${version_curl}.tar.gz
	tar -xzf curl-${version_curl}.tar.gz
	# Configure package
	cd curl-${version_curl} && ./configure --prefix=${prefix} --with-zlib=${prefix} --with-ssh=${prefix} 
	# Build and install package
	cd curl-${version_curl} && make && make install
	# Clean-up
	rm -rf curl-${version_curl}*

## === Editra editor =================================================

editra:
	${WGET} http://editra.googlecode.com/files/Editra-0.7.20.tar.gz
	tar -xzf Editra-0.7.20.tar.gz

## === Expat XML parsing library =====================================

expat:
	# Download and unpack archive
	${WGET} ${sf_projects}/expat/files/expat/${version_expat}/expat-${version_expat}.tar.gz/download -O expat-${version_expat}.tar.gz
	tar -xzf expat-${version_expat}.tar.gz
	# Configure package
	cd expat-${version_expat} && ./configure --prefix=${prefix}
	# Build package
	cd expat-${version_expat} && make && make install
	# Clean-up
	rm -rf expat-${version_expat}*

## === File identification library ===================================

file: autoconf automake libtool
	git clone https://github.com/glensc/file.git
	# Configure package
	cd file && libtoolize --force  && aclocal && autoheader && automake --force-missing --add-missing
	cd file && ${prefix}/bin/autoconf
	cd file && ./configure --prefix=${prefix}
	cd file && make && make install
	rm -rf file

## === Git source control ============================================

git: curl expat libiconv subversion
	# Download and unpack archive
	${WGET} https://www.kernel.org/pub/software/scm/git/git-${version_git}.tar.gz
	tar -xzf git-${version_git}.tar.gz
	# Configure package
	cd git-${version_git} && ./configure --prefix=${prefix} --with-zlib=${prefix} --with-iconv=${prefix} --with-openssl=${prefix} --with-expat=${prefix} --with-curl=${prefix}
	# Build and install package
	cd git-${version_git} && make && make install
	# Clean-up
	rm -rf git-${version_git}*

## === GNU MP ========================================================

gmp:
	# Download and unpack archive
	${WGET} http://ftp.gnu.org/pub/gnu/gmp/gmp-${version_gmp}.tar.gz
	tar -xzf gmp-${version_gmp}.tar.gz
	# Configure package
	cd gmp-${version_gmp} && ./configure --prefix=${prefix}
	# Build and install package
	cd gmp-${version_gmp} && make && make install
	# Clean-up
	rm -rf gmp-${version_gmp}*

## === GNU Scientific Library (GSL) ==================================

gsl:
	# Download and unpack archive
	${WGET} http://gnu.xl-mirror.nl/gsl/gsl-${version_gsl}.tar.gz
	tar -xzf gsl-${version_gsl}.tar.gz
	# Configure package
	cd gsl-${version_gsl} && ./configure --prefix=${prefix}
	@echo " [gsl] Build and install package"
	cd gsl-${version_gsl} && make && make install
	@echo " [gsl] Clean-up"
	rm -rf gsl-${version_gsl}*

## === GTK ===========================================================

gtk: pango
	${WGET} http://ftp.gnome.org/pub/gnome/sources/gtk+/3.12/gtk+-${version_gtk}.tar.xz
	tar -xJf gtk+-${version_gtk}.tar.xz
	cd  gtk+-${version_gtk} && ./configure --prefix=${prefix}

## === Guile library =================================================

guile: libtool gmp libunistring libffi
	# Download and unpack archive
	${WGET} ${url_gnu}/guile/guile-${version_guile}.tar.gz
	tar -xzf guile-${version_guile}.tar.gz
	# Configure package
	export LIBFFI_LIBS=${prefix}/lib
	export LIBFFI_CFLAGS=${prefix}/include
	cd guile-${version_guile} && LIBFFI_CFLAGS=${prefix} ./configure --prefix=${prefix} CPPFLAGS='-I${prefix}/include' LDFLAGS='-L${prefix}/lib'
	# Build and install package
	cd guile-${version_guile} && make && make install
	# Clean-up
	rm -rf guile-${version_guile}*

## === HDF5 library ==================================================

hdf5: szip openmpi
	# Download and unpack archive
	${WGET} http://www.hdfgroup.org/ftp/HDF5/current/src/hdf5-${version_hdf5}.tar.gz
	tar -xzf hdf5-${version_hdf5}.tar.gz
	# Configure package
	cd hdf5-${version_hdf5} && CC=mpicc ./configure --prefix=${prefix} --with-szlib=${prefix} --enable-parallel
	# Build and install package
	cd hdf5-${version_hdf5} && make && make install
	# Clean-up
	rm -rf hdf5-${version_hdf5}*

## === libconfig - C/C++ Configuration File Library ==================

libconfig:
	# Download and unpack archive
	${WGET} http://www.hyperrealm.com/libconfig/libconfig-${version_libconfig}.tar.gz
	tar -xzf libconfig-${version_libconfig}.tar.gz
	# Configure package
	cd libconfig-${version_libconfig} && ./configure --prefix=${prefix}
	# Build and install package
	cd libconfig-${version_libconfig} && make && make install
	# Clean-up
	rm -rf libconfig-${version_libconfig}*

## === Portable Foreign Function Interface Library (libffi) ==========

libffi:
	# Download and unpack archive
	${WGET} http://www.mirrorservice.org/sites/sourceware.org/pub/libffi/libffi-${version_libffi}.tar.gz
	tar -xzf libffi-${version_libffi}.tar.gz
	# Configure package
	cd libffi-${version_libffi} && ./configure --prefix=${prefix}
	# Build and install package
	cd libffi-${version_libffi} && make && make install
	## Clean-up
	rm -rf libffi-${version_libffi}*

## === IConv library =================================================

libiconv:
	# Download and unpack archive
	${WGET} ${url_gnu}/libiconv/libiconv-${version_libiconv}.tar.gz
	tar -xzf libiconv-${version_libiconv}.tar.gz
	# Configure package
	cd libiconv-${version_libiconv} && ./configure --prefix=${prefix}
	# Build package
	cd libiconv-${version_libiconv} && make && make install
	# Clean-up
	rm -rf libiconv-${version_libiconv}*

## === Libtool =======================================================

libtool:
	# Download and unpack archive
	${WGET} ${url_gnu}/libtool/libtool-${version_libtool}.tar.gz
	tar -xzf libtool-${version_libtool}.tar.gz
	# Configure package
	cd libtool-${version_libtool} && ./configure --prefix=${prefix}
	# Build and install package
	cd libtool-${version_libtool} && make && make install
	# Clean-up
	rm -rf libtool-${version_libtool}*

## === Libunistring ==================================================

libunistring:
	# Download and unpack archive
	${WGET} http://ftp.gnu.org/pub/gnu/libunistring/libunistring-${version_libunistring}.tar.gz
	tar -xzf libunistring-${version_libunistring}.tar.gz
	# Configure package
	cd libunistring-${version_libunistring} && ./configure --prefix=${prefix}
	# Build and install package
	cd libunistring-${version_libunistring} && make && make install
	# Clean-up
	rm -rf libunistring-${version_libunistring}*

## === NetCDF (network Common Data Form) =============================

#netcdf: git hdf5
netcdf:
	@echo " [netcdf] Download and unpack archive"
	${WGET} https://github.com/Unidata/netcdf-c/archive/v${version_netcdf}.tar.gz
	tar -xzf v${version_netcdf}
	@echo " [netcdf] Configure package"
	cd netcdf-c-${version_netcdf} && ./configure --prefix=${prefix}
	@echo " [netcdf] Build and install package"
	cd netcdf-c-${version_netcdf} && make

## === NCurses library ===============================================

ncurses:
	# Download and unpack archive
	${WGET} ${url_gnu}/ncurses/ncurses-${version_ncurses}.tar.gz
	tar -xzf ncurses-${version_ncurses}.tar.gz
	# Configure package
	cd ncurses-${version_ncurses} && ./configure --prefix=${prefix}
	# Build and install package
	cd ncurses-${version_ncurses} && make && make install
	# Clean-up
	rm -rf ncurses-${version_ncurses}*

ncurses_patch: ncurses
	cd ${prefix}/include && tar -cvzf ncurses.tgz ncurses
	cd ${prefix}/include/ncurses && tar -xzf ../ncurses.tgz
	rm ${prefix}/include/ncurses.tgz

## === Open MPI ======================================================

openmpi:
	# Download and unpack archive
	${WGET} http://www.open-mpi.org/software/ompi/v1.6/downloads/openmpi-${version_openmpi}.tar.gz
	tar -xzf openmpi-${version_openmpi}.tar.gz
	# Configure package
	cd openmpi-${version_openmpi} && ./configure --prefix=${prefix}
	# Build and install package
	cd openmpi-${version_openmpi} && make && make install
	# Clean-up
	rm -rf openmpi-${version_openmpi}*

## === OpenSSL encryption library ====================================

# On Fedora and Red Hat systems, be sure to export
# CFLAGS="-fPIC" and explicitly specify 'shared' to
# config. Failing to do so will result in static
# libraries only.That is, you will be missing the
# shared objects and engines.

openssl:
	# Download archive
	${WGET} http://www.openssl.org/source/openssl-${version_openssl}.tar.gz
	# Expand archive
	tar -xzf openssl-${version_openssl}.tar.gz
	# Configure, build and install
	cd openssl-${version_openssl} && ./config --prefix=${prefix} --openssldir=${prefix}/share/openssl shared
	cd openssl-${version_openssl} && CFLAGS="-fPIC" make && make install
	# Clean-up
	rm -rf openssl-${version_openssl}*

## === Pango =========================================================

pango: cairo
	${WGET} http://ftp.gnome.org/pub/GNOME/sources/pango/1.36/pango-1.36.8.tar.xz
	tar xJf pango-1.36.8.tar.xz
	cd pango-1.36.8 && ./config --prefix=${prefix}

## === Perl Compatible Reglar Expressions ============================

pcre: perl
	${WGET} http://downloads.sourceforge.net/project/pcre/pcre/${version_pcre}/pcre-${version_pcre}.tar.gz
	tar -xzf pcre-${version_pcre}.tar.gz
	# Configure package
	cd pcre-${version_pcre} && ./configure --prefix=${prefix} --enable-pcre16 --enable-pcre32 --enable-pcregrep-libz --datadir=${prefix}/share
	# Build and install
	cd pcre-${version_pcre} && make && make install
	# Clean-up
	rm -rf pcre-${version_pcre}*

## === Perl ==========================================================

perl:
	${WGET} http://www.cpan.org/src/5.0/perl-${version_perl}.tar.gz
	tar -xzf perl-${version_perl}.tar.gz
	# Configure package
	cd perl-${version_perl} && ./Configure -des -Dprefix=${prefix}
	# Build and install package
	cd perl-${version_perl} && make && make install
	# Clean-up
	rm -rf perl-${version_perl}*

## === Ruby ==========================================================

ruby:
	${WGET} http://cache.ruby-lang.org/pub/ruby/2.2/ruby-${version_ruby}.tar.gz
	tar -xzf ruby-${version_ruby}.tar.gz
	# Configure package
	cd ruby-${version_ruby} && ./configure --prefix=${prefix}
	#Build and (if successful) install package
	cd ruby-${version_ruby} && make && make install

## === Scons =========================================================

scons:
	${WGET} http://downloads.sourceforge.net/project/scons/scons/${version_scons}/scons-${version_scons}.tar.gz
	tar -xzf scons-${version_scons}.tar.gz
	# Configure package
	cd scons-${version_scons} && python setup.py install --prefix=${prefix}
	# Clean-up
	rm -rf scons-${version_scons}*

## === Serf library ==================================================

serf: scons
	# Download and unpack archive
	${WGET} http://serf.googlecode.com/svn/src_releases/serf-${version_serf}.tar.bz2
	tar jxf serf-${version_serf}.tar.bz2
	# Configure package
	cd serf-${version_serf} && scons APR=${prefix} APU=${prefix} PREFIX=${prefix}
	# Install package
	cd serf-${version_serf} && scons PREFIX=${prefix} install
	# Clean-up
	rm -rf serf-${version_serf}*

## === SQLite ========================================================

sqlite:
	${WGET} http://sqlite.org/2015/sqlite-autoconf-${version_sqlite}.tar.gz
	tar -xzf sqlite-autoconf-${version_sqlite}.tar.gz
	# Configure package
	cd sqlite-autoconf-${version_sqlite} && ./configure --prefix=${prefix}
	# Build and install package
	cd sqlite-autoconf-${version_sqlite} && make && make install
	# Clean-up
	rm -rf sqlite-autoconf-${version_sqlite}*

## === Subversion ====================================================

subversion: apr-util sqlite serf pcre
	# Download and unpack archive
	${WGET} ${url_apache}/subversion/subversion-${version_subversion}.tar.gz
	tar -xzf subversion-${version_subversion}.tar.gz
	# Configure package
	cd subversion-${version_subversion} && ./configure --prefix=${prefix} --with-apr=${prefix} --with-apr-util=${prefix} --with-sqlite=${prefix} --with-serf=${prefix}
	# Build and install package
	cd subversion-${version_subversion}	&& make && make install
	# Build and install bindings
	cd subversion-${version_subversion} && make swig-pl && make install-swig-pl
	# Clean-up
	rm -rf subversion-${version_subversion}*

## === SWIG ==========================================================

swig: pcre
	# Download and unpack archive
	${WGET} http://downloads.sourceforge.net/project/swig/swig/swig-${version_swig}/swig-${version_swig}.tar.gz
	tar -xzf swig-${version_swig}.tar.gz
	# Configure package
	cd swig-${version_swig} && ./configure --prefix=${prefix} --with-pcre-prefix=${prefix}
	# Build and install bindings
	cd swig-${version_swig} && make && make install
	# Clean-up
	rm -rf swig-${version_swig}*

## === SZIP compression library ======================================

szip:
	@echo " [szip] Download and unpack archive"
	${WGET} http://www.hdfgroup.org/ftp/lib-external/szip/2.1/src/szip-${version_szip}.tar.gz
	tar -xzf szip-${version_szip}.tar.gz
	@echo " [szip] Configure package"
	cd szip-${version_szip} && ./configure --prefix=${prefix}
	@echo " [szip] Build and install package"
	cd szip-${version_szip} && make && make install
	@echo " [szip] Clean-up"
	rm -rf szip-${version_szip}*

## === wxWidgets =====================================================

wxWidgets:
	@echo " [wxWidgets] Check out working copy from SVN"
	svn checkout http://svn.wxwidgets.org/svn/wx/wxWidgets/trunk wxWidgets
	@echo " [wxWidgets] Configure package"
	cd wxWidgets && ./configure --prefix=${prefix}
	@echo " [wxWidgets] Clean-up"

## === ZLIB compression library ======================================

zlib:
	cd ${basedir}
	@echo " [zlib] Download and unpack archive"
	${WGET} http://zlib.net/zlib-${version_zlib}.tar.gz
	tar -xzf zlib-${version_zlib}.tar.gz
	@echo " [zlib] Configure package"
	cd zlib-${version_zlib} && ./configure --prefix=${prefix}
	@echo " [zlib] Build and install the package"
	cd zlib-${version_zlib} && make && make install
	@echo " [zlib] Clean-up"
	rm -rf zlib-${version_zlib}*

## =============================================================================
##
##  Clean-up
##
## =============================================================================

clean:
	rm -f *.tgz
	rm -f *.gz

distclean:
	rm -rf ${prefix}/bin
	rm -rf ${prefix}/doc
	rm -rf ${prefix}/docs
	rm -rf ${prefix}/etc
	rm -rf ${prefix}/include
	rm -rf ${prefix}/lib
	rm -rf ${prefix}/lib64
	rm -rf ${prefix}/libexec
	rm -rf ${prefix}/man
	rm -rf ${prefix}/share
	rm -rf ${prefix}/ssl
