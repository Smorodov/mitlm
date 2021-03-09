cmake_minimum_required(VERSION 3.16.0 FATAL_ERROR)

project(libf2c C)
# Uncomment below to build and run in Unicode
add_definitions(-DUNICODE -D_UNICODE)

set(CMAKE_DEBUG_POSTFIX _d)
################################################################################
# Source groups
################################################################################
set(Header_Files
    #"src/arith.h"
    "src/ctype.h"
    "src/f2c.h"
    "src/fio.h"
    "src/fmt.h"
    "src/fp.h"
    "src/lio.h"
    "src/math.h"
    "src/signal1.h"
    "src/sysdep1.h"
)
source_group("Header Files" FILES ${Header_Files})

set(Source_Files
    "src/abort_.c"
#    "src/arithchk.c"
    "src/backspac.c"
    "src/c_abs.c"
    "src/c_cos.c"
    "src/c_div.c"
    "src/c_exp.c"
    "src/c_log.c"
    "src/c_sin.c"
    "src/c_sqrt.c"
    "src/cabs.c"
    "src/close.c"
    "src/d_abs.c"
    "src/d_acos.c"
    "src/d_asin.c"
    "src/d_atan.c"
    "src/d_atn2.c"
    "src/d_cnjg.c"
    "src/d_cos.c"
    "src/d_cosh.c"
    "src/d_dim.c"
    "src/d_exp.c"
    "src/d_imag.c"
    "src/d_int.c"
    "src/d_lg10.c"
    "src/d_log.c"
    "src/d_mod.c"
    "src/d_nint.c"
    "src/d_prod.c"
    "src/d_sign.c"
    "src/d_sin.c"
    "src/d_sinh.c"
    "src/d_sqrt.c"
    "src/d_tan.c"
    "src/d_tanh.c"
    "src/derf_.c"
    "src/derfc_.c"
    "src/dfe.c"
    "src/dolio.c"
    "src/dtime_.c"
    "src/due.c"
    "src/ef1asc_.c"
    "src/ef1cmc_.c"
    "src/endfile.c"
    "src/erf_.c"
    "src/erfc_.c"
    "src/err.c"
    "src/etime_.c"
    "src/exit_.c"
    "src/f77_aloc.c"
    "src/f77vers.c"
    "src/fmt.c"
    "src/fmtlib.c"
    "src/ftell_.c"
    "src/getarg_.c"
    "src/getenv_.c"
    "src/h_abs.c"
    "src/h_dim.c"
    "src/h_dnnt.c"
    "src/h_indx.c"
    "src/h_len.c"
    "src/h_mod.c"
    "src/h_nint.c"
    "src/h_sign.c"
    "src/hl_ge.c"
    "src/hl_gt.c"
    "src/hl_le.c"
    "src/hl_lt.c"
    "src/i77vers.c"
    "src/i_abs.c"
    "src/i_dim.c"
    "src/i_dnnt.c"
    "src/i_indx.c"
    "src/i_len.c"
    "src/i_mod.c"
    "src/i_nint.c"
    "src/i_sign.c"
    "src/iargc_.c"
    "src/iio.c"
    "src/ilnw.c"
    "src/inquire.c"
    "src/l_ge.c"
    "src/l_gt.c"
    "src/l_le.c"
    "src/l_lt.c"
    "src/lbitbits.c"
    "src/lbitshft.c"
    "src/lread.c"
    "src/lwrite.c"
    "src/main.c"
    "src/open.c"
    "src/pow_ci.c"
    "src/pow_dd.c"
    "src/pow_di.c"
    "src/pow_hh.c"
    "src/pow_ii.c"
    "src/pow_ri.c"
    "src/pow_zi.c"
    "src/pow_zz.c"
    "src/r_abs.c"
    "src/r_acos.c"
    "src/r_asin.c"
    "src/r_atan.c"
    "src/r_atn2.c"
    "src/r_cnjg.c"
    "src/r_cos.c"
    "src/r_cosh.c"
    "src/r_dim.c"
    "src/r_exp.c"
    "src/r_imag.c"
    "src/r_int.c"
    "src/r_lg10.c"
    "src/r_log.c"
    "src/r_mod.c"
    "src/r_nint.c"
    "src/r_sign.c"
    "src/r_sin.c"
    "src/r_sinh.c"
    "src/r_sqrt.c"
    "src/r_tan.c"
    "src/r_tanh.c"
    "src/rdfmt.c"
    "src/rewind.c"
    "src/rsfe.c"
    "src/rsli.c"
    "src/rsne.c"
    "src/s_cat.c"
    "src/s_cmp.c"
    "src/s_copy.c"
    "src/s_paus.c"
    "src/s_rnge.c"
    "src/s_stop.c"
    "src/sfe.c"
    "src/sig_die.c"
    "src/signal_.c"
    "src/sue.c"
    "src/system_.c"
    "src/typesize.c"
    "src/uio.c"
    "src/uninit.c"
    "src/util.c"
    "src/wref.c"
    "src/wrtfmt.c"
    "src/wsfe.c"
    "src/wsle.c"
    "src/wsne.c"
    "src/xwsne.c"
    "src/z_abs.c"
    "src/z_cos.c"
    "src/z_div.c"
    "src/z_exp.c"
    "src/z_log.c"
    "src/z_sin.c"
    "src/z_sqrt.c"
)
source_group("Source Files" FILES ${Source_Files})

set(ALL_FILES
    ${Header_Files}
    ${Source_Files}
)

################################################################################
# Target
################################################################################
add_library(${PROJECT_NAME} STATIC ${ALL_FILES})
add_executable(arithchk "src/arithchk.c")
################################################################################
# Compile definitions
################################################################################
add_definitions(#-DWIN32
                -DNO_SSIZE_T
                -DNO_FPINIT
                -D_LIB
                -D_CRT_SECURE_NO_WARNINGS
                -DUSE_CLOCK
                -DMSDOS
                -DNO_ONEXIT
                -DNO_My_ctype
                -DNO_ISATTY             
                )




