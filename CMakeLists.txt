# Copyright (C) 2012 LuaDist.
# Created by Peter Drahoš, Peter Kapec
# Redistribution and use of this file is allowed according to the terms of the MIT license.
# For details see the COPYRIGHT file distributed with LuaDist.
# Please note that the package source code is licensed under its own license.

project ( lua-linenoise C )
cmake_minimum_required ( VERSION 2.8 )
include ( cmake/dist.cmake )
include ( lua )

set ( SRC_LINENOISE src/linenoise.c src/linenoiselib.c )

if ( WIN32 )
  set ( SRC_LINENOISE ${SRC_LINENOISE} src/win32fixes.c )
endif ()

# Binary
install_lua_module ( linenoise ${SRC_LINENOISE} )

install_data ( COPYING )
install_data ( README.md )
