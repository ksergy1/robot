
include(FindPkgConfig)

pkg_check_modules(check REQUIRED check)

include_directories(.)
file(GLOB_RECURSE tests_src *.c *.h)
add_executable(tests ${tests_src})

set_target_properties(tests
                      PROPERTIES
                      COMPILE_FLAGS "${check_CFLAGS} ${misc_CFLAGS}")
target_link_libraries(tests
                      multigrid graph multigrid-converter
                      path-finder
                      ${check_LDFLAGS})

add_test(NAME tests COMMAND tests)
