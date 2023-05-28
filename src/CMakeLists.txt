add_executable(global global.c)
set_target_properties(global PROPERTIES LINKER_LANGUAGE C)

add_executable(leak leak.cpp)

add_executable(overrun overrun.c)
set_target_properties(overrun PROPERTIES LINKER_LANGUAGE C)

add_executable(stack stack.c)
set_target_properties(stack PROPERTIES LINKER_LANGUAGE C)

add_executable(tiny tiny.cpp)

add_executable(uar uar.cpp)

add_executable(undefined undefined.cpp)

add_executable(uninit uninit.c)
set_target_properties(uninit PROPERTIES LINKER_LANGUAGE C)
