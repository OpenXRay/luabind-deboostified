if (NOT LUABIND_BUILD_SHARED)
    add_library(xrLuabind STATIC)
else()
    add_library(xrLuabind SHARED)

    target_compile_definitions(xrLuabind
        PRIVATE
        LUABIND_DYNAMIC_LINK
    )
endif()

target_sources(xrLuabind PRIVATE
	class.cpp
	class_info.cpp
	class_registry.cpp
	class_rep.cpp
	create_class.cpp
	error.cpp
	exception_handler.cpp
	function.cpp
	function_introspection.cpp
	headertest.cpp
	inheritance.cpp
	link_compatibility.cpp
	memory.cpp
	object_rep.cpp
	open.cpp
	operator.cpp
	pcall.cpp
	scope.cpp
	set_package_preload.cpp
	stack_content_by_name.cpp
	weak_ref.cpp
	wrapper_base.cpp
)

target_include_directories(xrLuabind
	PUBLIC
    "${CMAKE_CURRENT_SOURCE_DIR}/.."
)

target_link_libraries(xrLuabind
	PUBLIC
	xrLuabindApi
)

if (XRAY_USE_LUAJIT)
    target_link_libraries(xrLuabind PUBLIC xrLuaJIT)
else()
    target_link_libraries(xrLuabind PUBLIC Lua51)
endif()

if (MASTER_GOLD)
    target_compile_definitions(xrLuabind
        PUBLIC
        LUABIND_NO_EXCEPTIONS
        LUABIND_NO_ERROR_CHECKING
    )
endif()

target_compile_options(xrLuabind
	PRIVATE
	$<$<CXX_COMPILER_ID:MSVC>:"/MP">
	$<$<CXX_COMPILER_ID:MSVC>:"/wd4251">
)

set_target_properties(xrLuabind PROPERTIES
	PREFIX ""
    POSITION_INDEPENDENT_CODE ON
)

install(TARGETS xrLuabind LIBRARY
	DESTINATION "${CMAKE_INSTALL_LIBDIR}"
)
