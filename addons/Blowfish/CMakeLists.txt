# Base Io build system
# Written by Jeremy Tregunna <jeremy.tregunna@me.com>
#
# Builds the Blowfish addon

# Create the _build bundle hierarchy if needed.
make_build_bundle(_build)

# Output our dynamic library to the top-level _build hierarchy
set(LIBRARY_OUTPUT_PATH ${CMAKE_CURRENT_BINARY_DIR}/_build/dll)

# Generate the IoBlowfishInit.c file.
# Argument SHOULD ALWAYS be the exact name of the addon, case is
# important.
generate_ioinit(Blowfish)

# Our library sources.
set(SRCS
	"${CMAKE_CURRENT_SOURCE_DIR}/source/blowfish.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/source/IoBlowfish.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/source/IoBlowfishInit.c"
)

# Now build the shared library
add_library(IoBlowfish SHARED ${SRCS})
add_dependencies(IoBlowfish iovmall)
target_link_libraries(IoBlowfish iovmall)

# Install the addon to our global addons hierarchy.
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} DESTINATION lib/io/addons)
install(DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/_build DESTINATION lib/io/addons/Blowfish)
