set(LUABIND_SOURCES
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

set(LUABIND_API_HEADERS
	../luabind/back_reference.hpp
	../luabind/back_reference_fwd.hpp
	../luabind/class.hpp
	../luabind/class_info.hpp
	../luabind/config.hpp
	../luabind/error.hpp
	../luabind/error_callback_fun.hpp
	../luabind/exception_handler.hpp
	../luabind/lua_extensions.hpp
	../luabind/from_stack.hpp
	../luabind/function.hpp
	../luabind/function_introspection.hpp
	../luabind/get_main_thread.hpp
	../luabind/handle.hpp
	../luabind/luabind.hpp
	../luabind/lua_argument_proxy.hpp
	../luabind/lua_include.hpp
	../luabind/lua_index_proxy.hpp
	../luabind/lua_iterator_proxy.hpp
	../luabind/lua_proxy.hpp
	../luabind/lua_proxy_interface.hpp
	../luabind/lua_state_fwd.hpp
	../luabind/make_function.hpp
	../luabind/memory.hpp
	../luabind/memory_allocator.hpp
	../luabind/nil.hpp
	../luabind/no_dependency.hpp
	../luabind/object.hpp
	../luabind/open.hpp
	../luabind/operator.hpp
	../luabind/pointer_traits.hpp
	../luabind/prefix.hpp
	../luabind/scope.hpp
	../luabind/set_package_preload.hpp
	../luabind/shared_ptr_converter.hpp
	../luabind/typeid.hpp
	../luabind/types.hpp
	../luabind/version.hpp
	../luabind/weak_ref.hpp
	../luabind/wrapper_base.hpp

)

set(LUABIND_DETAIL_API_HEADER
	../luabind/detail/call.hpp
	../luabind/detail/call_function.hpp
	../luabind/detail/call_member.hpp
	../luabind/detail/call_shared.hpp
	../luabind/detail/call_traits.hpp
	../luabind/detail/class_registry.hpp
	../luabind/detail/class_rep.hpp
	../luabind/detail/constructor.hpp
	../luabind/detail/conversion_storage.hpp
	../luabind/detail/convert_to_lua.hpp
	../luabind/detail/crtp_iterator.hpp
	../luabind/detail/debug.hpp
	../luabind/detail/decorate_type.hpp
	../luabind/detail/deduce_signature.hpp
	../luabind/detail/enum_maker.hpp
	../luabind/detail/format_signature.hpp
	../luabind/detail/garbage_collector.hpp
	../luabind/detail/has_get_pointer.hpp
	../luabind/detail/inheritance.hpp
	../luabind/detail/instance_holder.hpp
	../luabind/detail/link_compatibility.hpp
	../luabind/detail/make_instance.hpp
	../luabind/detail/meta.hpp
	../luabind/detail/most_derived.hpp
	../luabind/detail/object.hpp
	../luabind/detail/object_rep.hpp
	../luabind/detail/open.hpp
	../luabind/detail/operator_id.hpp
	../luabind/detail/other.hpp
	../luabind/detail/pcall.hpp
	../luabind/detail/pointee_sizeof.hpp
	../luabind/detail/pointee_typeid.hpp
	../luabind/detail/policy.hpp
	../luabind/detail/primitives.hpp
	../luabind/detail/property.hpp
	../luabind/detail/ref.hpp
	../luabind/detail/signature_match.hpp
	../luabind/detail/stack_utils.hpp
	../luabind/detail/typetraits.hpp
	../luabind/detail/yes_no.hpp
)

set(LUABIND_DEFAULT_POLICIES_HEADERS
	../luabind/detail/conversion_policies/conversion_base.hpp
	../luabind/detail/conversion_policies/conversion_policies.hpp
	../luabind/detail/conversion_policies/enum_converter.hpp
	../luabind/detail/conversion_policies/function_converter.hpp
	../luabind/detail/conversion_policies/lua_proxy_converter.hpp
	../luabind/detail/conversion_policies/native_converter.hpp
	../luabind/detail/conversion_policies/pointer_converter.hpp
	../luabind/detail/conversion_policies/reference_converter.hpp
	../luabind/detail/conversion_policies/value_converter.hpp
)

set(LUABIND_USER_POLICIES_HEADERS
	../luabind/adopt_policy.hpp
	../luabind/container_policy.hpp
	../luabind/copy_policy.hpp
	../luabind/dependency_policy.hpp
	../luabind/discard_result_policy.hpp
	../luabind/iterator_policy.hpp
	../luabind/out_value_policy.hpp
	../luabind/raw_policy.hpp
	../luabind/return_reference_to_policy.hpp
	../luabind/yield_policy.hpp
)


set(LUABIND_EXTRA_LIBS)
if(MSVC)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /wd4251")
elseif(CMAKE_COMPILER_IS_GNUCXX)
	list(APPEND LUABIND_EXTRA_LIBS m)
endif()

if(LUABIND_BUILD_SHARED)
	message("Build shared lib")
	add_library(${PROJECT_NAME} SHARED ${LUABIND_SOURCES} ${LUABIND_API_HEADERS} ${LUABIND_DETAIL_API_HEADERS} ${LUABIND_DEFAULT_POLICIES_HEADERS} ${LUABIND_USER_POLICIES_HEADERS})
	set_target_properties(${PROJECT_NAME} PROPERTIES PREFIX "")
else()
	message("Build static lib")
	add_library(${PROJECT_NAME} STATIC ${LUABIND_SOURCES} ${LUABIND_API_HEADERS} ${LUABIND_DETAIL_API_HEADERS} ${LUABIND_DEFAULT_POLICIES_HEADERS} ${LUABIND_USER_POLICIES_HEADERS})
endif()
target_link_libraries(${PROJECT_NAME} ${LUA_LIBRARIES} ${LUABIND_EXTRA_LIBS})

install(TARGETS ${PROJECT_NAME} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} PERMISSIONS OWNER_READ OWNER_WRITE 
    GROUP_READ 
    WORLD_READ )

